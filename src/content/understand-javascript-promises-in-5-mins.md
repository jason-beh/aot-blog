---
layout: post
title: Understand Javascript Promises In 5 Mins
image: img/understand-javascript-promises-in-5-mins/1.jpg
author: Jason Beh
date: 2019-10-12T03:01:09+00:00
tags:
  - What Is It
  - Javascript
draft: false
---

Javascript Promises is an essential concept that all developers should grasp, including you! If you missed out on Part 1 about understanding what is a callback function, click [here](https://agentsoftechclub.com/what-is-a-callback-function/). The concepts there are important because the knowledge of callback is the prerequisite for this article.

---

## The Problem ⚠️

If you remember callback functions, they can be very useful in our daily coding life. This is because most libraries written by other people have callbacks.

```javascript
fs.readdir(source, function(err, files) {
  if (err) {
    console.log('Error finding files: ' + err);
  } else {
    files.forEach(function(filename, fileIndex) {
      console.log(filename);
      gm(source + filename).size(function(err, values) {
        if (err) {
          console.log('Error identifying file size: ' + err);
        } else {
          console.log(filename + ' : ' + values);
          aspect = values.width / values.height;
          widths.forEach(
            function(width, widthIndex) {
              height = Math.round(width / aspect);
              console.log('resizing ' + filename + 'to ' + height + 'x' + height);
              this.resize(width, height).write(dest + 'w' + width + '_' + filename, function(err) {
                if (err) console.log('Error writing file: ' + err);
              });
            }.bind(this),
          );
        }
      });
    });
  }
});
```

As you can see, there is a monster called callback hell. The snippet above is obtained from [callbackhell.com](http://callbackhell.com/), where you can also learn more about how to deal with this problem in various ways.

## Introducing Promises ✌️

In simple terms, a promise is an object that returns a value soon. Usually, a promise can only be in one of three states:

- Fulfilled
- Rejected
- Pending

Now, the pending state means that the promise hasn't resolved yet, hence it needs more time. For fulfilled and rejected, the promise has been resolved.

Below is an example that we will go through together:

```javascript
var myPromise = new Promise(function(resolve, reject) {
  // Resolve the promise after 3 seconds
  setTimeout(() => resolve('I am resolved!'), 3000);
});
```

To write a promise, we use the new Promise syntax to create an instance of the class called Promise. Then the promise will automatically resolve itself after 3 seconds.

### Imagine this:

- After 1 second, the state of the promise will be "pending", because it has not been resolved or rejected yet. Result will be undefined.
- After 3 seconds, the state of the promise will be "fulfilled", because it has been resolved.

```
// myPromise Properties (Pending) - After 1 second
state: "pending"
result: undefined

// myPromise Properties (Resolved) - After 3 seconds
state: "fulfilled"
result: "I am resolved!"
```

Likewise, you can also reject the promise with the example below, by using the reject function with whatever value that you want to return.

```javascript
var myPromise2 = new Promise(function(resolve, reject) {
  // Reject the promise after 2 seconds
  setTimeout(() => reject(new Error('Opps')), 2000);
});
```

The state change will be the same as above:

- After 1 second, the state of the promise will be "pending", because it has not been resolved or rejected yet. Result will be undefined;
- After 2 seconds, the state of the promise will be "fulfilled", because it has been resolved.

```
// myPromise2 Properties (Pending) - After 1 second
state: "pending"
result: undefined

// myPromise2 Properties (Resolved) - After 2 seconds
state: "fulfilled"
result: Error('Oops') // this is the typical error object
```

---

![How?](img/understand-javascript-promises-in-5-mins/2.jpg)

###### How?

## What Else Can Promises Do? 🤔

Hold up, promises have more up their sleeves! There are three more very useful functions that are usually utilized with promises:

1. then
2. catch
3. finally

### Then?

The most vital one, .then, has the following syntax.

```javascript
myPromise.then(
  function(result) {
    /* handle a successful result */
  },
  function(error) {
    /* handle an error */
  },
);
```

You might have guessed it. Then has two arguments for the fulfilled and rejected state. The logic is if it isn't fulfilled, the first function argument won't run and the second one will run.

Let's move to an example.

```javascript
var myPromise2 = new Promise(function(resolve, reject) {
  // Reject the promise after 2 seconds
  setTimeout(() => reject(new Error('Opps')), 2000);
});

myPromise2.then(
  resolve => alert(resolve), // it won't run this
  error => alert(error), // shows "Error: Oops" after 2 seconds
);
```

Note: If you only care about the resolve part in the .then() function, you can provide only one argument to it.

### Catch?

The effort to always write the following code for error is tedious, hence you should consider the catch function which accepts only one argument for the rejected state:

```javascript
var myPromise2 = new Promise(function(resolve, reject) {
  // Reject the promise after 2 seconds
  setTimeout(() => reject(new Error('Opps')), 2000);
});

myPromise2.catch(alert) // shows "Error: Oops" after 2 seconds
);
```

### Finally?

Finally is executed regardless it is a resolved or rejected state in the end. This way, you don't need to write twice the amount of code for both resolved and rejected states.

```javascript
var myPromise2 = new Promise(function(resolve, reject) {
  // Reject the promise after 2 seconds
  setTimeout(() => reject(new Error('Opps')), 2000);
});

myPromise2
  .finally(() => stopAnimation()) // stops animation
  .then(() => alert('Success')) // it won't run this
  .catch(alert) // shows "Error: Oops" after 2 seconds
);
```

This is useful for doing things such as removing the modal or loading animation.

---

![How?](img/understand-javascript-promises-in-5-mins/3.jpg)

###### How?

## How Does It Solve Callback Hell? 💻

Suppose the following scenario, where you have a few things listed in your to-do list and you can only do them in this order:

1. Cook Breakfast
2. Do Laundry
3. Meet Client
4. Watch a Movie

Your code might look like this:

```javascript
const beProductive = nextStep => {
  cookBreakfast(function (doneWithBreakfast) {
    doLaundry(function (doneWithLaundry) {
      meetClient(function (doneWithClient) {
        watchMovie(function (doneWithMovie) {
          feelHappy(donewithMovie)
        })
      })
    })
  })
}

beProductive(function (happinessLevel) => {
  alert(happinessLevel);
})
```

The code above looks crazy, doesn't it? Now behold the power of promises.

```javascript
const beProductive = () => {
  return cookBreakfast()
    .then(doLaundry)
    .then(meetClient)
    .then(watchMovie);
};

beProductive().then(alert);
```

## Closing Thoughts 💡

I hope you have learned something in this sweet and short tutorial on Promises. Make sure to utilize them fully and as soon as possible to write better code!
