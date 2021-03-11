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

re.search('(\w+)\s+\1', 'abc   abc')

Output: None

2. Use re.IGNORECASE Flag When Necessary
3. The “flags” is kind of unique in Python Regex which not all the other programming languages would have. That is, create regex patterns that are case-insensitive.
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

Input: re.search(r'[a-z]+', 'AbCdEfG', re.IGNORECASE)
Output: <re.Match object; span=(0, 7), match='AbCdEfG'>

Input: re.search(r'[a-z]+', 'AbCdEfG', re.I)
Output: <re.Match object; span=(0, 7), match='AbCdEfG'>

