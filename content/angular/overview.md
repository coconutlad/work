---
title: 'Overview'
weight: 1
---

# An overview (and miscellaneous stuff)
Angular is a platform, [apparently](https://angular.io/guide/what-is-angular), that includes a framework, some libraries, and developer tools to work with all of that. For most purposes, it's called a front-end web development framework.

## Typescript
Angular uses TS. It's a superset of JS that compiles to JS. You can adding typing via syntactic sugar which helps catch bugs when you compile. It also has editor plugins for the same. You can try it out [online](https://www.typescriptlang.org/play). Its main features are:
### Static typing
You can declare types while declaring variables, like so: `let var: number;`.
### Interfaces
They let you define a structure that objects must follow. An interface is a type. When you assign an object to a variable of that type, the object must have the properties in that interface (each of the same type). Like so
```ts
interface nice {
    name: string,
    age: number
}

let sic: nice;
sic = {
    name: "hai", // adding, removing, or changing the types of these properties causes an error
    age: 10
};
```
### Class properties
ES6 classes mainly define their properties via their constructors. TS lets you to define these properties in the class itself. You can optionally specify types for them. This is only for readability. E.g.
```ts
class Hip {
    num: number
    wutdis
    constructor() {
        this.num = 10;
        this.wutdis = "hmm";
    }
}
```
### Public / Private access
All class properties in ES6 are public. You can make them private in TS by adding the `private` before them during declaration. It also provides this nifty shorthand for the constructor:
```ts
class Hip {
    constructor(public wutdis: string, private num) {
        // it implicitly does this.wutdis = wutdis
    }
}
let f = new Hip("sic", 10);
console.log(f); // { wutdis: "sic", num: 10 }
```


## The bootstrap process
* The first file that is run is `main.ts` (as defined in `angular.json`  **That's a very useful file**). 
* It bootstraps a module, `app/module.ts` by default.
* It bootstraps the root component, `app/app.component.ts` by default.
* The root component is placed in `app/index.html` which is what is rendered.

## Modules and libraries
* Only the root NgModule should have a bootstrap property in its decorator.
The bootstrap property sets the root component for the app.
* Libraries are plain JS modules which can have angular modules.
* A component / directive / pipe can be declared in only one `NgModule`
* To use stuff that other module provide, you import that **`NgModule`** in this `NgModule`
* When you list services in the providers array, they are available app wide.
* It's possible to have multiple entry point components in the `bootstrap` array.

## File structure of workspace

## Deployment 🎈
This is done with the `ng build` command which:
* Minifies code (removes whitespaces and renames variables)
* Bundling (merges many JS file into a single JS file) so fewer requests are made
* Tree shaking (the production app doesn't have code that is never used). It's a *little* different from dead code elimination.

Angular has an Ahead Of Time (AOT) compiler that converts the HTML of templates into JS code that manupilates the DOM. 
It can help catch template errors, reduce the output size, and make rendering on the browser faster.

By default, running `ng build` will generate a "development" build which can still be deployed but isn't as optimized as it could be.
To run it in "production" mode use `ng build --prod` which reduces the number of requests and file sizes.

Deployment just involves copying the directory within "dist" to the web server!