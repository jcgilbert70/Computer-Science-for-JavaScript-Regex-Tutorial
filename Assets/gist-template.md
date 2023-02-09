# Regex Tutorial for Matching a URL

This gist will explain hor a regular expression for matching a URL using JavaScript functions. It explains how each part of the URL is expressed.

## Summary

This tutorial describes the regex characters that define each specific part of a URL seach: 

`/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

These characters are used in a as a pattern called "matacharacters", which uses a more general pattern. Regex is used to verify whether or not the input is a valid URL. Regex has a wide variety of applications, from finding patterns within a string, or replacing characters within that string.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)

## Regex Components

Components of a regex matching a URL:

* Anchors: `^ $`
* Quantifiers: `* + ? {}`
* Character classes: `\d \w .`
* Grouping and capturing: `()`
* Bracket expressions: `[]`
* Greedy match: `*`

### Anchors

In regular expressions, "anchors" are special symbols that match the position within a string, rather than matching a specific character or sequence of characters. The two most commonly used anchors in URL matching are the "start of line" (^) and "end of line" ($) anchors.

The `^` anchor matches the position at the very start of the string, ensuring that the regular expression will only match strings that start with the specified pattern.

The `$` anchor matches the position at the end of the string, ensuring that the regular expression will only match strings that end with the specified pattern.

Here is a simple example that uses the `^` and `$` anchors to match a URL that starts with "http://" and ends with ".com":
`^http:\/\/.*\.com$`

Explanation:

* `^` - Matches the start of the string.
http:\/\/ - Matches the "http://" scheme part of the URL.
* `.*` - Matches any sequence of characters (including zero characters) that occur between the scheme and TLD.
* `\.com` - Matches the ".com" TLD part of the URL.
* `$` - Matches the end of the string.

This pattern is a simplified example and will not match most URLs. It's just to illustrate the use of the ^ and $ anchors. For a more complete pattern to match URLs, see the previous answer.

### Quantifiers

A URL (Uniform Resource Locator) typically consists of several components including the scheme (e.g., "http"), host (e.g., "www.example.com"), path (e.g., "/path/to/resource"), and query string (e.g., "?query=string").

Here is a regular expression pattern that can be used to match most URLs: 
`^(?:https?:\/\/)?(?:[\w-]+\.)+(?:[a-zA-Z]{2,63})(?:\/[\w.-]*)*(?:\?[\w=&]+)*$`

Explanation:

* `^` - Matches the start of the string.
* `(?:https?:\/\/)?` - Matches the scheme part of the URL. The ? quantifier makes the scheme part optional, so URLs with or without "http://" or "https://" can be matched.
* `(?:[\w-]+\.)+` - Matches the host part of the URL. The + quantifier matches one or more repetitions of a group consisting of word characters (letters, digits, or underscores), hyphens, and a period.
* `(?:[a-zA-Z]{2,63})` - Matches the top-level domain (TLD) part of the host. The {2,63} quantifier specifies the minimum and maximum length of the TLD, which must be between 2 and 63 characters.
* `(?:\/[\w.-]*)*` - Matches the path part of the URL. The * quantifier matches zero or more repetitions of a group consisting of a slash, word characters, periods, or hyphens.
* `(?:\?[\w=&]+)*$` - Matches the query string part of the URL. The * quantifier matches zero or more repetitions of a group consisting of a question mark, word characters, equal signs, or ampersands.
* `$` - Matches the end of the string.

This pattern is intended as a starting point and may need to be modified or extended based on the specific requirements of your use case. URLs can vary greatly in their structure, and this pattern may not match all valid URLs.

### Grouping Constructs

In regular expressions, "grouping constructs" allow you to group multiple parts of a pattern together and refer to the entire group as a single unit. This can be useful for extracting specific parts of a URL or for creating complex patterns that match specific structures.

Here is an example that uses grouping constructs to match a URL and extract its different components:
`^(https?://)?([\w-]+\.)+([a-zA-Z]{2,63})(/[\w.-]*)*(\?[\w=&]+)*$`

Explanation:

* `^` - Matches the start of the string.
* `(https?://)?` - Matches the scheme part of the URL and groups it as a single unit. The ? quantifier makes the scheme part optional, so URLs with or without "http://" or "https://" can be matched.
* `([\w-]+\.)+` - Matches the host part of the URL and groups each repetition of the host as a single unit. The + quantifier matches one or more repetitions of a group consisting of word characters (letters, digits, or underscores), hyphens, and a period.
* `([a-zA-Z]{2,63})` - Matches the top-level domain (TLD) part of the host and groups it as a single unit. The {2,63} quantifier specifies the minimum and maximum length of the TLD, which must be between 2 and 63 characters.
* `(/[\w.-]*)*` - Matches the path part of the URL and groups each repetition of the path as a single unit. The * quantifier matches zero or more repetitions of a group consisting of a slash, word characters, periods, or hyphens.
* `(\?[\w=&]+)*$` - Matches the query string part of the URL and groups each repetition of the query string as a single unit. The * quantifier matches zero or more repetitions of a group consisting of a question mark, word characters, equal signs, or ampersands.
* `$` - Matches the end of the string.

Using grouping constructs, you can then extract the individual components of the URL

### Bracket Expressions

In regular expressions, "bracket expressions" are a type of character class that allow you to match any character that is contained within a set of characters specified in square brackets. Bracket expressions are commonly used to match URLs.

Here is an example that uses bracket expressions to match a URL:
`^https?://[\w.-]+\.[a-zA-Z]{2,63}(/[\w.-]+)*(\?[\w=&]+)*$`

Explanation:

* `^` - Matches the start of the string.
* `https?://` - Matches the scheme part of the URL. The ? quantifier makes the "s" in "https" optional, so URLs with either "http://" or "https://" can be matched.
* `[\w.-]+` - Matches the host part of the URL and groups each repetition of the host as a single unit. The bracket expression matches any combination of word characters (letters, digits, or underscores), hyphens, and periods. The + quantifier matches one or more repetitions of the bracket expression.
* `\.[a-zA-Z]{2,63}` - Matches the top-level domain (TLD) part of the host and groups it as a single unit. The bracket expression matches any combination of letters from the alphabet with a minimum length of 2 and a maximum length of 63 characters. The period is escaped to match the literal period character.
* `(/[\w.-]+)*` - Matches the path part of the URL and groups each repetition of the path as a single unit. The bracket expression matches any combination of word characters, hyphens, and periods. The * quantifier matches zero or more repetitions of the bracket expression.
* `(\?[\w=&]+)*$` - Matches the query string part of the URL and groups each repetition of the query string as a single unit. The bracket expression matches any combination of word characters, equal signs, or ampersands. The * quantifier matches zero or more repetitions of the bracket expression.
* `$` - Matches the end of the string.

This pattern should match most common URL structures.

### Character Classes

In regular expressions, "character classes" are a way to match any one character out of a set of characters. Character classes are specified within square brackets `[]`.

Here's an example of how character classes can be used to match a URL:
`^https?://[\w.-]+\.[a-zA-Z]{2,63}(/[\w.-]+)*(\?[\w=&]+)*$`

Explanation:

* `[\w.-]+` - Matches one or more repetitions of word characters (letters, digits, or underscores), hyphens, or periods.
* `[a-zA-Z]{2,63}` - Matches a sequence of 2 to 63 alphabetical characters.
In this example, the character classes are used to match the different parts of a URL, such as the host and top-level domain, and to ensure that they conform to certain requirements, such as the length of the top-level domain and the characters it can contain.

Character classes are just one of many features of regular expressions, and there are many other features, such as quantifiers, grouping constructs, and anchors, that can be combined to match complex patterns like URLs.

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)

Created by Jeff Gilbert

Any questions or comments please go to my [GitHub profile](https://github.com/jcgilbert70) or reach out via email at jcgilbert70@gmail.com.

