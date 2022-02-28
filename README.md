# CS Regex Reference Guide for JavaScript

If you're a customer science engineer, in any language, learning how to use and understand Regex expressions is a must.

## Summary

This is a general reference guide on how to understand and use some basic Regex
Expressions. I've broken down specific functions below with basic examples and
real-life scenarios where the associted regex expression would be useful.

---

The content on this Gist was created on **[this GitHub Repo](https://github.com/ErikPlachta/cs-regex-reference-guide/)**, published to this **[GitHub Website](https://erikplachta.github.io/cs-regex-reference-guide/)**, and published on [this GitHub Gist](https://gist.github.com/ErikPlachta/250107ea2e00086af9c1d29082c502b1/).

---

---

## Repo Stats

[![GitHub license](https://img.shields.io/github/license/ErikPlachta/cs-regex-reference-guide)](https://github.com/ErikPlachta/cs-regex-reference-guide) [![GitHub Number of Languages](https://img.shields.io/github/languages/count/ErikPlachta/cs-regex-reference-guide)](https://github.com/ErikPlachta/cs-regex-reference-guide)
[![GitHub top Language](https://img.shields.io/github/languages/top/ErikPlachta/cs-regex-reference-guide)](https://github.com/ErikPlachta/cs-regex-reference-guide)
[![GitHub issues](https://img.shields.io/github/issues/ErikPlachta/cs-regex-reference-guide)](https://github.com/ErikPlachta/cs-regex-reference-guide/issues)
![GitHub last commit](https://img.shields.io/github/last-commit/erikplachta/cs-regex-reference-guide)

---

---

## Table of Contents

- [CS Regex Reference Guide for JavaScript](#cs-regex-reference-guide-for-javascript)
  - [Summary](#summary)
  - [Repo Stats](#repo-stats)
  - [Table of Contents](#table-of-contents)
  - [Regex - Regular Expressions](#regex---regular-expressions)
    - [What are some other ways to explain Regular Expressions?](#what-are-some-other-ways-to-explain-regular-expressions)
    - [Undersatnding Regex -> Regular Expressions Are ~~not~~ Easy to Understand](#undersatnding-regex---regular-expressions-are-not-easy-to-understand)
      - [Example - Phone Number](#example---phone-number)
      - [Example - Email Address](#example---email-address)
    - [1. Regex Components](#1-regex-components)
      - [1.1 Literal Characters](#11-literal-characters)
      - [1.2 Meta Characters](#12-meta-characters)
    - [2. Anchors](#2-anchors)
    - [3. Quantifiers](#3-quantifiers)
    - [4. OR Operator](#4-or-operator)
      - [4.1 Character Classes / Bracket Expressions](#41-character-classes--bracket-expressions)
      - [4.2 Alteration Classes / Grouping and Capturing](#42-alteration-classes--grouping-and-capturing)
      - [4. Positions](#4-positions)
    - [Boundaries](#boundaries)
    - [Flags](#flags)
    - [Grouping and Capturing](#grouping-and-capturing)
    - [Greedy and Lazy Match](#greedy-and-lazy-match)
    - [Back-references](#back-references)
    - [Look-ahead and Look-behind](#look-ahead-and-look-behind)
  - [Author](#author)
  - [Contact Me](#contact-me)
  - [Resources and References](#resources-and-references)

---

---

## Regex - Regular Expressions

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

---

### What are some other ways to explain Regular Expressions?

Great questions!

The [MDN team said,](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)
> "*Regular expressions are patterns used to match character combinations in strings.*"

[Wikipedia says,](https://en.wikipedia.org/wiki/Regular_expression)
> "*A regular expression is a sequence of characters that specifies a search pattern in text. Usually such patterns are used by string-searching algorithms for "find" or "find and replace" operations on strings, or for input validation.*"

---

---

### Undersatnding Regex -> Regular Expressions Are ~~not~~ Easy to Understand

To understand a regex pattern, *the search / filter you're creating*, you'll need
to learn some syntax. But first, let's start with some examples.

#### Example - Phone Number

Without the area-code, phone numbers are generally 9-digits separated by a space
or a hyphen.

---

**We can look for 9 digits like this `/\d\d\d-\d\d\d-\d\d\d\d/`**
Here's, we're using the [meta character](#2-meta-characters) arguement `\d` for 
each unique digit that we're searching for seperated by a hyphen.

BUT what IF the single phone-number is formatted differently through-out the data?
For Example, our regex expression ran on the below data would only retrun 1
results, `123-456-7890`, even though ALL of them are the same phone number.
> `(123)-456-7890`, `123-456-7890`, `123.456.7890`, and `123 456 7890`

---

**So how could we improve our regex expression?**

Well, considering the same phone numbers 4 times again, we want to account for
`(`,`)`, ` `, and `-`.
> `(123)-456-7890`, `123-456-7890`, `123.456.7890`, and `123 456 7890`

**1.** Add a FEW OR operators to account for spaces vs hyphens
    > To do this we'll use **`[]`**, the [character class syntax](#character-classes),
    > where each [literal character](#1-literal-characters) inside the square-
    > brackets is considered a unqiue argument.

**2.** Add the ability to match `(` and `)` if they exist.
    > For optional parameters, we'll use the **`?`** [quantifier](#quantifiers),
    > which allows us to search for intances where a value does and does not exist.

**What does this fully fleshed out syntactically accurate regex argument look like?**

`/(\(?)+(\d{3})+[-.) ]+(\s?)(\d{3})+[-. ]+(\s?)+(\d{4})/`

Let's break it down 👇🏼

| Syntax      | Description |
|-------------|-------------|
| **`/`** | Starting the regex expression |
| **`\(?`** | Left-parenthesis `(` if exists|
| **`+`** | Followed by... |
| **`\d{3}`** | A collection of 3 digits |
| **`+`** | Followed by... |
| **`[)-. ]`** | a right-parenthesis `)`, OR hyphen `-`, OR period `.`, OR a space` `|
| **`+`** | Followed by... |
| **`\s?`** | A white-space if it exists |
| **`[- ]`** | Hyphen OR a space|
| **`+`** | Followed by... |
| **`\d{3}`** | A collection of 3 digits |
| **`+`** | Followed by... |
| **`[-. ]`** | A hyphen, dash, or space |
| **`+`** | Followed by... |
| **`\s?`** | A white-space if it exists |
| **`+`** | Followed by... |
| **`\d{4}`** | A collection of 4 digits |
| **`/`** | Ending the regex expression |

#### Example - Email Address

Now that we've covered the basics, let's look at the regex search pattern for
all email addresses, again.
> *The goal here is to understand the concept of what's possible!*

**Do you see a pattern in this regex search pattern?**

`/([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})/`

Let's break it apart into smaller chunks based on the high-level patterns we see!

| Symbol | Description |
|--------|-------------|
| **`/`** | Starting the regex expression |
|**`(`** | Encapsulating a sub-expression |
|**`[a-z0-9_\.-]`** | Any alpha-numeric characters along with `_`, `.`, and `-`. Results must |
|**`+)`** | Ending sub-exepression, and reuqiring it be followed by the next argument. |
|**`@`**    | MUST include the `@` character. |
|**`([\da-z\.-]+)`** | Any digit or alpha-number character, followed by a `.` or `-`. |
|**`([a-z\.]{2,6})`** | Look for alpha-characters of any combonation between 2-6 characters in length |
| **`/`** | Ending the regex expression |

---

---

### 1. Regex Components

#### 1.1 Literal Characters

Any/all ASCII or unicode characters you're wanting to search for or filter out. 
This will include sincle characters

| Syntax | Description                |
|--------|----------------------------|
| **`a-z`** | Any lower-case letters  |
| **`A-Z`** | Any upper-case letters  |
| **`0-9`** | Any digits |
| **`\.`**  | A period character |
| **`Unicode Characters`**  | There's a lot. here's an index -> *[Microsoft - Insert ASCII or Unicode Latin-based symbols and characters](https://support.microsoft.com/en-gb/office/insert-ascii-or-unicode-latin-based-symbols-and-characters-d13f58d3-7bcb-44a7-a4d5-972ee12e50e0)* |

#### 1.2 Meta Characters

Regex operator that represent specific data-types within the ASCI or Unicode
character sets.

| Syntax | Description  | Note | Example |
|--------|--------------|------|---------|
| **`\`** | Converts ASCI or Unicode character **into meta-characters** | *WARNING: If you don't use this it will be considered a literal-character!* | |
| **`/^`**| Any new line | | |
| **`.`** | Any ASCI or Unicode Character.| *WARNING: Within a [character class](#character-classes), a `.` does not need to be escaped to be read as a [literal character](#1-literal-characters)* | |
| **`\d`**| Any Digit 0-9 | | |
| **`\w`**| Anything that is a word-character | *`A-Z`*, *`a-z`*, **`0-9`** |  **`\w\w`** -> Returns any sequent of two word-characters. |
| **`\W`**| Anything that is NOT a word-character |   |   |
| **`\s`**| Any white-space characters. | `Space`, `Tab`, and sometimes `new-line`| **`\s\s`** -> Returns any sequent of two white-space characters. |
| **`\S`**| Anything that is NOT white-space. | `Space`, `Tab`, and sometimes `new-line` | |
| **`[a-z]`**| All character a-z. | When in a class, the `-` plays as an operator to reutrn a-z character argument values. See the [character classes](#character-classes) section for more details | | `[a-c]` -> return all characters between `a` and `c` |

---

---

### 2. Anchors

| Syntax  | Description  |   Example   |
|---------|--------------|-------------|
| **`^`** | Used to look for a string value start | `^test` looks for all strings that start with the [literal characters](#1-literal-characters) `t`, `e`, `s`, and `t`. |
| **`$`** | Used to look for [literal characters](#1-literal-characters) that end with a specific value. | `/test$/` looks for all strings that end with the [literal characters](#1-literal-characters) `t`, `e`, `s`, and `t`. |

---

---

### 3. Quantifiers

... are a meta character that modify the pervious meta characters in a regular
expesion.
> Based on your regex search paramters, how many of times do you want it to
> match in a row?

| Syntax | Description  |   Example   |
|--------|--------------|-------------|
| **`*`**|  0 or more   | |
| **`+`**|  1 or more   | |
| **`?`**|  0 or 1      | **`/test?t/`** -> all combonations of `test` and `testt` where the second T is optional.       |

| **`{min,max}`**| Range of number of times former-arguement must exist to qualify as a result. | **`\w{1,5}`** -> All word-character combonations with 1-5 characters followed by white-space.|
| **`{n}`**| Number of times the former-arguement must exist to qualify as a result. | **`\w{5}\s`** -> All word-character combonations with 5 character followed by white-space.   |

---

---


### 4. OR Operator

How to use OR Arugments witin a regex statement.

#### 4.1 Character Classes / Bracket Expressions

... is one of the two **OR operators**, where arguments are placed inside of square-brackets **`[ ]`**.

| Snytax | Description | Notes | Example |
|--------|-------------|-------|---------|
| **`[^argument]`** | **NOT OR Operator**, returns anything except for the argument in the Class | A carrot, `^`, becomes a [meta character](#2-meta-characters) when used at the preface of a class. Anywhere else and it becomes a [literal character](#1-literal-characters) | `[^0-5]` -> anything not 0-5. `[^a-c]` -> Anything that is not between the letters a-c.
| **`[.]`** |  All literal character instances of a period, `.` | Within a class, does **not** need to be escaped to be read as a literl character. |`[-.]` -> looks for the literal characters `-` OR `.` |
| **`a[bc]de`** | All cases of `abde` AND/OR `acde`. |   |  |
| **`[letter-letter]`**   | Any literal characters a-z based on case sensitivy. | A hyphen, `-` becomes a [meta character](#2-meta-characters) when used between two literal characters of the same family within a class. | `[a-c]` -> return all characters between `a` and `c`. `/\b[A-Za-z]{4}\b/` -> to match any 4-letter word with letter [literal characters](#1-literal-characters) in it. `/\b[A-Z][a-z]*\b/` -> to match any 0-or more letter word with letter [literal characters](#1-literal-characters) in it starting with a capital letter. `\b[\w]{4}\b` -> All 4 letter words that contain any value used within words. |
| **`[number-number]`** | A range between two numbers | A hyphen, `-` becomes a [meta character](#2-meta-characters) when used between two literal characters of the same family within a class. | `[0-5]{3}` -> All combonations of 3-digits where each unique digit is between 0 - 5 |

---

#### 4.2 Alteration Classes / Grouping and Capturing

... is the second **OR Operator**, and is used with as an or operator to look
for grouped literal characters within parentheisis and separated by a vertical
bar `( arg1 | arg2 )`.

| Snytax | Description | Notes | Example |
|--------|-------------|-------|---------|
| **`(arg1\|arg2)`** | Return all instances where `arg1` or `arg2` exist. | This is how you search for very specific groups of literal characters. | `/[\w.]+@\w+\.+(com\|net\|edu)/` -> Returns all email address that end with .net, .com, or.edu |

#### 4. Positions

... are used to match the location of a litercal character within your defined
searach-paramters.

| Syntax  | Description  |   Example   |
|---------|--------------|-------------|
| **`^`** |  The beganning of line | **Lines with only 1 word:** -> **`^\w+$** -> Any new line followed by a word-character followed by end of line. |
| **`$`** |  The End of the line   |  |

### Boundaries

| Syntax  | Description  |   Example   |
|---------|--------------|-------------|
| **`\b`** |  A word boundry | **All 4 letter words** -> **`/\b\w{4}/`** -> Looking at each word, look ALL word-character values of length 4. `/\btest\b/` -> Returns a whole word waerch |

---

---

### Flags

... are used to classify speciic search-case scenarios to you regex expression.
They can be combined or used individually as needed, and are added to the end
of your regex expression. `/regex-pattern/flag`

| Syntax  | Description  |   Example   |
|---------|--------------|-------------|
| **`g`** | Globally searching. |`/[a-z]/g` -> returns all letters within all content. |
| **`i`** | Case-insenstivie searching | `/[a-z]/gi` -> returns ALL literal character despite case from A-Z and a-z |
| **`m`** | Multi-line searching. | `/^\d/gm` -> returns ALL initial digits within all lines 
| **`s`** | Dotall mode returns results with any [literal character](#11-literal-characters) between them. | |
| **`u`** | Enable unicode support | |
| **`y`** | Sticky mode allows you to search exact position within content | |

### Grouping and Capturing

### Greedy and Lazy Match

### Back-references

### Look-ahead and Look-behind

---

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