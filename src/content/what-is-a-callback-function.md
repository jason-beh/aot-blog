---
layout: post
title: What Is A Callback Function?
image: img/what-is-a-callback-function/1.jpg
author: Jason Beh
date: 2019-10-05T03:01:09+00:00
tags:
  - What Is It
draft: false
---

This article teaches you an important concept in programming called callback functions and how to use them.

---

## The Definition 🤓

Imagine as if you want to cook pasta now and you don't have the ingredients. Hence for you to cook pasta, you will need to buy the ingredients first.

In simple steps:

1. Buy ingredients
2. Cook pasta

A callback function is a function that is executed immediately after the completion of the immediate past function.

Yes, you might have guessed it right. In this example, Step 2 will be our callback function.

---

## Why Is This Important? 🤔

The concept of callbacks is essential because it shows that it is possible to perform a function after the complete execution of a particular function.

It is impossible to cook pasta without getting the ingredients first.

```javascript
function getIngredients() {
  setTimeout(function() {
    console.log('Bought ingredients!');
  }, 3000);
}
function cookPasta() {
  console.log('Pasta is cooked!');
}
getIngredients();
cookPasta();
```

If you look at the code above, you might have noticed that we have performed the logic in terms of code. Getting the ingredients tend to incur some time, which is why I stimulated the process with a setTimeout function.

However, the result might not be the case.

```
// Output
Pasta is cooked!
Bought ingredients!
```

As you can see, we didn't manage to buy the ingredients and cook the pasta first, because Javascript is very sensitive to listening to programming events. This means that it will continue executing without waiting for the response time.

---

![Red Carpet](img/what-is-a-callback-function/2.jpg)

###### Red carpet for Callback

## Introducing Callbacks 🙌

Now, we can easily solve the whole thing by using callback functions.

```javascript
function getIngredients(callback) {
  setTimeout(function() {
    console.log('Bought ingredients!');
    callback();
  }, 3000);
}
function cookPasta() {
  console.log('Pasta is cooked!');
}
getIngredients(cookPasta);
```

Woah, it looks a bit overwhelming, but let me break it down for you.

In our getIngredients() function, we have now created an additional parameter that takes in a callback function. Then, it calls the callback function after buying the ingredients.

Functions can be taken as parameters because functions are considered as first-class objects in the world of Javascript. They can, therefore, be treated as variables that can be inserted as inputs.

## Another Popular Way of Creating Callbacks 💯

One popular way of creating callbacks that you may find conventional in these modern days is demonstrated below.

```javascript
function getIngredients(callback) {
  setTimeout(function(){
    console.log("Bought ingredients!");
    callback();
  },3000)
}
getIngredients(function() {
  console.log('Pasta is cooked!');
}
```

Notice the difference in calling the function.

Sometimes, you may not want to purposely create standalone functions that will be called only as a callback later. With the first-class object feature, you can just slap the whole thing as a parameter as well.

## Callback Use Cases 💪

You will often find yourself using the power of callbacks when you use APIs, especially when it comes to success in receiving data or checking for errors.

```javascript
router.get('/posts', function(err, data) {
  if(err) throw err;
  return data;
}
```

- This function tries to get data from the "/posts" route.
- If there is an error, we stop everything and show the error.
- If there is no error, we will return the data.

Callbacks are important in this context because API calls usually take some time for it to receive and send back the HTTP request.

## Closing Thoughts 💡

Congratulations, this is the essential concept of a callback function and you have made it to the very end of this article.

I hope you utilize callback functions, but not excessively, because there is a drawback to overusing them called 'callback hell'.

Be sure to not miss out on the next article, by subscribing to our newsletter below.
