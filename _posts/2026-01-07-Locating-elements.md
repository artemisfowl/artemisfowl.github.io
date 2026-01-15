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

Since `__getattr__` is called when the attribute is not present in the instance, we will be using the same in order to locate the element. The following could be considered as a
simple implementation.
```python
class Page:
  ...
  def __getattr__(self, attribute_name: str):
    ...
```

In this function, we will be adding the capacity to resolve the element based on the format of the INI file. In the INI file, the locators would be present as follows:
```ini
...
[Login]
username = CSS | input[data-test="username"] | false
password = CSS | input[data-test="password"] | false
login_button = CSS | button[data-test="login"] | false

[Profile]
...
```

In order to locate the element, the user would be writing something like `Login.username.type("john_doe")`. We will concentrate on the `Login.username...` portion only, we will get
back to the `...type("john_doe")` in the next post. In order to locate the element and return the same using the `.`, the definition of the `__getattr__(...)` to check the value of the
option and then return a Selenium Web Element.


The implementation would be changed to something as follows:
```python
def __getattr__(self, name):
  value = self.__dict__.get(name)
  if not value:
    raise AttributeError("Invalid attribute name specified")

  strategy, locator, is_multiple = (i.strip() for i in value.split("|"))
  ...
```
The `is_multiple` could be converted into boolean using a simple logic as follows:
```python
...
from ast import literal_eval
...
is_multiple = literal_eval(is_multiple.capitalize())
...
```
Once this is done, the next step is to locate the element using `By.<strategy>` resolution.
