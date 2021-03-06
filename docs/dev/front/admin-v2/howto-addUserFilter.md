---
title: howto-addUserFilter
id: howto-addUserFilter
---
This document describes the procedure to follow to add a filter to the user list in admin v2 app.

# Procedure

## Step 1: Add filter to User filter service

In user list filters service (**entcore/admin/src/main/ts/services/userlist.filters.service.ts**), add a class that extends UserFilter, example:

    class SourcesFilter extends UserFilter<string> {
        type = 'source'
        label = 'sources.multi.combo.title'
        comboModel = []
        order = '+'
        filterProp = 'this'

        filter = (source: string) => {
            let outputModel = this.outputModel
            return outputModel.length === 0 || outputModel.indexOf(source) >= 0
        }
    }

where :

-   **type**: UserModel attribute corresponding to the filter

-   **label**: label (i18n key in fr.json)

-   **comboModel**: values array

-   **order**: order attribute (prefix with "+" or "-" following the order you want)

-   **display**: object attribute to display

-   **filter**: filter function, return true to keep current item in the list

Then, add a private field for the new created filter and add it to filters array, example:

    private sourcesFilter = new SourcesFilter(this.updateSubject)

    filters : UserFilterList<any> = [
        ...
        this.sourcesFilter
    ]

Finally, add a setter to set filter comboModel (combo values), example:

    setSources(sources: Array<string>) {
        this.sourcesFilter.comboModel = sources
    }

## Step 2: Initialize filter model in User root component

Initialize filter model, by calling previously declared filter setter in function **initFilters(structure)** in file **entcore/admin/src/main/ts/modules/users/components/users-root/users-root.component.ts**, example:

    private initFilters(structure) {
        ...
        this.filtersService.setSources(structure.sources)
    }
