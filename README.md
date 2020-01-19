[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# Intro to Express

## Learning Objectives

- Understand Express
- Use `npm` to manage project dependencies
- Use `require` to organize code
- Install Nodemon

<br />

## What Are We Learning This Morning?

This morning, we are going to learn about how to set up and configure a server that will listen for HTTP requests from the browser.

<br />

## Intro
How many of you, prior to this course, had heard of the MEAN or MERN stack?  Today, we will be talking about [ExpressJS](https://expressjs.com/) the "E" in the MEAN/MERN stack. It is one of the most heavily used libraries in the entire Node community.  According to the Express home page, Express is a "Fast, unopinionated, minimalist web framework for Node.js".

> Node.js is not a framework. It is an application runtime environment that allows you to write server-side applications in javascript. Javascript that does not depend on a browser.

Some frameworks, like Rails, are very opinionated frameworks- meaning that it follows convention over configuration.  A Rails developer can go into any other Rails app, and understand the basic layout, because all Rails applications are built in the same way, with the same file structure.  

Express is much less opinionated. We have a lot of freedom in how we structure our application (folders and files, how to load different files, how to manage dependencies, etc).  

<br />

## Recap

&#x1F535; **YOU DO: 5 minutes**

With your buddy, discuss the following questions:

- What are the **HTTP verbs** and how are they used?
- What are the different parts of a URL and what is the purpose of each?
- Explain a request/response

<br />

## What is npm?

&#x1F535; **YOU DO:** Take 5 minutes to read and watch this [video](https://docs.npmjs.com/getting-started/what-is-npm)

> Summary: **npm** (node package manager), allows us to install dependencies for our Node.js application.

You may also see tutorials refer to a package called `Yarn` for installing packages.  This is an alternative to NPM that is built by Facebook. Both packages pull from the NPM, so anything you see done in Yarn can also be done with NPM. 

<br />

## Codealong: Hello World - Express

I **HIGHLY** recommend that you pay attention, write the commands down, and refer back to this lesson plan as you become more familiar with Express and Node.js:

<br />

### STEP 1 - Initialize a Simple Hello World Express Application

In the terminal:

```bash
$ cd ~/ "cd to your codealong directory"
$ mkdir hello-express
$ cd hello-express
$ npm init
// make sure that when you get to 'entry point' that you change 
that to 'server.js'.
// if you make a mistake, you can always type 'no' when it asks
you whether this is 'ok' at the end of the questions/set up
$ code .
```

- `npm init` will initialize a new Node.js application. Upon initialization, it will prompt you for your input in order to update the `package.json`.

- If we hit enter and use all of the default values (except for the `server.js`) and we take a look at the contents of the `package.json` file.

- The `package.json` file contains meta data about your app or module. More importantly, it includes the list of dependencies to install from npm when running npm install. **We** certainly don't want to keep track of them!  This makes it really easy for other people to work on the same app.  All they need to do is clone your repo, and then npm install all of the dependencies in order to start working on the app.

> **Pro Tip**: `npm init -y` is a shortcut that will select all of the defaults for your `package.json` for you.

<br />

&#x1F535; **YOU DO: 2 minutes**

1. Walk through STEP 1 above to instantiate your `hello-express` app.

<br />

### STEP 2 - Install Express

1. Let's install the express node module using `npm`. In the terminal type:

```bash
$ npm install express
```
or

```bash
$ npm i express
```

We could have also entered express manually- to the dependencies list in our package.json file.  If we added Express this way, we would need to run `npm install` afterward in order to install the package. 
    
 **SIDE NOTE** As we saw during `npm init`, the default file for a node app is `index.js`.  If your package.json still uses this as the default, you should update it to `server.js`.

<br />

&#x1F535; **YOU DO: 1 minute**

1. Walk through STEP 2 above, and add Express to your `hello-express` app.

<br />

### STEP 3 - Create a `server.js`

2. Let's make a new file `$ touch server.js` and add the following contents:

```javascript
const express = require('express'); // Loading the express module on our server
const app = express(); // Creates a new instance of express on our server


app.get('/', function(req, res) { 
  // when a request comes in at localhost:3000, it will respond 
});

const port = process.env.PORT || 3000; // tells the server where to listen for requests

app.listen(port, function() {
  // tells the server where to listen for requests on port 3000

  console.log('hello-express is listening on port ' + port);
}); // actualizing the line above
```

<br />

### Let's talk through this...

#### `require()`

`require()` is a JS keyword with which we are going to become very, _very_ familiar. It is a Node.js feature that loads modules. We are "requiring" the Express module and saving all of that code to the variable `express` on line one. 


#### `const app = express()`

Requiring Express isn't quite enough. We have required and assigned all of Express's code to the `express` variable, but Express is an application that needs to be invoked. 

When we invoke express, we get an instance of all of the functionality that Express provides.  We then save that instance to a variable called `app`.

#### `app.listen(port, callback)`

With express invoked and running, we now have access to various functions and properties that allow us to configure and set up our application. The first one that we are going to use is the `listen()` function. It tells express and node to listen for HTTP requests on whatever port is passed in.

<br />

## Let's Run Our App

If we run the application (`$ node server.js`) we can see our console.log in the terminal `hello-express is listening on port 3000`. This means that our server is running on port 3000. Let's try going to the localhost of that port number. What happens?

#### OH NOES, what's going on here?

Basically, we have told the server what port to listen to (3000), but we have not specified what to do if a user goes to the `"/"` or root/home route. 
    
1. Use `ctrl + c` to stop the server.
    
2. Let's update the `server.js`:

```javascript
app.get("/", function(req, res){
  // display 'Hello World!'
  res.send('Hello World!');
});
```
With the script above, we are telling the app that when a user goes to our home route at localhost:3000 (their request), that we will send back a response of 'Hello World!'    
    
1. Let's restart the server (`$ node server.js`) and reload the browser. You should now see `Hello World!`.

<br />

## Nodemon

This is great!  But it is kind of a pain to have to restart the server every time we make changes to our files... 

[Nodemon](http://nodemon.io/) is a very helpful npm module that will automatically restart your server when a file is saved.

```bash
$ npm install --global nodemon
```

> When using the `--global` flag (-g for short), we are specifying that nodemon will be installed "globally" (not per project) so that we can utilize nodemon across all of our node applications.

<br />

After installing, we start up our application a little bit differently. In the terminal type:

```bash
$ nodemon server.js
```

Instead of `node server.js`. 

<br />

Pretty easy, eh?

<br />

## RECAP - What have we done so far?

We just built the foundation for our server and for your first web application!

- We created a file (`server.js`) that contains instructions for the server (Node).
    - **Node** is our server software that we have configured to run on a port to listen for incoming HTTP requests from the browser.
- We installed **Express**, which is our lightweight JS framework, and was built to help simplify the job of building an application that can interact with HTTP requests coming from the internet.
- We defined a single root/home route (`/`). When Node receives a request via `http://localhost:3000`, it will serve "Hello World" as a response. All of our local routes for this app will start with `http://localhost:3000`, as we have set our default port to 3000.
- We also installed Nodemon which will automatically restart our node server whenever a change is detected, so we don't have to manually stop/restart our server every time a file changes.W

<br />

&#x1F535; **YOU DO (15 minutes)**

Get together with your buddy. Remember: We are here and you can still ask questions! Spend the next 15 minutes on this exercise.

http://expressjs.com/en/starter/basic-routing.html

1. Write a second route underneath the first that listens for `/greeting` and responds with `'Hey, WDI 13!'`

1. Write a third route underneath the that one that listens for `/rihanna` and responds with `"Work work work work work"`

<details>
<summary>SOLUTION</summary>

```javascript
app.get('/greeting', (req, res) => {
  res.send('HEY, WDI 13!');
});

app.get('/rihanna', (req, res) => {
  res.send("Work work work work work");
});
```
</details>

<br />

**Stretch Goal**: Implement `req.query` functions in one of your routes explanation [here](http://expressjs.com/en/api.html#req.query)

<br />

---
