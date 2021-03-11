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
