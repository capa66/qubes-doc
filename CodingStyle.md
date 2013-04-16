---
layout: wiki
title: CodingStyle
permalink: /wiki/CodingStyle/
---

Coding Guidelines for Qubes Developers
======================================

Rationale
---------

Maintaining proper coding style is very important for any larger software project, such as Qubes. Here's why:

-   It eases maintenance, such as adding new functionality or generalization later,
-   It allows others (as well as the original author after some time!) to easily understand fragments of code, what they were supposed to do, and so makes it easier to later extend them with newer functionality or bug fixes,
-   It allows others to easily review the code and catch various bugs,
-   It provides for an aesthetically pleasing experience when one reads the code...

Often, developers, usually smart developers, neglect the value of proper coding style, thinking that it's most important how their code works, and expecting that if it solves some problem using a nice and neat trick, then it's all that is really required. Such thinking shows, however, immaturity and is a signal that the developer, however bright and smart, might not be a good fit for any larger project. Writing a clever exploit, that is to be used at one Black Hat show is one thing, while writing a useful software that is to be used and maintained for years, is quite a different story. If you want to show off how smart programmer you are, then you should become a researcher and write exploits. If, on the other hand, you want to be part of a team that makes real, useful software, you should ensure your coding style is impeccable. We often, at Qubes project, often took shortcuts, and often wrote nasty code, and this always back fired at us, sometime months, sometime years later, the net result being we had to spend time fixing code, rather than implementing new functionality.

General typographic conventions
-------------------------------

-   **Use space-expanded tabs that equal 4 spaces.** Yes, we know, there are many arguments for using "real" tabs, instead of space-expanded tabs, but we need to pick one convention to make the project consistent. One argument for using space-expanded tabs is that this way the programmer is in control of how the code will look like, despite how other users have configured their editors to visualize the tabs (of course, we assume any sane person uses a fixed-width font for viewing the source code). Anyway, if this makes you feel better, assume this is just an arbitrary choice.

-   **Maintain max. line length of 80 characters**. Even though today's monitors often are very wide and it's often not a problem to have 120 characters displayed in an editor, still maintaining shorter line lengths improves readability. It also allows to have two parallel windows open, side by side, each with different parts of the source code.

-   Class, functions, variables, and arguments naming convention -- let's keep that simple: **`ClassName` -- for all class names,** `some_variable`, `some_function`, `some_argument` -- for everything else (including instances of classes, AKA objects).

-   Horizontal spacing -- maintain at least decent amount of horizontal spacing, such as e.g. add obligatory space after `if` or before `{` in C, and similar in other languages. Whether to also use spaces within expressions, such as (x\*2+5) vs. (x \* 2 + 5) is left to the developer's judgment.

-   **Use single new lines** ('\\n' aka LF) in any non-Windows source code. On Windows, exceptionally, use the CRLF line endings -- this will allow the source code to be easily view-able in various Windows-based programs.

-   **Use descriptive names for variables and functions**! Really, these days, when most editors have auto-completion feature, there is no excuse for using short variable names.

File naming conventions
-----------------------

TODO

General programming style guidelines
------------------------------------

-   Use comments to explain non-trivial code fragments, or expected behavior of more complex functions, if it is not clear from their name.
-   Do **not** use comments for code fragments where it is immediately clear what the code does. E.g. avoid constructs like this:

    ``` {.wiki}
    // Return window id
    int get_window_id (...) {
        (...)
        return id;
        }
    ```

-   Do **not** use comments to disable code fragments. In a production code there should really be no commented or disabled code fragments. If you really, really have a good reason to retain some fragment of unused code, use \#if or \#ifdef to disable it, e.g.:

\#if 0

> (...) *Some unused code here*

\#endif

... and preferably use some descriptive macro instead of just `0`, e.g.:

\#if USE\_OLD\_WINDOW\_TRAVERSING

> (...) *Some unused code here*

\#endif

Not sure how to do similar thing in Python... Anyone?

But generally, there is little excuse to keep old, unused code fragments in the code. One should really use the functionality provided by the source code management system, such as git, instead. E.g. create a special branch for storing the old, unused code -- this way you will always be able to merge this code into upstream in the future.

Source Code management (Git) guidelines
---------------------------------------

-   Use git to maintain all code for Qubes project.

-   Before you start using git, make sure you understand that git is a decentralized Source Code Management system, and that it doesn't behave like traditional, centralized source code management systems, such as SVN. Here's a good [​introductory book on git](http://git-scm.com/book). Read it.

-   Qubes code is divided into many git repositories. There are several reasons for that:

> **This creates natural boundaries between different code blocks, enforcing proper interfaces, and easing independent development to be conducted on various code parts at the same time, without the fear of running into conflicts.**

> **By maintaining relatively small git repositories, it is easy for new developers to understand the code and contribute new patches, without the need to understand all the other code.**

> **Code repositories represent also licensing boundaries. So, e.g. because `core-agent-linux` and `core-agent-windows` are maintained in two different repositories, it is possible to have the latter under a proprietary, non-GPL license, while keeping the former fully open source.**

> **We have drastically changes the layout and naming of the code repositories shortly after Qubes OS R2 Beta 2 release. For details on the current code layout, please read [​this article](http://theinvisiblethings.blogspot.com/2013/03/introducing-qubes-odyssey-framework.html).**

Security coding guidelines
--------------------------

-   As a general rule: **untrusted input** is our \#1 enemy!
-   Any input that comes from untrusted, or less trusted, or just differently-trusted, entity should always be considered as malicious and should always be sanitized and verified. So, if your software runs in Dom0 and processes some input from any of the VMs, this input should be considered to be malicious. Even if your software runs in a VM, and processes input from some other VM, you should also assume that the input is malicious and verify it.

To Be Continued.

Python-specific guidelines
--------------------------

TODO

C-specific guidelines
---------------------

TODO

C++-specific guideline
----------------------

TODO