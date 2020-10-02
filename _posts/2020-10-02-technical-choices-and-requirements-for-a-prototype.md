---
layout: post
title:  "Part 3: Technical choices and requirements for a prototype"
---

<!---
your comment goes here
and here
-->

### Introduction

In [my last article](../../../2020/09/25/some-mockups.html), I presented some mockups of a document editor that is meant to be intuitive and to enable the user to be more productive. Now I am going to explain the technical choices I made and the goal a prototype has to fulfil. 

### Technical choices

I am going to develop in C++, using Qt as a GUI (graphical user interface) Toolkit. ConTeXt will be used as a backend to translate the document into PDF.

#### Why ConTeXt?

Despite its old age, TeX remains one of the most famous typesetting systems available today. It is indeed a very sophisticated software that produces high-quality documents. Several extensions were made to TeX, to make it easier to write structured documents. The most famous one is LaTeX. So why not choose LaTeX? There are several reasons that pushed me to choose ConTeXt, another variant:

* I had a better experience with ConTeXt as with LaTeX, and I believe it to be better designed as LaTeX.
* While its numerous 3rd party modules makes LaTeX a very powerful software, the design choice to delegate to them basic functionalities that could have been in the core (e.g. setting document margin, setting spacing of headings), makes LaTeX a giant with feet of clay. These modules may conflict or become obsolete, which is certainly manageable for someone writing documents directly in LaTeX, but it's a different story for a document editor built on top of LaTeX that is supposed to provide the basic functionalities expected by the user while running without errors for all kind of documents, for all kind of users. ConTeXt, on the other hand, has much more functionalities in its core.
* ConTeXt is an extension of LuaTeX. That means that I can write extensions in Lua, which is much more convenient than to write them in plain TeX. That said, there is support for programming in Lua in LaTeX via 3rd party modules.

#### Why Qt?

I already used Qt a few times, although it has been for some basic user interfaces, and I found it pleasant to use. It's also a good choice for multiplatform applications, which is an important factor as I would like to target Windows, OS X and Linux. While C++ is the most natural choice when it comes to developing an application with Qt, it also supports numerous other programming languages such as Python, C#, Java, Go, Ada. Moreover it is also used for embedded devices, which is an asset for me, as I have a strong interest in hardware-oriented software development.

#### Why C++

Besides it's the most natural choice with Qt, it is also widely used for embedded systems. So, learning to master this language makes definitively sense for me.

I however have a preference for Ada. I really like the philosophy behind the language. As a developer spends much more time reading code than writing it, then readability should be optimized even when it means typing a few more characters. Besides that, Ada has an excellent type system which includes types attributes. That way, you can add additional specifications on how the compiler should implement your code, so that you only program as low level as needed, but not more that is really needed. I believe, Ada didn't get the success, that it deserved. Throughout the history, it wasn't always the most deserving technology that was the most successful, and it's certainly an interesting topic to dig into as I can see some life principles to be discovered there. However that would be beyond the scope of this article, so it would be for another article. That said, choosing a little-known language such as Ada for an application where it doesn't provide a substantial advantage doesn't sound a good option to me. However, the day I have the opportunity to design a safety-critical software, I would be happy to develop it in Ada, as it's type safety and the ability for the programmer to define specific requirements to be met by the compiler would be decisive there.

### Prototype

We can't really know the value of an idea before it has been implemented, and creating a prototype can help evaluating an idea before investing too much time on it. Moreover, as I lack experience on creating and leading a project, there are additional unknowns that I would like to clear before I decide whether I would go ahead and develop such a document editor. These unknowns can be seen as both a risk and an opportunity:

| Risk | Opportunity |
|---|---|
| I tend to be too detail oriented, so I could spent too much time searching how to do exactly what I want | By repeated practice, I learn to evaluate whether the resolution of an issue is an important milestone toward my vision or just a distraction to be let go (*) |
| Wrong choice for the backend, which causes too slow document generation, or errors happening randomly, or a lack of flexibility to do easy things easily | Backend will go unnotified for the average user, while the advanced user can do powerful things thanks to inserting backend code in his document |
| The user interface isn't as user-friendly as first thought, because important things where overlooked | The user interface ends up being a pleasure for the user to interact with, and it makes him more productive than ever |
| This project costs me more time that I am ready to give | I discover that I can run this project at the right pace, and that I will be OK to slow it down at necessarily times |

_(*) By the way, I discovered the Pomodoro technique. The breaks that this technique requires help me to step back and to reflect whether what I am doing at the moment is really adding enough value to my objectives compared to the efforts it requires._

This is how the prototype will look like once it's done:

* Multiple levels of sections (Chapter, section, sub-section, paragraph, ...)
* At least one of the following object can be inserted in a document without any backend code: images, tables, bullet or numbered lists
* Some, but not necessarily all, basic customizations are possible, like e.g. spacing between paragraphs
* Layouts can be inserted in the document, as needed by the CV example I gave in [my first article](../../../2020/09/16/time-for-a-new-document-editor.html).

### What comes next?

I will start coding the prototype and I will publish the code in [this repository](https://github.com/jonsba/joed/)
