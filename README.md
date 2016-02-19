# Mocha Testing Framework

## Objectives

1. Describe how to install Mocha and Chai Expect
1. Describe how to create a simple test
1. Describe how to launch a test

## Overview

Imagine that you are at a hackathon, and you're pressed for time to finish your app. You make the last minute changes, go on stage with your buddies to present the prototype and boom! It's not working, because your last changes broke something important. If only you had tests to catch that error! Tests are great time-savers for the simple reason that they automate manual testing.

How do you test applications in Node to avoid breaking existing functionality? You can use one of the most popular testing frameworks Mocha. This lesson will cover the basics of Mocha testing framework and Chai Expect behavioral-driven language to get you started with the labs.


## Installing Mocha and Chai Expect

Note: In the labs, all you need to do is to run `npm install` because we did all the setup work for you. Read the rest of this section only if you are starting from scratch. Otherwise, skip to Writing Mocha Tests to understand how Mocha and Chai work. And if all you want to know is how to run the tests for your lab, then you can skip this entire lessons, because all you need for the labs is to run these two commands:

```
npm install
npm test
```

First, we need to install Mocha and Chai. To do so, you'll need to open your terminal and create either the `node_modules` folder or the `package.json` file:

```
mkdir node_modules
```

```
npm init
```

Then, you can use the `npm install NAME` to install Mocha and Chai Expect. We'll cover npm and modules later in more details. For now all you need to know is the modules are akin to browser JavaScript libraries or [Ruby gems](https://rubygems.org).

```
npm install mocha@2.4.5 --save-dev
npm install chai@3.5.0 --save-dev
```

That's it. In your `node_modules` you should see two new folders: `mocha` and `chai`, if you run ` ls node_modules` to get the list of directories.

Note: Chai comes with Expect so by installing Chai we are getting Chai Expect.

## Writing Mocha Tests

Expect has a lot of features and if you're familiar with behavioral-driven development (like from Rspec and Jasmine), you can learn Expect fast. We won't be covering all of the features in the lesson, only the most important ones which you'll encounter in the labs of this course.

You can create a file `test.js` to follow this exercise. So in the beginning, we need to import the module. 

```js
var expect = require('chai').expect
```

Then we need to create some objects which we will be testing. Typically these objects will come from other modules (unit testing):

```js
var name = 'React Quickly'
var url = ['http://reactquickly.co', 'https://www.manning.com/books/react-quickly']
```

Next, we use `describe` with a string and function arguments to define the test suite. The first argument is a string of the object that we are testing. (object in a broad sense, it can be a module or a function). Typically it's a noun:

```js
describe('name and url', function() {
```

The next method is `it()`, think about it as the test case. The first argument is the behavior, i.e., a plain english description of the expected behavior of the code we're testing:

```js
  it('must be a string', function(done){
```

We invoke `expect()` with the object which we want to test like `name` or `url`. Then, we use chained methods and properties like `to.be.a()` to check for the type (string) and value (React Quickly):

```js
    expect(name).to.be.a('string')
    expect(name).to.equal('React Quickly')
```

`expect` actually calls your functions and tests your variables by using a matcher like `to.be.a`. Then `expect` compares the actual value (`name`) to the value expected value (`string`) passed to the matcher.

The `to.have` checks for properties with `length` being a property of an array:

```js    
    expect(url).to.have.length(2)
```

We can use `deep.property` to check for values of the nested elements. In this case, we're checking for the value of the second element of the `url` array:

```js
    expect(url).to.have.deep.property('[1]', 'https://www.manning.com/books/react-quickly')
      .with.length(43)
```

It's important to define the `done` argument in the callback, because that's how Mocha will know that this test is over:

```js
    done()
  })
})
```

So the whole `test.js` must look like this. Compare agains your file:

```js
var expect = require('chai').expect
var name = 'React Quickly'
var url = ['http://reactquickly.co', 'https://www.manning.com/books/react-quickly']
describe('name and url', function() {
  it('must match the values', function(done){
    expect(name).to.be.a('string')
    expect(name).to.equal('React Quickly')
    expect(url).to.have.length(2)
    expect(url).to.have.deep.property('[1]', 'https://www.manning.com/books/react-quickly')
      .with.length(43)
    done()
  })
})
```

Now we are ready to run our first Mocha test. How exciting!

## Launching Mocha Tests

There are two ways to run Mocha tests: local and global. We'll cover the local because that's what we'll be using in our labs. Assuming you installed Mocha with the command in the first section of this lesson, type this in your terminal:


```
node_modules/mocha/bin/mocha test.js
```

You should see this output which mean that test was run successfully:

```
  name and url
    ✓ must match the values


  1 passing (11ms)
```

The idea behind this command `$ node_modules/mocha/bin/mocha test.js` is to point to your local version of Mocha. Now open `package.json` in your editor. If you don't have it, then create it. Find a line with `scripts` and edit the value of `test`:

```
  "scripts": {
    "test": "node_modules/mocha/bin/mocha test.js"
  },
```  

This will enable us to use `npm test` to test with local Mocha the `test.js` file. This is how all future labs in this course will test your solutions. Just remember, run `npm install` so that each lab can download their own local versions of Mocha and Chai. If this is confusing, stay calm. We'll cover modules, npm and `package.json` later. For now to run the labs, just remember to run these two commands:

```
npm install
npm test
```

And the tests in the lab will verify your solution.


## Resources

1. [Mocha](https://mochajs.org)
1. [Test suite](https://en.wikipedia.org/wiki/Test_suite)
1. [Chai BDD](http://chaijs.com/api/bdd)


---

<a href='https://learn.co/lessons/node-mocha' data-visibility='hidden'>View this lesson on Learn.co</a>
