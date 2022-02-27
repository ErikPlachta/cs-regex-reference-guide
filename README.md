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
    - [2. Meta characters](#2-meta-characters)
    - [3. Quantifiers](#3-quantifiers)
    - [4. Positions](#4-positions)
    - [Let's Look at a Basic Example - Phone Number](#lets-look-at-a-basic-example---phone-number)
    - [Let's Look at A More Complex Example - Email Address](#lets-look-at-a-more-complex-example---email-address)
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

### 2. Meta characters

Regex operator that represent specific data-types within the ASCI or Unicode
character sets.

| Syntax | Description  | Note | Example |
|--------|--------------|------|---------|
| **`\`** | Converts ASCI or Unicode character into meta-characters | | |
| **`/^`**| TODO: 02/27/2022 #EP |  | |
| **`.`** | Any ASCI or Unicode Character.| *Warning: Use with caution. It's a broad grab.* | |
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

| Syntax | Description  |
|--------|--------------|
| **`*`**|  0 or more   |
| **`+`**|  1 or more   |
| **`?`**|  0 or 1      |
| **`{min,max}`**|Range |
| **`{n}`**| ? |

---

### 4. Positions

... are

---

### Let's Look at a Basic Example - Phone Number

`\d\d\d-\d\d\d-\d\d\d\d`


### Let's Look at A More Complex Example - Email Address

Now that we've covered the basics, let's look at the regex search pattern for
all email addresses, again.
> *The goal here is to understand the concept of what's possible!*

`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

**Do you see a pattern in this regex search pattern?**

Let's break it apart into smaller chunks based on the high-level patterns we see.
I'll explain what is happening for context.
> Don't forget this is just to understand the concept!

**Regex and Email Addresses: `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`**

1. **`/^`** are two [meta characters](#2-meta-characters) strating the regular expression.
2. **`(`** is another [meta character](#2-meta-characters) defining the start of a regex-search-pattern.
3. **`[a-z0-9_\.-]`** is a our first mix of [literal](#1-literal-characters) and [meta](#2-meta-characters) characters!
    - `[]` are the [meta character](#2-meta-characters) that encapsulate the search/filter paramters.
    - `a-z0-9_\.-` are the [literal](#1-literal-characters), which is telling the regex-expression to search for ALL *alpha-number* *characters* including the asci-characters **underscore**, **period**, and **hyphen** too.
      > What about the backslash **`\`**?
      >> The [meta character](#2-meta-characters) **`\`** is escapging the [meta character](#2-meta-characters) operator **`.`**, converting it to a [literal character](#1-literal-characters).
4. **`+)`** are two more [meta character](#2-meta-characters) operators.  
    - **`+`** is indicating to add the next [literal character(s)](#1-literal-characters) to the former as part of the filter.
    - **`)`** is ending a regex-search-pattern block.
5. **`@`** is a [literal character](#1-literal-characters) that is 
6. **`([\da-z\.-]+)`** mirrors what is happening in #3 above.
7. **`\.`**
8. **`([a-z\.]{2,6})`**
9. *`$/`*



##

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