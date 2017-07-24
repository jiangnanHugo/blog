---
layout: "post"
title: "Unpacking Argument Lists"
date: "2017-07-24 21:55"
comments: True
---

## Lists
```python
param=[x,y,z]
model.train(*param)
```

## Dict
````python
param={'x':xx,
      'y':yy,
      'z':zz
}
model.train(**param)
```
