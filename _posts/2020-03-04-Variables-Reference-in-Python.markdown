---
layout: post
title:  "Variable Reference in Python"
date:   2020-03-04 13:30:00 +0800
categories: howto
---

# Pass by reference

When a variable is given a value. The object will be initialized, and variable is a reference to the object managed in the memory. Return variable will trigger the garbabe collector to destry the object.

```
list_a = ['apple','google','facebook']
list_b = list_a
del list_b[0]
print(list_b)   # ['google','facebook']
print(list_a)   # ['google','facebook']

a = {}
b = {}
a['apple'] = b
print(a)    # {'apple': {}}
b['banana'] = {}
print(a)    # {'apple': {'banana': {}}}

c = {}
d = c
d = d.setdefault('apple',{})
print(d) # {}
print(c) # {'apple': {}}

e = c
e = e['apple']
e['banana'] = {}
print(c) # {'apple': {'banana': {}}}

```