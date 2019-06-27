---
title: index
id: index
---
# Getting started

If you’ve used [skeletons](https://github.com/entcore/skeletons) to initialize your application, you already have a gulpfile,
a webpack config file, and a npm package file. To start front-end development,
you first need to install nodeJS 6.11.

<https://nodejs.org/en/>

Then, you can go in your application folder and install all dependencies:

`npm install`

You will also need to make the gulp command available:

`npm install -g gulp@3.9.1`

# Gulp commands

Two gulp commands are available in your application:

`` gulp `build` ``

will start building your typescript files, bundle them in a single file,
and add cache-busting utilities.

> **Warning**
>
> You need to use gulp build before gradle install,
> as Gradle (the server-side build tool) will use your current resources directory.

The second one is

`gulp watch`

This will start a process listening to all changes made to your files, build them and copy them to your springboard directory. You can set your springboard path with the springboard parameter:

`gulp watch --springboard /path/to/my/springboard`

This also works with relative paths:

`gulp watch --springboard ../my/springboard`

# Covered topics

-   [Using AngularJs](angularjs/index.adoc)

    -   [Translations](angularjs/translations.adoc)

    -   [Templates](angularjs/templates.adoc)

    -   [Notifications](angularjs/notifications.adoc)

    -   [Routing](angularjs/routing.adoc)

    -   [UI Module](angularjs/ui-module.adoc)

-   [Making your model](model/index.adoc)

    -   [HTTP](model/http.adoc)

    -   [Mix](model/mix.adoc)

    -   [Selection](model/selection.adoc)

    -   [Eventer](model/eventer.adoc)

    -   [Provider](model/provider.adoc)

    -   [Autosave](model/autosave.adoc)

    -   [Behaviours](model/behaviours.adoc)

    -   [Rights](model/rights.adoc)

    -   [Resources (in Behaviours)](model/resources.adoc)

    -   [Sniplets](model/sniplets.adoc)

    -   [Extensions (in Behaviours)](model/extensions.adoc)

    -   [Preferences](model/preferences.adoc)

    -   [Workspace](model/workspace.adoc)

    -   [Addind others NPM modules](model/use-npm-modules.adoc)


