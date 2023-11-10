# Regex notes

Hello, My name is CJ Cabrera, in this notesheet I will describe a few regex expressions.

## Summary

I'll be presenting a regular expression (regex) pattern designed to validate email addresses. This regex ensures that an email adheres to a conventional structure, encompassing a username, the "@" symbol, and a domain name. I'll break down the individual components of the regex and share a straightforward Python code snippet illustrating how to apply this regex for validation.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

### Anchors
What is a regex anchor?
In regular expressions, anchors are used to specify the position of a match within a string. The `^` symbol, for example, anchors the regex at the start of the string, while the `$` symbol anchors it at the end. There are other anchors like the word boundary anchor which is 
```
Consider the regex ^abc:

Input: "abcxyz"
Matches: "abc"
The ^ anchor asserts that the regex pattern must appear at the start of the string. It matches "abc" at the beginning of "abcxyz."
Now, consider the regex xyz$:

Input: "abcxyz"
Matches: "xyz"
The $ anchor asserts that the regex pattern must appear at the end of the string. It matches "xyz" at the end of "abcxyz."
Next, consider the regex hello\b:

Input: "hello world"
Matches: "hello"
The \b anchor asserts a word boundary. It matches "hello" because it is followed by a space, indicating the end of the word.
Finally, consider the regex asdfg\B:

Input: "asdfgh"
Matches: "asdfg"
The \B anchor asserts a non-word boundary. It matches "asdfg" because it is not followed by a word boundary, and "h" is part of the word.
```
### Quantifiers
Quantifiers control the number of occurrences of a character or group in a regex. Common quantifiers include `*` (zero or more), `+` (one or more), and `?` (zero or one).
```
Example: `*` (Zero or More)

Consider the regex `a*`:

- Input: "aaab"
- Matches: "aaa" (three 'a' characters)
- Explanation: The `*` quantifier allows for zero or more occurrences of the preceding character, 'a' in this case. So, it matches any sequence of 'a' characters, including an empty string.

- Input: "b"
- Matches: "" (empty string)
- The `*` quantifier allows for zero occurrences, so it matches an empty string when there are no 'a' characters.
Additional:
     Specific Quantity x ({x})
        a{3} only matches specifically to the number of occurances.



    x or More ({x,})
        a{5,} will match all occurrences of variable "a" greater than or equal to 5. The test will fail for anything less than 5 occurrences.



    Between x and y ({x,y})
        a{2,6} will match between 2 and 6 occurrences of variable a
```
### Grouping Constructs
Grouping constructs, denoted by parentheses `()`, allow you to treat multiple characters as a single unit. This is useful for applying quantifiers to a specific part of the regex.
```
Consider the regex `(ab)+`:

- Input: "ababab"
- Matches: "ababab"
- The `(ab)` in parentheses is a capturing group. The `+` quantifier outside the parentheses applies to the entire group, allowing it to match one or more occurrences of the entire "ab" sequence.

Now, consider the regex `(\d{3})-(\d{2})`:

- Input: "123-45"
- Matches: "123-45"
- Here, we have two capturing groups `(\d{3})` and `(\d{2})`. This regex matches a three-digit number, followed by a hyphen, and then a two-digit number.

```
### Bracket Expressions
Bracket expressions, defined by square brackets `[]`, match any single character within the brackets.
```
Consider the regex `[aeiou]`:

- Input: "apple"
- Matches: "a" and "e"
- The bracket expression `[aeiou]` matches any single character within the brackets. It matches the vowels "a" and "e" in the word "apple."

Now, consider the regex `[0-9]`:

- Input: "Hello123"
- Matches: "1," "2," and "3"
- The bracket expression `[0-9]` matches any single digit. It matches the digits "1," "2," and "3" in the string "Hello123."

```
### Character Classes
Character classes provide a concise way to match sets of characters.
```
Consider the regex `\d{3}`:

- Input: "123abc"
- Matches: "123"
- The `\d` character class matches any digit (equivalent to `[0-9]`). In this example, `\d{3}` matches three consecutive digits, resulting in "123."

Now, consider the regex `\w+`:

- Input: "Hello_World"
- Matches: "Hello_World"
- The `\w` character class matches any word character (equivalent to `[a-zA-Z0-9_]`). The `+` quantifier allows it to match one or more word characters. In this case, it matches the entire "Hello_World" sequence.

```
### The OR Operator
he OR operator, represented by the | symbol, allows you to specify alternatives within a regex pattern. It matches either the expression preceding it or the expression following it.
```
Consider the regex `(red|blue|green)`:

- Input: "The sky is blue."
- Matches: "blue"
- The `(red|blue|green)` regex matches "blue" in the input string. It allows for the flexibility to match any of the specified alternatives separated by the OR operator.

Matching Programming Languages

Consider the regex `(Python|JavaScript|Java)`:

- Input: "I enjoy programming in Python."
- Matches: "Python"
- In this case, the regex `(Python|JavaScript|Java)` matches "Python" in the input string, demonstrating how the OR operator provides choices for matching different alternatives.

```
### Flags
Flags in regular expressions are optional parameters that modify the behavior of the regex pattern. They are usually appended to the end of the regex and are case-insensitive. Here are some common flags:
```
`i`- Case-Insensitive Matching
The `i` flag allows the regex to match characters regardless of their case. For example:
regex: /abc/i
Input: "ABC"
Matches: "ABC"
The i flag makes the regex case-insensitive, allowing it to match "ABC" despite the different case.

`g` - Global Matching
The g flag performs a global search, meaning it finds all matches in the input string rather than stopping after the first match. For example:
regex: /\d/g
- Input: "123a45"
- Matches: "1," "2," "3," "4," and "5"
- The regex `/d/g` searches globally for digit matches in the input string. It successfully matches all digits "1," "2," "3," "4," and "5." The global matching (`g` flag) ensures that all digit matches are found.
```
### Character Escapes
Character escapes in regular expressions allow you to match specific characters with special meanings. Here are some common character escapes:
```
`\d` - digit
The \d escape matches any digit (equivalent to [0-9]). For example:
regex: /\d{3}/
Input: "123abc"
Matches: "123"
The \d escape matches three consecutive digits in the input string.

`\w` - Word Character
The \w escape matches any word character, including letters, digits, and underscores (equivalent to [a-zA-Z0-9_]). For example:
regex:/\w+/
Input: "Hello_World123"
Matches: "Hello_World123"
The \w+ escape matches the entire sequence of word characters in the input string.
```
## Author

This is a note sheet made by myself on common regular expressions. t's an extremely useful tool to strengthen your knowledge in regex! Check it out at my github:https://github.com/CjCabrera1/regexGist
