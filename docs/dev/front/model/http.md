---
title: http
id: http
---
Http requests are handled through axios. They return Promises and can therefore be awaited.

    import http from ‘axios’;

    class MyClass {
        data;
        async sync(){
            const response = await http.get(‘/my/path’);
            this.data = response.data;
        }
    }

Http errors can be caught through try/catch :

    try {
        const response = await http.get(‘/my/path’);
        this.data = response.data;
    }
    catch(e){
        notify.error(e.response.data.error);
    }

The catch here is the equivalent to a .catch on a Promise. The .then is inside the try.

You can of course also await custom Promises:

    myFunction(): Promise<MyClass> {
        return new Promise((resolve, reject) => {
            otherFunction((data) => {
                resolve(new MyClass(data));
            });
        });
    }

    async function load(){
        const myObj = await myFunction();
    }
