---
title: "The DRY (Don't Repeat Yourself) Principle"
permalink: /2020/07/dry-dont-repeat-yourself.html
published: true
---

DRY stands for Don't Repeat Yourself, which basically means to avoid writing duplicate code. If you find a block of code that is repeated multiple places, consider using abstraction or moving the code to a separate method. Similarly, if you use a hard-coded value more than once, try making it a constant. This can be applied to every area of software development including database, unit tests, build systems, and documentation. 

The benefit of the DRY principle is code maintenance. Changing functionalities in the future will be much easier because you don't have to remember all the places where the code needs to be changed. 

An important point to remember here is to not abuse the principle. Duplication is not for code, but for functionality. It means you should never use a standard code for two functionalities that have similar code but are logically unrelated. Doing it will tightly couple two different functionalities together and changing one of them in the future will become harder.