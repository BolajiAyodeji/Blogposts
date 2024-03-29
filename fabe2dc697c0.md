---
title: "Introducing CSS Custom Properties (Variables)"
datePublished: Mon Mar 25 2019 04:31:15 GMT+0000 (Coordinated Universal Time)
cuid: fabe2dc697c0
slug: introducing-css-custom-properties-variables
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1560101696129/Tm_aBkKwB.png
tags: variables, css, developer, tech

---

In the past years, maintaining CSS was a very big problem for bigger projects or complex apps as a result, building reusable components and cleaner styles were hard to achieve.

[CSS Preprocessors](https://guide.freecodecamp.org/css/css-preprocessors/) came to solve this problem and have been around for years now (SASS, LESS, e.t.c). They extend CSS with key features like variables, operators, interpolations, functions, imports, mixins e.t.c.

However, in [Modern CSS](https://medium.com/actualize-network/modern-css-explained-for-dinosaurs-5226febe3525), we now have a new powerful feature called **Custom properties**, otherwise known as **CSS variables** or **cascading variables**. Now you can declare variables directly in your CSS without having to use CSS Preprocessors.

In this article, I’d show you how to start using CSS variables. Let’s roll :)

* * *

If you’re familiar with JavaScript or other programming languages, you should understand how variables work already.


```
let name = 'Bolaji Ayodeji'
```


A variable stores some sort of information or data, that would be used later in your program.


```
console.log(name);
```


### What are CSS variables?

> **_Custom properties_** _(sometimes referred to as_ **_CSS variables_** _or_ **_cascading variables_**_) are entities defined by CSS authors that contain specific values to be reused throughout a document. They are set using custom property notation. — _**_MDN DOCS_**

### CSS variables syntax

A CSS Variable is defined with a special syntax, with **two dashes** before the variable name (`--variable-name`), then a colon and the variable value.


```
.container {
 --black: #000;
}
```


### Accessing the variable

You can access the already declared variable using `var()`


```
.container {
 --black: #000
 color: var(--black);
}
```


### Variables Scope

CSS Variables can be defined inside any CSS element.

```
body {  --color: red;}
```

```
h1 {  --color: red;}
```

```
p {  --color: red;}
```

```
span {  --color: red;}
```

```
a {  --color: red;}
```

However, adding variables to a selector makes them available to **ONLY** their children. If you add a variable inside a `.container` selector, it’s only going to be available to children of `.container` . Outside `.container` , the variable will not work.

%[https://codepen.io/iambolajiayo/pen/BbMGqr]

Though we set `p` to be red, it works for only `p` tags within `.container` , any `p` outside `.container` will not inherit this style.

### : root

`:root` is a CSS pseudo-class that identifies the document itself.

A better way to declare CSS variables is to add the variable to `:root`, this makes it available to all the elements in the page.

%[https://codepen.io/iambolajiayo/pen/gEqZOe]

Now all `p` tags are red irrespective of their position or parent.

### CSS Variables are case sensitive

This variable:

```
--color: red;
```

is not the same as:

```
--Color: red;
```

### Setting a fallback value for var()

`var()` accepts a second parameter, which is the default fallback value when the variable value is not set:


```
p {
  color: var(--red, #f00);
}
```

%[https://codepen.io/iambolajiayo/pen/xBMmrq]

Here we forgot to declare `--red` but `p` still has the red color because we already have a fallback value.

### Browser Support

![](https://cdn-images-1.medium.com/max/2400/1*-HHDutFGICwb84UsH91rsQ.png)Browser support for CSS Variables [according to Can I Use](https://www.caniuse.com/#feat=css-variables).

CSS variables are supported in modern browsers. I personally don’t focus on IE and far older browsers because a large number of internet users are using modern browsers now, just a few aren’t. So If you don’t need to support Internet Explorer and old versions of the other browsers, CSS variables should be your best friend.

### Conclusion

CSS Variables follow the normal CSS cascading rules, with precedence set according to the specificity. We can also use the values of custom properties in JavaScript, just like standard properties.

_Complex websites have very large amounts of CSS, often with a lot of repeated values. For example, the same color might be used in hundreds of different places, requiring global search and replace if that color needs to change. Custom properties allow a value to be stored in one place, then referenced in multiple other places. An additional benefit is semantic identifiers. For example,_ `--black` is easier to understand than `#00000` , especially if this same color is also used in other contexts. -**MDN**

CSS variables are cool and have come to stay, if you want your CSS styles and development to become clean, easier and more efficient, you should stick to CSS variables :)

For more knowledge, read [here](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)