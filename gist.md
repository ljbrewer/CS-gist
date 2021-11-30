## What Is a Regex?

Regex is short for Regular Expression.  This is a way to search for patterns within a string. When included in code or search algorithms, regular expressions can be used to find certain patterns of characters within a string, or to find and replace a character or sequence of characters within a string. They are also frequently used to validate input. 

For example, the following regular expression can be used to verify that user input is a valid email address:

    `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

Each component of this regex has a unique responsibility to make sure that a user enters an email address that begins with an unspecified number of characters preceding the `@` symbol, followed by a domain.


## Table of Contents

- [Regex Components](#regex-components)
- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

A regex is considered a literal, so the pattern must be wrapped in slash characters (/). As an example let's use “Matching a Email Address” regex:

    `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

### Anchors

The characters ^ and $ are both considered to be anchors.

`/^beginning to ending$/`

The ^ anchor signifies a string that begins with the characters that follow it. 

Regex is case-sensitive so it must be an exact string match, such as ^The, where the strings "The" or "The person" match, but lower case "the" and "the person" do not. 

The $ anchor signifies a string that ends with the characters that precede it. It can be preceded by an exact string or a range of possible matches.

So, in an example of “Matching an Email Address” regex, the string has multiple sections that have different criteria.

    `/^  ([a-z0-9_\.-]+)  @ ([\da-z\.-]+)  \. ([a-z\.]{2,6})$/`

The first section ([a-z0-9_\.-]+), in the brackets it  can have any lowercase letters between a to z, can have any numbers between 0 to 9,  an underscore,  period and hyphen or any combination of these.  The plus sign means any other characters before the “@” symbol.

After the “@” symbol comes the next section ([\da-z\.-]+), in the brackets it can have any digit, lowercase letters a to z, can have a period, can have a hyphen, any other characters.  The “\.” is a period after this section.

The last section ([a-z\.] has any letters from a to z followed by a period

 You'll notice that we didn't include the pattern {2,6}, which precedes the $ character. Why? Because this is a special component called a quantifier.

### Quantifiers

All right, so now we know what we're looking for inside the brackets. Now what about sequence of characters that appeared before the $ anchor ({2,6}).

Quantifiers set the limits of the string that your regex matches (or a specific section of the string). They frequently include the minimum and maximum number of characters that your regex is looking for.

Quantifiers match as many occurrences of particular patterns as possible. They include the following:

    * — Matches the pattern zero or more times

    + — Matches the pattern one or more times

    ? — Matches the pattern zero or one time

    {} — Curly brackets can provide three different ways to set limits for a match:

    { n } — Matches the pattern exactly n number of times

    { n, } — Matches the pattern at least n number of times

    { n, x } — Matches the pattern from a minimum of n number of times to a maximum of x number of times

Each of these quantifiers can be made lazy by adding the ? symbol after it, meaning it will match as few occurrences as possible.

Now let’s look at how quantifiers are used in the “Matching an Email Address” regex. We have the quantifier {2,6}. This means that we want to find the preceding string pattern a minimum of 2 times and a maximum of 6 times. This quantifier means that this string has to be between 2 and 6 characters.

This regex is looking for any string between 2 and 6 characters that starts and ends with a combination of lowercase characters.

## Grouping

Anything inside a set of square brackets ([]) represents a range of characters that we want to match. These patterns are known as bracket expressions, but they are also known as a positive character group, because they outline the characters we want to include. We can write these expressions to include all of the characters we want to match. For example, [abc] will look for a string that includes a or b or c, regardless of the length of the string. So, all of the following examples would match: "aaa", "bin" "court", "abracadabra", and "bca".

You'll more commonly see a hyphen (-) used between alphanumeric characters (letters and numbers only) to represent a range of those possible characters. 

It's important to note that a bracket expression can be turned into a negative character group(i.e. exclude the characters in this string) by adding the ^ symbol to the beginning of the expression inside the brackets. A common example is matching a string that doesn't include any vowels. The pattern [^aeiouAEIOU] would find any strings that don't include lowercase or uppercase vowels.ng Constructs

#### Character Classes

A character class in a regex defines a set of characters, any one of which can occur in an input string to fulfill a match. The bracket expressions outlined previously, including positive and negative character groups, are considered character classes.

Here are some of the other common character classes:

    . — Matches any character except the newline character (\n)

    \d — Matches any Arabic numeral digit. This class is equivalent to the bracket expression [0-9].

    \w — Matches any alphanumeric character from the basic Latin alphabet, including the underscore (_). This class is equivalent to the bracket expression [A-Za-z0-9_].

    \s — Matches a single whitespace character, including tabs and line breaks

Each of the last three-character classes can be changed to perform an inverse match (or negative match) by capitalizing the letter character. For example, \D matches a non-digit character.

### The OR Operator

Remember that a bracket expression does not require the string to meet all of the requirements in the pattern. This means that [a-z0-9_-] searches for alphanumeric characters or the two special characters included in the pattern. Often, you'll want to add this same logic outside of a bracket expression, especially within a grouping construct or between two different grouping constructs.

Using the OR operator (|), the expression [abc] could be written as (a|b|c). Using our example in the grouping constructs section, we can take the original expression:

    (abc):(xyz)
And then use the OR operator to convert it to the following:

    (a|b|c):(x|y|z)
Now, both of the strings "abc:xyz" and "acb:xyz" would match, as well as "a:z", but "xyz:abc" would not.

## Character Escapes

The backslash (\) in a regex “escapes” a character that otherwise would be interpreted literally. For example, the open curly brace ({) is used to begin a quantifier, but adding a backslash before the open curly brace (\{) means that the regex should look for the open curly brace character instead of beginning to define a quantifier. This is common when looking for strings with special characters that are the same as a particular component of a regex.

It's important to note that all special characters, including the backslash (\), lose their special significance inside bracket expressions.

## Flags

Regex must be wrapped in slash characters. The one exception to this rule is with the component known as flags. Flags are placed at the end of a regex, after the second slash, and they define additional functionality or limits for the regex. There are six optional flags that can be used, either separately or together and in any order, but these are the three you're most likely to encounter:

    g — Global search: the regex should be tested against all possible matches in a string.

    i — Case-insensitive search: case should be ignored while attempting a match in a string

    m — Multi-line search: a multi-line input string should be treated as multiple lines

## Let's test our understanding

Explain the following regular expression and how it is used to verify that user input is a valid email address:

    `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

The string starts with an opening /, so this is where the regex begins. The caret "^" indicates the string is beginning. The first set of parentheses are the first section of the expression and it can contain any lower-case letter or numbers between 0-9 or an underscore, period, or hyphen, and any additional characters. To the first section we are adding the "@" literally to the string.  Then we come to the next section with the next set of parentheses that start after the @ symbol. This section can contain any numeral from 0 to 9 and any lowercase letters a to z, it can have a period or hyphen and any number of characters.  It is followed by a “.”, then we have the last section starting with the last set of parentheses. This last section can have only lower-case letters in it.  Then we have section surrounded with the braces ({}).  This tells us that the last section can must have a minimum of 2 letters and can have up to a maximum of 6 characters.  The $ indicates we are at the end of the string.   


## Author

I am new developer taking a boot camp. I have been coding for 5 months and can't wait to learn more! Please visit my GitHub to see what I've been working on!  https://github.com/ljbrewer
Thank you for reading my first gist. 
