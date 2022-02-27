# CS Regex Reference Guide

If you're a customer science engineer, in any language, learning how to use and understand Regex expressions is a must.

## Summary

This is a general reference guide on how to understand and use some basic Regex
Expressions. I've broken down specific functions below with basic examples and
real-life scenarios where the associted regex expression would be useful.

---

## Useage

To use this reference guide, you can either **[navigate to my website](https://erikplachta.github.io/cs-regex-reference-guide/)**, or scroll down for for the markdown version.

---

## Repo Stats

[![GitHub license](https://img.shields.io/github/license/ErikPlachta/cs-regex-reference-guide)](https://github.com/ErikPlachta/cs-regex-reference-guide) [![GitHub Number of Languages](https://img.shields.io/github/languages/count/ErikPlachta/cs-regex-reference-guide)](https://github.com/ErikPlachta/cs-regex-reference-guide)
[![GitHub top Language](https://img.shields.io/github/languages/top/ErikPlachta/cs-regex-reference-guide)](https://github.com/ErikPlachta/cs-regex-reference-guide)
[![GitHub issues](https://img.shields.io/github/issues/ErikPlachta/cs-regex-reference-guide)](https://github.com/ErikPlachta/cs-regex-reference-guide/issues)
![GitHub last commit](https://img.shields.io/github/last-commit/erikplachta/cs-regex-reference-guide)

## Table of Contents

- [CS Regex Reference Guide](#cs-regex-reference-guide)
  - [Summary](#summary)
  - [Useage](#useage)
  - [Repo Stats](#repo-stats)
  - [Table of Contents](#table-of-contents)
- [Regex - Regular Expressions](#regex---regular-expressions)
  - [What are some other ways to explain Regular Expressions?](#what-are-some-other-ways-to-explain-regular-expressions)
  - [Regular Expressions Are ~~not~~ Easy to Understand](#regular-expressions-are-not-easy-to-understand)
  - [Four Cateogires of Regex Expression Values](#four-cateogires-of-regex-expression-values)
    - [1. Literal Characters](#1-literal-characters)
    - [2. Meta Characters](#2-meta-characters)
    - [3. Quantifiers](#3-quantifiers)
    - [4. Positions](#4-positions)
  - [Examples with Explinations](#examples-with-explinations)
    - [Example - Phone Number](#example---phone-number)
    - [Example - Email Address](#example---email-address)
    - [Regex Components](#regex-components)
    - [Anchors](#anchors)
    - [Quantifiers](#quantifiers)
    - [OR Operator](#or-operator)
    - [Character Classes](#character-classes)
    - [Flags](#flags)
    - [Grouping and Capturing](#grouping-and-capturing)
    - [Bracket Expressions](#bracket-expressions)
    - [Greedy and Lazy Match](#greedy-and-lazy-match)
    - [Boundaries](#boundaries)
    - [Back-references](#back-references)
    - [Look-ahead and Look-behind](#look-ahead-and-look-behind)
  - [Author](#author)
  - [Contact Me](#contact-me)
  - [Resources and References](#resources-and-references)

---

# Regex - Regular Expressions

**A regular expression, *aka regex*, is used to simplify advanced searching/filtering
of content based on a user-specified search patern.**
> You define what you are searching at the level of precision you need.

**What makes a regex search/filter different from others is that it searches for
patterns in ASCII or unicode characters.**
> You're not just looking for a specific character value, you're looking for all
> instances of a pattern within the content. For example, all phone-numbers,
> email-addresses, websites, or really any type of content that folows a
> universal pattern.

---

## What are some other ways to explain Regular Expressions?

Great questions!

The [MDN team said,](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)
> "*Regular expressions are patterns used to match character combinations in strings.*"

[Wikipedia says,](https://en.wikipedia.org/wiki/Regular_expression)
> "*A regular expression is a sequence of characters that specifies a search pattern in text. Usually such patterns are used by string-searching algorithms for "find" or "find and replace" operations on strings, or for input validation.*"

---

## Regular Expressions Are ~~not~~ Easy to Understand

At first glance, a regex pattern can be intimidating.
> For example of searching for an email address `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` 🤯

It's much less complicated than it appears, so let's break it down! 👇🏼

## Four Cateogires of Regex Expression Values

A regex pattern, *the search / filter you're creating*, is Broken Down 4 Categories

### 1. Literal Characters

Any/all ASCII or unicode characters you're wanting to search for or filter out. 
This will include sincle characters

| Syntax | Description                |
|--------|----------------------------|
| **`a-z`** | Any lower-case letters  |
| **`A-Z`** | Any upper-case letters  |
| **`0-9`** | Any digits |
| Unicodes  | There's a lot. here's an index -> *[Microsoft - Insert ASCII or Unicode Latin-based symbols and characters](https://support.microsoft.com/en-gb/office/insert-ascii-or-unicode-latin-based-symbols-and-characters-d13f58d3-7bcb-44a7-a4d5-972ee12e50e0)* |

---

### 2. Meta Characters

Regex operator that represent specific data-types within the ASCI or Unicode
character sets.

| Syntax | Description  | Note | Example |
|--------|--------------|------|---------|
| **`\`** | Converts ASCI or Unicode character **into meta-characters** | *WARNING: If you don't use this it will be considered a literal-character!* | |
| **`/^`**| Any new line |
| **`.`** | Any ASCI or Unicode Character.| *WARNING: Use with caution. It's a broad grab.* | |
| **`\d`**| Any Digit 0-9 | | |
| **`\w`**| Anything that is a word-character | *`A-Z`*, *`a-z`*, **`0-9`** |  **`\w\w`** -> Returns any sequent of two word-characters. |
| **`\W`**| Anything that is NOT a word-character |   |   |
| **`\s`**| Any white-space characters. |`Space`, `Tab`, and sometimes `new-line`| **`\s\s`** -> Returns any sequent of two white-space characters|
| **`\S`**| Anything that is NOT white-space. | `Space`, `Tab`, and sometimes `new-line` |

---

> New Lines  *New-line has abnormal rules I need to add here*

### 3. Quantifiers

... are a meta character that modify the pervious meta characters in a regular
expesion.
> Based on your regex search paramters, how many of times do you want it to 
> match in a row?

| Syntax | Description  |   Example   |
|--------|--------------|-------------|
| **`*`**|  0 or more   | |
| **`+`**|  1 or more   | |
| **`?`**|  0 or 1      | **`test?t`** -> all combonations of `test` and `testt` where the second T is optional        |
| **`{min,max}`**|Range | **`\w{1,5}`** -> All word-character combonations with 1-5 characters followed by white-space |
| **`{n}`**| ?          | **`\w{5}\s`** -> All word-character combonations with 5 character followed by white-space    |

---

### 4. Positions

... are used to match the location of a litercal character within your defined 
searach-paramters.

| Syntax  | Description  |   Example   |
|---------|--------------|-------------|
| **`^`** |  The beganning of line | **Lines with only 1 word:** -> **`^\w+$** -> Any new line followed by a word-character followed by end of line. | 
| **`$`** |  The End of the line   |  |
| **`\b`** |  A word boundry       | **All 4 letter words** -> **`\b\w{4}`** -> Looking at each word, look ALL word-character values of length 4. |

---

## Examples with Explinations

Now that we've covered all of the details, let's look at some basic examples to
tie it all togther.

### Example - Phone Number

Without the area-code, phone numbers are generally 9-digits.
- We can look for 9 digits like this `\d\d\d-\d\d\d-\d\d\d\d`
  - Here, we're expliciting writing out each digit [Meta Character](#2-meta-characters), **`\d`**.
- We can also look for 9 digits like this `\d{3}-\d{3}-\d{4}`
  - Here, we're defining the digit [meta character](#2-meta-characters) **`\d`**, and then stating we want a quantity of three with the **`{n}`** [Quantifier](#quantifiers).


### Example - Email Address

Now that we've covered the basics, let's look at the regex search pattern for
all email addresses, again.
> *The goal here is to understand the concept of what's possible!*

**Do you see a pattern in this regex search pattern?**

`([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})`

> Let's break it apart into smaller chunks based on the high-level patterns we see.

| Symbol | Description |
|--------|-------------|
|**`(`** | Encapsulating a sub-expression |
|**`[a-z0-9_\.-]`** | Any alpha-numeric characters along with `_`, `.`, and `-`. Results must |
|**`+)`** | Ending sub-exepression, and reuqiring it be followed by the next argument. |
|**`@`**    | MUST include the `@` character. |
|**`([\da-z\.-]+)`** | Any digit or alpha-number character, followed by a `.` or `-`. |
|**`([a-z\.]{2,6})`** | Look for alpha-characters of any combonation between 2-6 characters in length |

---

### Regex Components


### Anchors


### Quantifiers


### OR Operator


### Character Classes


### Flags


### Grouping and Capturing


### Bracket Expressions


### Greedy and Lazy Match


### Boundaries


### Back-references


### Look-ahead and Look-behind




<!--
![GitHub commit activity](https://img.shields.io/github/commit-activity/w/erikplachta/cs-regex-reference-guide)
![GitHub commit activity](https://img.shields.io/github/commit-activity/m/erikplachta/cs-regex-reference-guide)
![GitHub commit activity](https://img.shields.io/github/commit-activity/y/erikplachta/cs-regex-reference-guide)
-->
## Author

**[Erik Plachta](https://github.com/ErikPlachta)**

## Contact Me

**Do you want to get in touch?**
> Feel free to connect with me on my [Twitter @ErikPlachta](https://www.twitter.com/erikplachta/) or [LinkedIn @ErikPlachta](https://www.linkedin.com/in/erikplachta/)

---

## Resources and References

A collection of resources I used to learn about Regex.

- [Wikipedia - Regular Expressions](https://en.wikipedia.org/wiki/Regular_expression)
- [MDN - Regular Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)
- [Microsoft - Regular Expression Language - Quick Reference](https://docs.microsoft.com/en-us/dotnet/standard/base-types/regular-expression-language-quick-reference)
- [MDN - Regular expression syntax cheatsheet](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Cheatsheet)
- [Regular-Exprsesions.info](https://www.regular-expressions.info/)
- [RexEgg.com](https://www.rexegg.com/)
- [Youtube - The Coding Train - Introduction to Regular Expressions - Programming with Text](https://www.youtube.com/watch?v=7DG3kCDx53c)
- [Regex tutorial — A quick cheatsheet by examples](https://medium.com/factory-mind/regex-tutorial-a-simple-cheatsheet-by-examples-649dc1c3f285)