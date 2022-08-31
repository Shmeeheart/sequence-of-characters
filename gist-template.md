# Sequence-Of-Characters

A sequence of characters that defines a specific search pattern. This is what we are learning about today - regular expressions (a.k.a. regex). We will go through several different concepts to ensure one is confident in regular expressions in reference to matching email addresses. There are a wide range of possible combinations with emails. There is no such thing as a perfect regex to capture all leginate email addresses.

## Summary

We are going to learn how to identify the different components that make up a regex and explain what they do for matching an email. One thing to remember is that there are two basic reasons for validating email addresses; one is to improve usability and make sure users don't accidnelty leave off an important part of their email addresses. The second is to make sure that people are not entering dummy addresses.

`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

## Table of Contents

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

## Regex Components

/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/

### Anchors

In most regex flavors, the anchors < ^ > and < $ > force the regular expression to find its match at the start and the end of the subject text, respectively.

For instance:

/^([a-zA-Z0-9_.-]+)@([\da-zA-Z.-]+).([a-zA-Z.]{2,6})$/

The ^ signifies the regex will match with the code group in the first set of parantheses that the caret precedes meaning the information provided before the @ symbol appears in the rest of the code string preventing a user from simply submitting an '@(DOMAIN).com email address without the first required part of the email address, the NAME section.

The $ symbol signifies the string regex will match ends with the DOMAIN the dollar sign follows.

Examples:

Not matched: @gmail.com; there is no NAME.

Not matched: goodwije@gmail.c; the extension is less than two letters, the minimum required for the extension.

Matched: goodwije@email.co.us; this email address has a name, domain name, extnesion, and an acceptable country code extension.

### Quantifiers

Quantifiers match a number of instances of a character, group, or character class in a string.

If you want to avoid your system choking on arbitrarily large input, you can replace the infinite quanitifiers with finite ones.

^[A-Z0-9._%+-]{1,64}@(?:[A-Z0-9-]{1,63}\.){1,125}[A-Z]{2,63}$ takes into account that the local part (before the @) is limited to 64 characters and that each part of the domain name is limited to 63 characters

### OR Operator

-

### Character Classes

A character class allows you to match any symbol from a certain character set. A character class is also called a character set.

Suppose you have a phone number like this: +1-(888)-555-0000 and you want to turn it into a plain number: 188855500000.

Well - character classes with regex can help you do this! In this case, the digit character class can be used. This is denoted by \d which matches any single digit.

let phone = '+1-(888)-555-0000';

let re = /\d/;

The most commonly used character classes are:

- \d - match a single character from 0 to 9
- \s - match a single whitespace symbol such as space, a tab \t, a newline \n.
- \w - w stands for word character. It matches the ASCII character [A-Za-z0-9_] including Latin alphabets, digits, and the underscore\_

### Flags

Regular expressions may have flags that affect the search. There are only 6 of them in JavaScript. I could not find anything that was applicable exclusively to validate email addresses, but I have included the flags below:

i - with this flag the search is case-insensitive: no difference between A and a

g - with this flag the search looks for all matches, without it - only the first match is returned

m - multiline mode

s - enables 'dotall' mode, that allows a dot . to match newline character \n

u - enables full Unicode support. The flag enables correct processing of surrogate pairs.

y - "sticky" mode: searching at the exact positino in the text

### Grouping and Capturing

A part of a pattern can be enclosed in parantheses (...). This is called a "capturing group"

That has two effects:

1. It allows to get a part of the match as a separate item in the result array.
2. If we put a quantifier after the parentheses, it applies to the parentheses as a whole.

For example:

The email format is: name@domain. Any word can be the name, hyphens and dots are allowed. In regex that's [-.\w]+.

### Bracket Expressions

The part after the @ also has two alternatives. It can either be a fully qualified domain name (e.g. regular-expressions.info), or it can be a literal Internet address between square brackets. The literal Internet address can either be an IP address, or a domain-specific routing address.

The reason you shouldn’t use this regex is that it is overly broad. Your application may not be able to handle all email addresses this regex allows. Domain-specific routing addresses can contain non-printable ASCII control characters, which can cause trouble if your application needs to display addresses. Not all applications support the syntax for the local part using double quotes or square brackets. In fact, RFC 5322 itself marks the notation using square brackets as obsolete.

We get a more practical implementation of RFC 5322 if we omit IP addresses, domain-specific addresses, the syntax using double quotes and square brackets. It will still match 99.99% of all email addresses in actual use today.

### Greedy and Lazy Match

There wasn't any salient information for a greedy or lazy match for email addresses. However, for educational purposes I will add a few details.

Greedy search: to find a match, the regular expression engine uses the following algorithm:
-For every position in the string
-Try to match the pattern at that position
-If there's no match, go to the next position

Lazy mode: the lazy mode of quantifiers is an opposite to the greedy mode. It means: "repeat minimal number of times". We can enable it by putting a question mark '?' after the quantifier, so that it becomes \*? or +? or even ?? for '?'.

To make things clear: usually a question mark ? is a quantifier by itself (zero or one), but if added after another quantifier (or even itself) it gets another meaning – it switches the matching mode from greedy to lazy.

### Boundaries

If your regex is delimited with word boundaries, it becomes suitable for extracting email addresses from files or larger blocks of text. If you want to check whether the user typed in a valid email address, replace the word boundaries with start-of-string and end-of-string anchors, like this: ^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$.

You may need to change word boundaries into start/end-of-string anchors, or vice versa. And you have to turn on the case insensitive matching option.

### Back-references

Not really applicable for email matching. However, to provide some insight - we can use the contents of capturing groups (...) not only in the result or in the replacement string, but also in the patther itself.

## Author

Jennifer Goodwin is a current student for the University of Utah Continuing Education for a Coding Bootcamp for Full-Stack Web Development.

Name: Jennifer Goodwin (Shmeeheart)
Email: goodwije@gmail.com

Github Profile: https://github.com/Shmeeheart
