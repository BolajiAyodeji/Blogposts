## The differences between Object.freeze() vs Const in JavaScript

ES6 has brought several new features and methods into JavaScript since its release. These features have better improved our workflow and productivity as JavaScript developers. Amongst these new features are `Object.freeze()` method and `const`.

It is argued among a few developers especially newbies that these two feature works the same way, but they actually don’t. `Object.freeze()` and `const` work differently, and I'll show you how in this article.

## Overview

`const` and `Object.freeze()` are totally different.

-   **const** behaves like `let`. The only difference is, it defines a variable that cannot be reassigned. Variables declared by `const` are block-scoped and not function scoped like variables declared with `var`.
-   **Object.freeze()** takes an object as an argument and returns the same object as an immutable object. This implies that **no properties of the object can be added, removed, or changed.**

> **Mutable objects** have properties that can be changed. Immutable **objects** have no properties that can be changed after the **object** is created.

## Demystifying Const


```
const user = 'Bolaji Ayodeji'
```

```
user = 'Joe Nash'
```

This would throw an `Uncaught TypeError` because we are trying to reassign the variable **user**, which was declared with the `const` keyword. THIS IS NOT VALID.

![](https://cdn-images-1.medium.com/max/1600/1*fkm8tv7a1jdhQSWa1Hl5tg.png)

Originally, this would work with `var` or `let` but will not with `const`.

### The problem with const

When working with Objects, using const only prevents reassignment and not immutability (Ability to prevent changes to its properties).

Consider the code below. We have declared a variable using the `const` keyword and assigned an object named `user` to it.

```
const user = {
  first_name: "bolaji",
  last_name: "ayodeji",
  email: "hi@bolajiayodeji.com",
  net_worth: 2000,
};
```

```
user.last_name = 'Samson';
// this would work, user is still mutable!
```

```
user.net_worth = 983265975975950;
// this would work too, user is still mutable and getting rich :)!
```

```
console.log(user);  
// user is mutated
```

![](https://cdn-images-1.medium.com/max/1600/1*fXjTs7lGxDXd3bFv2rF1Vg.png)

Although we can’t reassign this variable called object, we can still mutate the object itself.

```
const user = {  
user_name: 'bolajiayodeji'
}
// won't work
```

![](https://cdn-images-1.medium.com/max/1600/1*hxSHWKuB8nopFHif_ETW9g.png)

We definitely would want to have Objects with properties that cannot be modified or deleted. `const` cannot do this, and this is where `Object.freeze()` saves the day :).

## Demystifying Object.freeze()

To disable any changes to the object, we need `Object.freeze()`.

```
const user = {
  first_name: "bolaji",
  last_name: "ayodeji",
  email: "hi@bolajiayodeji.com",
  net_worth: 2000,
};
```

```
Object.freeze(user);
```

```
user.last_name = 'Samson';
// this won't work, user is still immutable!
```

```
user.net_worth = 983265975975950;
// this won't work too, user is still immutable and still broke :(!
```

```
console.log(user);  
// user is immutated
```

![](https://cdn-images-1.medium.com/max/1600/1*uiv64RdHsencUe9ZKptrbw.png)

#### The problem with Object.freeze()

Objects with nested properties are not actually frozen. `Object.freeze()` is a bit shallow; you will need to apply it on nested objects to protect them recursively.

```
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

```
user.last_name = 'Samson';
// this won't work, user is still immutable!
```

```
user.contact.telephone = 07054394926;
// this will work because the nested object is not frozen
```

```
console.log(user);
```

![](https://cdn-images-1.medium.com/max/1600/1*xL0vmY5YC7n3hq5SfIT-Vg.png)

So `Object.freeze()` doesn't fully **freeze** an object when it has properties that are nested. To completely freeze objects and their nested properties, you can write your own library or use already created libraries like [Deepfreeze](https://github.com/substack/deep-freeze) or [immutable-js](https://github.com/immutable-js/immutable-js).

## Conclusion

I hope you've learned why `const` and `Object.freeze()` are not the same. `const` prevents reassignment and `Object.freeze()` prevents immutability.

Thanks for reading; cheers!