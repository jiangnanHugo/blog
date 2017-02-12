---
layout: post
title: "Regular Expression in Python"
description: "daily post"
comments: true
keywords: "regrex,python"
---

# Regular Expression Patterns

Following lists the regular expression syntax that is available in Python.

| Pattern | Description                              |
| ------- | ---------------------------------------- |
| ^       | match beginning of the line.             |
| $       | match end of line.                       |
| .       | match any single character except '\n'.  |
| [...]   | match any single character in brackets.  |
| re*     | match 0 or more occurrences of preceding expression |
| re+     | match 1 or more occurrences of preceding expression |
| re?     | match 0 or 1 occurrence of preceding expression. |
| re{n}   | match exactly n number of occurrences of preceding expression. |
| \1...\9 | match n-th grouped sub-expression.       |
| (re)    | Groups regular expressions and remembers matched text. |

```python
# \<
ESCAPE_RE = r'\\(.)'

# *emphasis*
EMPHASIS_RE = r'(\*)([^\*]+)\2'

# **strong**
STRONG_RE = r'(\*{2}|_{2})(.+?)\2'

# ***strongem*** or ***em*strong**
EM_STRONG_RE = r'(\*|_)\2{2}(.+?)\2(.*?)\2{2}'

# ***strong**em*
STRONG_EM_RE = r'(\*|_)\2{2}(.+?)\2{2}(.*?)\2'

# _smart_emphasis_
SMART_EMPHASIS_RE = r'(?<!\w)(_)(?!_)(.+?)(?<!_)\2(?!\w)'

# _emphasis_
EMPHASIS_2_RE = r'(_)(.+?)\2'

# [text](url) or [text](<url>) or [text](url "title")
LINK_RE = NOIMG + BRK + \
    r'''\(\s*(<.*?>|((?:(?:\(.*?\))|[^\(\)]))*?)\s*((['"])(.*?)\12\s*)?\)'''

# ![alttxt](http://x.com/) or ![alttxt](<http://x.com/>)
IMAGE_LINK_RE = r'\!' + BRK + r'\s*\(\s*(<.*?>|([^"\)\s]+\s*"[^"]*"|[^\)\s]*))\s*\)'

# [Google][3]
REFERENCE_RE = NOIMG + BRK + r'\s?\[([^\]]*)\]'

# [Google]
SHORT_REF_RE = NOIMG + r'\[([^\]]+)\]'

```

$$f(x)=\sigmoid(Wx+b)$$
