---
title: Locating elements.
date: 2026-01-07 23:47:20 +0530
categories: [Programming]
tags: [programming]
---

### Locating Elements

In the last post we discussed about loading locators dynamically. The next portion is to locate the elements when the user types `container.page_name.element_name`. In order to locate the elements,
we will be adopting an approach using the `__getattr__(...)` of Python.

#### __getattr__

Before we go ahead with the implementation of the `__getattr__` of Python, we need to understand the working of this magic function.

> Yes, I know these are called magic "methods". However, to me, one who comes from C and C++, these are just functions. There are no methods for me.
{: .prompt-info }

In Python, we have two magic functions which might be of interest when we are retrieving attributes(some call it properties as well) of an object. One of the functions is the
`__getattr__` and the other is the `__getattribute__` magic function. When we create an instance of a call, or as we call an object, Python basically calls `getattr(instance, attribute_name)`.
Internally when the attribute value is being retrieved using `getattr(...)` as well, internally the `__getattr__` is called if the attribute is not present. `__getattribute__` magic function
is always called, irrespective of whether the attribute is present or not present.

The loading of the elements are done in the following manner:
```python
...
for section in parser.sections():
  ...
  for option, value in parser.items(section):
    setattr(tmp, option, value)
...
```
