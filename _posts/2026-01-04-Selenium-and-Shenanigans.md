---
title: Selenium and Shenanigans
date: 2026-01-04 15:35:11 +0530
categories: [Rant]
tags: [rant, development]
---

### Automation

_Automation describes a wide range of technologies that reduce human intervention in processes, mainly by predetermining decision criteria, subprocess relationships and related actions, as well as
embodying those predeterminations in machines._

The aforementioned definition could be picked up from Wikipedia, this is literally the first line of the entire Wikipedia article on automation. In my opinion, it is all about minimizing human
involvement, if possible entire human intervention. With that being said, given the large scale of software(s) being written now-a-days, automation has become a part and parcel of the entire software
use life cycle.
If there is a software being used for certain tasks, then an automation is required so that proper manpower could be deployed in other areas that really require manual intervention. In this backdrop,
the number of Web Based Applications or simply called WebApps has become heavily prevalent. Corporates as well as other software builders want to leverage automation in building software faster(using
AI), test software with least manual intervention(using various technologies) and want to resolve issues if any, by providing automation to such an extent that the only thing required from the user
would be an approval. For Web Application automation as well, people are leveraging a library called Selenium - in the areas of automating workflows as well as for testing the web applications.

It is in this backdrop, that I found some very peculiar cases in which the module , despite being stable, is unable to keep the automations run smoothly. However, before detailing on the scenarios
where this module fails, I think I should be giving out some more information on the Module itself.

### Selenium

If we refer to the information available from Wikipedia, the following could be found:

_Selenium is an open source umbrella project for a range of tools and libraries aimed at supporting browser automation._

I have used Selenium as an extension in Firefox browser initially and then used it with Python Programming language. In my experience with Selenium, I have mostly worked with Python and Selenium for
automating workflows or testing functionalities of Web Applications. The library is exceptionally stable unless the only 2 scenarios which break the automations exist. Selenium with Python (as well
as Java, based on the examples that I have seen on the web) uses 2 inputs, one is the locator string which it would be using in order to parse the DOM and then locate the element of choice, the other
is the locating strategy. The locating strategy is primarily based on locating elements using CSS, ID, class or some other attribute. There are certain techniques which could be leveraged to even
locate elements based on the text content present.

For some reason though, I have always found CSS to be verbose enough for locating elements. There are a lot of techniques already present for locating elements using CSS selectors. The main reason I
like the CSS way of locating elements is because, one can test if the locator is proper using the `document.querySelector(...)` approach or check for multiple elements using the
`document.querySelectorAll(...)` approach. If the locator string is proper, the element would be located right away, in case it is not, there would be nothing found.

More information on CSS selectors could be found [here](https://scrapfly.io/blog/posts/css-selector-cheatsheet).

### Scenarios

The 2 scenarios where I have seen the Selenium powered automations failing are as follows:

- **The first scenario is that of the locators changing continuously**

- **The system has a workflow change.**

In the first scenario, the issue is for the element locators, a string which is used by Selenium in order to locate an element.

If the web application workflow being automated is getting updated continuously, then the locators are susceptible to changes which can lead to automated workflows failing over builds.
It can also lead to failure while performing critical testing, if Selenium is being used for testing as well.
There is a workaround to this, wherein the locators are placed in a separate file and then the file is being read before trying to locate the element. There are a few ways in which one can read the
file and load the locator information. There is the usual way and then the engineers' way and this is what I am about to rant below.

#### Usual Way

The age old way, which I have seen people doing is to create classes. Some term it as Application Object Model, some as Factory Model, sometimes it is referred to as Factory Pattern. I think there
are a few more names in the market which are used to refer to the same approach. These terms are usually propagated by the _"Architect"_ community who have created jargon after jargon in order to
refer to the approach(In my opinion, it is just to-ma-to and to-may-to). In the usual way, a lot of wrappers are created, mostly involving classes. Some do it by creating pages, some create the page
instances inside an application class and then use the application class instance in the actual automation implementation. Invariably the locator strings are added to the Page classes, resulting in
extensive automation failures and code changes.
