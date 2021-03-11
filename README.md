# Python_Regex
Regular expression implementation using Python

Regular Expression (aka Regex) is one of the most important and common in any programming languages. Of course, this also applies to Python. Python has some quite unique regex usage patterns compared to other programming languages.This page gives a 7 useful tips regarding the regex in Python for you. They are either little tricks that can improve your productivity, solve some complex problems or improve your code readability. Hope they’ll be helpful!

1. Always use “r-string”

A lot of learners know that we should use “r-string” when we define a regex pattern. However, I found that many people don’t know the reason. Some learners think of the “r-string” as “regex string”, which is totally wrong. It should be “raw string” instead.
Just like other programming languages, Python has the “escape” mechanism in the strings. For example, when we want to have a string with quotes, they have to be escaped to let the compiler knows that the string should not finish, the quotes are just part of the string.

s = 'I\'m Smith'

Of course, not only the quotes can be escaped, there are a lot of other scenarios that we have to use backward slashes. For example, the \n in the following string will be interpreted as “new-line”.

print('Chris\nSmith')

Output:
Chris 
Smith

If we mean to have the \n as part of the string, in other words, it should not be a new-line, we can use the “r-string” to tell Python do not interpret it.

Input: print(r'Chris\nSmith')

Output: Chris\nSmith

When we write a regex pattern, sometimes we have to use slashes or other special characters. Therefore, to avoid that Python interpreter would interpret the string in the wrong way. It is always recommended to use “r-string” when defining a regex pattern.
Suppose we are searching for a pattern that several letters repeated after a few whitespaces, we can write the regex as follows.

re.search(r'(\w+)\s+\1', 'abc   abc')

output: <re.Match object; span=(0, 9), match='abc   abc'>

However, if we don’t use “r-string” here, the “group” indicator \1 won’t be recognised.

Example

Input: re.search('(\w+)\s+\1', 'abc   abc')

Output: None

2. Use re.IGNORECASE Flag When Necessary

The “flags” is kind of unique in Python Regex which not all the other programming languages would have. That is, create regex patterns that are case-insensitive.
Suppose we want to match a series of letters regardless of upper cases or lower cases. Of course, we can write it as follows.

re.search(r'[a-zA-Z]+', 'AbCdEfG')

This is definitely the standard way, and if we don’t add A-Z, it won’t match the whole string as expected.

Input : re.search(r'[a-zA-Z]+', 'AbCdEfG')
Output: <re.Match object; span=(0, 7), match='AbCdEfG'>

Input : re.search(r'[a-z]+', 'AbCdEfG')
Output: <re.Match object; span=(1, 2), match='b'>

However, Python provides such a way that we can focus more on the pattern itself and don’t need to worry about the cases of the letters. That is to use the re.IGNORECASE. You can even make it very short as re.I which does the same thing.

re.search(r'[a-z]+', 'AbCdEfG', re.IGNORECASE)
re.search(r'[a-z]+', 'AbCdEfG', re.I)

Example

Input: re.search(r'[a-z]+', 'AbCdEfG', re.IGNORECASE)
Output: <re.Match object; span=(0, 7), match='AbCdEfG'>

Input: re.search(r'[a-z]+', 'AbCdEfG', re.I)
Output: <re.Match object; span=(0, 7), match='AbCdEfG'>

3. Use re.VERBOSE Flag to Improve the Readability

One of the major drawbacks of the regex is that it has poor readability. Usually, this is the comprising that we have to face. However, do you know that Python has a better way to improve the readability of a regex pattern string? That is to use the re.VERBOSE flag.
We can re-write the regex pattern in section 1. Originally, the pattern string has to be r'(\w+)\s+\1'. Well, this is not too bad, but suppose if we have a much more complex pattern, probably only the author can understand it. This is a very common issue with regex. However, with the verbose flag, we can write it this way.

re.search(r'''
    (\w+)   # Group 1: Match one or more letters, numbers or underscore
    \s+     # Match one or more whitespaces
    \1      # Match the Group 1 whatever it is
''', 'abc   abc', re.VERBOSE)

Example

Input: re.search(r'''
    (\w+)   # Group 1: Match one or more letters, numbers or underscore
    \s+     # Match one or more whitespaces
    \1      # Match the Group 1 whatever it is
''', 'abc   abc', re.VERBOSE)
Output: <re.Match object; span=(0, 9), match='abc   abc'>

It is exactly equivalent to the r'(\w+)\s+\1'. Please be noticed that the flag re.VERBOSE is a must-have thing if we want to write it in this way. Otherwise, the regex won’t work, of course.

Again, the flag has a short version — re.X

Example

Input: re.search(r'''
    (\w+)   # Group 1: Match one or more letters, numbers or underscore
    \s+     # Match one or more whitespaces
    \1      # Match the Group 1 whatever it is
''', 'abc   abc', re.X)
Output: <re.Match object; span=(0, 9), match='abc   abc'>

4. Customise Substitution Behaviour of re.sub()

re.sub() is one of the most commonly used functions in Python regex. It tries to find a pattern (pattern)in a string (string) and replace it with the provided replacement string (repl).
For example, the following code will hide any mobile numbers in a string.
re.sub(r'\d', '*', 'User\'s mobile number is 1234567890')

Example

Input: re.sub(r'\d', '*', 'User\'s mobile number is 1234567890')
Output: "User's mobile number is **********"

Most developers will know the function up to here. However, fewer will know that we can actually use a function for the repl parameter.For example, we still want to hide the user’s phone number, but we want to reveal the last 3 digits to make sure that the user has a clue what’s that number.

Example

Input: re.sub(r'\d+', lambda s: '*' * (len(s[0])-3) + s[0][-3:], 'User\'s mobile number is 1234567890')
Output: "User's mobile number is *******890"



