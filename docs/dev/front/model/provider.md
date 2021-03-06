---
title: provider
id: provider
---
The provider is an utility that requests the server on a given path only once, stores the collection, and casts it as a given class.

    import { Provider } from ‘entcore-toolkit’;

    const provider = new Provider<MyClass>('/path', MyClass);

    // All items are provided as instances of MyClass
    let data = await provider.data();
    setTimeout(() => {
        // Whether the first request is over or still loading, the provider
        // will return its content here too and only request the server once.
        let otherData = await provider.data();
    }, 50);

You can unsync the provider if you need to refresh data:

    provider.isSynced = false;
    const newData = await provider.data();

You can also add and remove elements manually if you want to avoid sending a new request:

    provider.push(myNewItem);
    provider.remove(myItem);
