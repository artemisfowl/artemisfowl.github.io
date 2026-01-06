---
title: Agnostic Approach of Locators
date: 2026-01-05 21:11:34 +0530
categories: [Programming]
tags: [programming]
---

### Solution to rapid changes

Yesterday, I ranted about a scenario where the locators of a Web Application changes from one build to the other. This is a scenario which I have seen in too many workplaces. The solution provided by
the _Architects_ in this case has always been a bit on the orthodox. I have seen only the usual way and the over-engineered way.

However, if we as engineers look at the problem statement and think about a solution, there is one solution which I think many would agree on. Create a file which could be referred to at runtime and
used in order to generate the classes and load the locators. I am not sure about other programming languages(it should be possible to do so though), but with Python we can come up with a solution as
follows.

#### The schema

First of all we need to design the schema of the file which will be containing all the locator data. As already detailed in the earlier post, we need to make sure that the locating strategy and the
locator string is included in the file. This means that there has to be a way to specify the locator strategy, the locator string in such a way that none of the locator strings which could be used to
identify elements are being hampered.

There is also another portion, the number of elements to be fetched also needs to be specified. This is something that I learned from the `Selenium Page Factory` module for Python. The module is good
in its approach of locating the element the moment the dot operator is used. So, for example, if the user types `somepage.someelement.click()`, `somepage.someelement` will already locate the element
and then return a `Selenium WebElement` reference on which the user would be able to chain the next operation.

**The problem with `Selenium Page Factory` module** is that it does not consider this fact that the locator string might require updates and forces the user to update the element locator strings in
the `locators` dictionary. There is also this part where the module only considers each locator string to fetch only a single element. However, there are cases where the user would like to locate
multiple elements using a single locator string.

It is at this juncture that we need to engineer our own solution. We will be using some of the concepts of this same `selenium_page_factory` Python module, however, we will be engineering our own
solution. Our approach would be to contain the locating strategy, the locator string and the specification as to whether the locator string would be fetching a single element or multiple elements.
We also need to keep in mind the user experience, if we use JSON, the following could be considered as a structure:

```json
{
	"LoginPage": {
		"username": {
				"by": "CSS",
				"locator": "input[data-test='username-input']",
				"multiple": false
		},
			"password": {
				"by": "CSS",
				"locator": "input[data-test='password-input']",
				"multiple": false
			},
			"login_button": {
				"by": "CSS",
				"locator": "input[data-test='submit-button']",
				"multiple": false
			}
	}
}
```

There is a fundamental problem with this approach. The indentation, despite trying to help the user to read and understand it, causes confusion when more members are to be added. There are also other
files which could be leveraged as well, for example TOML, YAML, XML and the like. All of these files suffer from the same basic problem, they have a cognitive complexity to themselves.

[!NOTE] Python also uses spaces in order to separate code blocks, however the interpreter actually catches the issues when the program is being run. One could argue that `json` and similar python
modules already report issues in case the file is not having proper format, however, the cognitive complexity is not taken into account for files like YAML and TOML.

If some argue that we should be using YAML file, since it is a _"standard"_, we would be looking at something as follows:

```yaml
LoginPage:
  username:
    by: CSS
    locator: input[data-test='username-input']
    multiple: false
  password:
    by: CSS
    locator: input[data-test='password-input']
    multiple: false
  login_button:
    by: CSS
    locator: input[data-test='submit-button']
    multiple: false

```

Just take a look at the YAML format above. If someone would have to add on top of the existing data, if they are editing with an editor which does not have autoindentation present, they might be
adding it in another layer of increased and decreased indentation.
