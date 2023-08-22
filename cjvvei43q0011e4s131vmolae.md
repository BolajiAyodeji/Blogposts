---
title: "The Differences Between Object.freeze() vs Const in JavaScript"
datePublished: Fri Apr 26 2019 23:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cjvvei43q0011e4s131vmolae
slug: the-differences-between-objectfreeze-vs-const-in-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1558298320519/PuO47ZWcA.png
tags: programming, javascript, es6, tech

---

ES6 has brought several new features and methods into JavaScript since its release. These features have better improved our workflow and productivity as JavaScript developers. Amongst these new features are `Object.freeze()` method and `const`.

It is argued among a few developers especially newbies that these two feature works the same way, but they actually don’t. `Object.freeze()` and `const` work differently, and I'll show you how in this article.

## Overview

`const` and `Object.freeze()` are totally different.

-   **const** behaves like `let`. The only difference is, it defines a variable that cannot be reassigned. Variables declared by `const` are block-scoped and not function scoped like variables declared with `var`.
-   **Object.freeze()** takes an object as an argument and returns the same object as an immutable object. This implies that **no properties of the object can be added, removed, or changed.**

> **Mutable objects** have properties that can be changed. Immutable **objects** have no properties that can be changed after the **object** is created.

## Demystifying Const


```js
const user = 'Bolaji Ayodeji'
```

```js
user = 'Joe Nash'
```

This would throw an `Uncaught TypeError` because we are trying to reassign the variable **user**, which was declared with the `const` keyword. This is not valid!

![](https://cdn-images-1.medium.com/max/1600/1*fkm8tv7a1jdhQSWa1Hl5tg.png)

Originally, this would work with `var` or `let` but will not with `const`.

### The problem with const

When working with Objects, using const only prevents reassignment and not immutability (the ability to prevent changes to the state and properties of an object after it's created).

Consider the code below. We have declared a variable using the `const` keyword and assigned an object named `user` to it.

```js
const user = {
  first_name: "bolaji",
  last_name: "ayodeji",
  email: "hi@bolajiayodeji.com",
  net_worth: 2000,
};
```

```js
user.last_name = 'Samson';
// this would work, user is mutable!
```

```js
user.net_worth = 983265975975950;
// this would work too, user is mutable and getting rich :)!
```

```js
console.log(user);  
// user is mutated
```

![](https://cdn-images-1.medium.com/max/1600/1*fXjTs7lGxDXd3bFv2rF1Vg.png)

Although we can’t reassign this variable called object, we can still mutate the object itself.

```js
const user = {  
user_name: 'bolajiayodeji'
}
// won't work
```

![](https://cdn-images-1.medium.com/max/1600/1*hxSHWKuB8nopFHif_ETW9g.png)

We definitely would want to have objects with properties that cannot be modified or deleted after creation. `const` cannot do this, and this is where `Object.freeze()` saves the day :).

## Demystifying Object.freeze()

To disable any changes to the object, we need `Object.freeze()`.

```js
const user = {
  first_name: "bolaji",
  last_name: "ayodeji",
  email: "hi@bolajiayodeji.com",
  net_worth: 2000,
};
```

```js
Object.freeze(user);
```

```js
user.last_name = 'Samson';
// this won't work, user is immutable!
```

```js
user.net_worth = 983265975975950;
// this won't work too, user is still immutable and broke :(!
```

```js
console.log(user);  
// user is immutable
```

![](https://cdn-images-1.medium.com/max/1600/1*uiv64RdHsencUe9ZKptrbw.png)

### The problem with Object.freeze()

`Object.freeze()` is a bit shallow. An object with nested properties is not actually frozen when `Object.freeze()` is applied.  You will need to apply `Object.freeze()` on nested objects to protect them recursively.

```js
const user = {  
first_name: 'bolaji',  
last_name: 'ayodeji',  
  contact: {    
   email: 'hi@bolajiayodeji.com',   
   telephone: 08109445504,  
  }
}
```

```
Object.freeze(user);
```

```js
user.last_name = 'Samson';
// this won't work, user is still immutable!
```

```js
user.contact.telephone = 07054394926;
// this will work because the nested object is not frozen
```

```js
console.log(user);
```

![](https://cdn-images-1.medium.com/max/1600/1*xL0vmY5YC7n3hq5SfIT-Vg.png)

So `Object.freeze()` doesn't fully **freeze** an object when it has properties that are nested. To completely freeze objects and their nested properties, you can write your own library or use already created libraries like [Deepfreeze](https://github.com/substack/deep-freeze) or [immutable-js](https://github.com/immutable-js/immutable-js).

## Conclusion

I hope you've learned why `const` and `Object.freeze()` are not the same. `const` prevents reassignment and `Object.freeze()` prevents immutability.

Thanks for reading; cheers!