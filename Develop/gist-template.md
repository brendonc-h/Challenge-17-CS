# Title (replace with your title)

For this week's challenge we're going to be explaing how a regex (regular expression) function works. I'm going to be explaing how a Hex Value function works. This is the function (/^#?([a-f0-9]{6}|[a-f0-9]{3})$/).

## Summary

Briefly summarize the regex you will be describing and what you will explain. Include a code snippet of the regex. Replace this text with your summary.



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
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

### Anchors
Anchor: ^
The Code Snippet: `/^#`

Description:
Anchors don't match any regular expression. Rather they assert something about the string based on expressions/matching pattern next to the anchor.

Example: `^This` indicates that the string must begin with `This`

The ^ is an anchor that indicates that the beginning of the string must match the character #. # is used to distinguish a hexadecimal number from a decimal number. However, as we will see in the next anchor, # is optional.

Anchor: $

Code Snippet: `$/`

Description: Matches the end of the string. Similar to the ^ anchor, $ is used to check if a string fully matches a pattern. However, $ asserts the pattern to theend of the string, not the beginning.

Example: `end$` indicates that the string must end with `end`.

In our case end of string must match with the 3 or 6 character pattern identified before the $ anchor. The 3 or 6 character patter is described in more detail under Qualifiers.

### Quantifiers

Qualifiers: ?

Code Snippet: `/^#?`

Description: 
? implies a boolean value, 0 or 1. Typically this makes the preceding symbol/character optional.

Example: 
This could be used to distinguish between British and American spelling in a string e.g. colour vs color -- the regex would colou?r.

In our regex, the quantifier ? indicates that the character # preceding the quantifier ? is optional. It's optional for # to appear at the beginning of the expression. 

Quantifier: {}

Code Snippet: `[a-f0-9]{6}`
Code Snippet: `[a-f0-9]{3}`

Description:
Quantifier indicates how many time the preceding pattern matches. Normally, the quantifiers are greedy, causing the regex to match as many occurences of a particular pattern as possible. However, if ? was appended, the quantifier would become lazy-- causing the regex to match as few occurences as possible. In our case, the quantifier is greedy.

Example: `2{5}` indicates that 2 must be repeated 5 times. Matching string must be 22222.

In our regex, {6} indicates that there are 6 instances of the string in the preceding bracket expression. That implies that this quantifier will allow exactly 6 characters in the string containing characters between a-f and/or integer between 0-9.

{3} indicates that there are 3 instances of the string in the preceding bracket expression. That implies that this quantifier will allow exactly 3 characters in the string containing characters betweem a-f and/or integer between 0-9.




### OR Operator
OR Operator: |

Code Snipet: `[a-f0-9]{6}|[a-f0-9]{3}`

Description: The | indicator (i.e. OR indicator) is a boolean that matches either the expression before or after.

Example: 3|5 indicates that either 3 or 5 or both integers are allowed in the string. 353 or 333 or 555 are all acceptable matching patterns. 

In our case, that implies match with 3 character string containing lower case a-f and/or integer 0-9 OR a string with 6 characters containing lowercase a-f and/or integer between 0-9. A matching string has to have 3 or 6 character with the specified pattern. Anything other than 3 or 6 characters will not match. 


### Character Classes
Code Snipet: `a-f0-9`
Description: Character classes only matches one out of several characters defined in the character set. A hyphen can be used inside a character class to define a range of characters More than one range can be used -- as is the case in our code snipet. 

Example: `[0-9]` This character class matches a single digit between 0 and 9

In our case, the character class consists of lower case a-f and/or integer 0-9 

### Flags

### Grouping and Capturing
Grouping and Capturing: ()

Code Snipet: `([a-f0-9]{6}|[a-f0-9]{3})`

Description: The () groups the regular expression between them. The grouping treats multiple characters as a single unit. 
This can proof useful when extracting information using any programming language. This group of data will be exposed in the form of an array. Values can be accessed using an index on the result of the match. 

Example: (dog){3} matched dogdogdog. The unit of characters 'dog' would need to repeat 3 times indicated in the quantifier. 

In our case, the grouped expression is a bracket expression whose details are provided in the section below. Ultimately the end string anchor $ is applied to this grouping. 

### Bracket Expressions
Bracket Expression: []

Code Snipet: `[a-f0-9]`

Description: Bracket expression is a regex that will match  a specific pattern of characters (alphabetic, numeric, special characters, symbols etc..) defined within the brackets. Typically a hyphen is used to describe a set or range of characters e.g. `[a-z]`. It's possible to use the ^ metacharacter to negate what is in between the brackets. 

Example: `[a-d 1-3]` indicates that the string must include atleast 1 character that is between a and d or 1-3

In our reg ex, the bracket [] expression indicates matching a string that has any lower case character between a-f or any integer between 0-9
### Greedy and Lazy Match
Code Snipet: `[a-f0-9]{6}`
Code Snipet: `[a-f0-9]{3}`

Quantifier: {}

Description: Greedy means match the longest possible string. Lazy means match the shortest possible string. 

Example:  `w.+l` matches `well` in `well` but the lazy `w.+?l` matches `wel`

As explained in the quantifier section, normal quantifiers are greedy, causing the regex to match as many occurrences of a particular pattern as possible. However, if ? was appended, the quantifier would become lazy-- causing the regex to match as few occurrences as possible. In our case, the quantifier is greedy.

### Boundaries

### Back-references

### Conclusion
Conclusion
When combined we're given the following Regex:

/^#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$/ : Starts the string.
/^#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$/ : Allows the string to start with or without a #.
/^#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$/ : Groups the bulk of the regex to define what can/will be matched.
/^#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$/ : Limits the characters available for the hex value to a-f, A-F, and 0-9.
/^#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$/ : Determines the groupings length will be 6 or 3 characters long.
/^#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$/ : Signifies that the grouping will provide either the results from the left OR right side.
/^#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$/ : Ends the string.
The final result matches with any valid standard hex value or hex triplet with/without a prefixed hashtag: #ffffff, AbC123, #GZ9, etc.

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)

My name is Brendon Curry-Hobbs. To contact me my GitHub profile is https://github.com/brendonc-h. 