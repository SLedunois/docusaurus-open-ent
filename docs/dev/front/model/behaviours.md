---
title: behaviours
id: behaviours
---
In ODE Framework, any application can communicate with all others.
This is done through the behaviours file, which is the exposed API of the application.
Typically, these are the options used in ODE Framework :

-   **[Rights](rights.adoc)** : all applications have to expose their rights system,
    to make sure other applications can display information properly

-   **[Resources](resources.adoc)** : it can be useful to list existing resources,
    so they can be linked or listed from another application

-   **[Sniplets](sniplets.adoc)**: applications may have sniplets.
    A sniplet is an exportable applicative snippet of code that can be embedded in another application.

-   **[Extensions](extensions.adoc)** : applications can also add any method they think can be useful.
    For instance, the workspace has a method allowing you to save data in a new file;
    if, say, your application is a reading list, allowing the user to save portions of text
    to read later, it makes sense to have a “addToReadingList” method.


