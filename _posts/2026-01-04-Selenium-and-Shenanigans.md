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
automating workflows or testing functionalities of Web Applications. The library is exceptionally stable unless the only 2 scenarios which break the automations exist.

### Scenarios

The 2 scenarios where I have seen the Selenium powered automations failing are as follows:

-
