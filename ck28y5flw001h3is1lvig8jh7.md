---
title: "Introduction to JavaScript Switch Cases"
datePublished: Thu Jan 03 2019 23:00:00 GMT+0000 (Coordinated Universal Time)
cuid: ck28y5flw001h3is1lvig8jh7
slug: introduction-to-javascript-switch-cases
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1572178084279/cowOORdvb.jpeg
tags: programming, javascript, es6

---

In this short article, I will introduce you to JavaScript switch cases and how
to use them with practical examples. PS: This article is not for those without any JavaScript knowledge; it is expected that you're taking some tutorial or course and you just got to the switch cases section. This article will explain better with more practical examples to help you understand switch cases in depth.

## Prerequisites.

* Basic JavaScript knowledge
* Code editor
* Web Browser
* Your brain :)

### **The Switch Syntax**

A `switch` statement can basically replace multiple `if` checks in JavaScript. It gives a more descriptive way to compare a value with multiple variants.

The `switch` has one or more `case` blocks and an optional default case.

```javascript
switch(x) {
  case 'value1':  // if (x === 'value1')
    //code here
    [break]

  case 'value2':  // if (x === 'value2')
    //code here
    [break]

  default:
    //code here
    [break]
}
```

* The value of `x` is checked for strict equality to the value from the first
`case` (that is, `value1`) then to the second (`value2`) and so on.
* If the equality is found, `switch` starts to execute the code starting from the
corresponding `case`, until the nearest `break`(or until the end of `switch`).
* If no case is matched then the `default` code is executed (if it exists).

## Some few real examples

* **Simple Play & Pause Switch**

The `switch` statement can be used for multiple branches based on a number or
string:

```javascript
switch (movie) {
  case 'play':
    playMovie();
    break;
  case 'pause':
    pauseMovie();
    break;
  default:
    doNothing();
}
```

If you don’t add a `break` statement, the execution will "fall through" to the
next level. It's essential that you deliberately label the fall through with a
comment if you really meant it to aid debugging:

```javascript
switch (movie) {
  case 'play': // fallthrough
  case 'pause':
    pauseMovie();
    break;
  default:
    doNothing();
}
```

The default clause is optional. You can have expressions in both the switch part
and the cases if you like; comparisons take place between the two using the
`===` operator:

```javascript
switch (3 + 7) {
  case 5 + 5:
    correct();
    break;
  default:
    neverhappens();
}
```

* **Simple Maths Calc Switch**

```javascript
let average = 2 + 6;

switch (average) {
  case 4:
    alert( 'Too small' );
    break;
  case 8:
    alert( 'Exactly!' );
    break;
  case 10:
    alert( 'Too large' );
    break;
  default:
    alert( "Incorrect values!" );
}
```

Here the `switch` starts to compare `average` from the first `case` variant, that
is `4`. The match fails.

Then `8`. That’s a match, so the execution starts from `case 8` until the nearest
`break`.

If there is no **`break`**, then the execution continues with the next **`case`** without any checks.

Here is an example without `break`:

```javascript
let average = 2 + 6;

switch (average) {
  case 4:
    alert( 'Too small' );
  case 8:
    alert( 'Exactly!' );
  case 10:
    alert( 'Too big' );
  default:
    alert( "Incorrect values!" );
}
```

In the example above, we’ll see the sequential execution of three `alerts`:

```javascript
alert( 'Exactly!' );
alert( 'Too big' );
alert( "Incorrect values!" );
```

* **getDay() method switch case**

The getDay() method returns the weekday as a number between 0 and 6.

(Sunday=0, Monday=1, Tuesday=2 , Wednesday=3, Thursday=4, Friday=5, Saturday=6)

This example uses the weekday number to calculate the weekday name:

```javascript
    switch (new Date().getDay()) {
      case 0:
        day = "Sunday";
        break;
      case 1:
        day = "Monday";
        break;
      case 2:
         day = "Tuesday";
        break;
      case 3:
        day = "Wednesday";
        break;
      case 4:
        day = "Thursday";
        break;
      case 5:
        day = "Friday";
        break;
      case 6:
        day = "Saturday";
    }
```

The result of the `day` will be the current weekday in day format.

PS: This would change according to when you’re reading this article.

I wrote this article on 01/04/2019, which is a Friday, so the result would be:

    Friday

### The default Keyword

The **default** keyword specifies the code to run if there is no case match,
more like an else statement:

```javascript
    switch (new Date().getDay()) {
      case 6:
        text = "Today is Saturday";
        break; 
      case 0:
        text = "Today is Sunday";
        break; 
      default: 
        text = "It's not the weekend yet!";
    }
```

The result of the text will be: **It's not the weekend yet!**.

The **default** case does not have to be the last case in a switch block:

```javascript
    switch (new Date().getDay()) {
      default: 
        text = "Its not weekend yet!";
        break;
      case 6:
        text = "Today is Saturday";
        break; 
      case 0:
        text = "Today is Sunday";
    }
```

> If the `default` is not the last case in the switch block, remember to end the default case with a break.

## Conclusion

There are so many practical examples of switch cases. You can head
[here ](https://javascript.info/switch)to learn more about switch cases.

Thanks for reading!