# node-express
node express

In command line once directory is made 
```text
npm init
```

This creates the package.json file
Fill in what what fields you want to fill in and make sure entry point is noted
 Then you create your entry point file 
 ```text 
 touch index.js
 ```
 once youve done that you can open up VScode

 In the terminal create a module JS file

 ```text
 touch myModule.js
 ```
 In VScode you can start to write code some examples would be 

 ```js
 let name = "Alex Bustillos"
console.log(name);

printName = (person) => {
    return `Hello, ${person}`;
}
console.log(printName(name));
```
To print this on the terminal you type this
```text
node index.js
```
This prints the code you have written in the index.js file
In the myModule.js file you can also write a function and make sure to include module.exports in the file like this

```js
module.exports.beBasic = () => "That's so fetch!";
```
to print that in the terminal make sure you have a variable with require and the name of the function like this
```js
const { beBasic } = require("./myModule");
```
myModule.js can now be used and any function in the file can be exported to the index.js file like so 

```js
add = (num1, num2) => {
    return num1 + num2;
};

subtract = (num1, num2) => {
    return num2 - num1;
};

module.exports = {
    beBasic,
    add,
    subtract
};
```
All the functions in the module.exports object can be used in the index.js file. Just make sure to include them in the variable thats in the index.js file like so 

```js
const { add, subtract, beBasic } = require("./myModule");
```
You can now run this in the terminal using 
```text
node index.js
```

# Express

## Setting up Express app

The first basic steps we did was create a new dir like so 
```text
mkdir hello-express
```
Then we initialized Node
```text
npm init
```
Once node was initialized we then installed Express
``` text
npm i express
```
You can use 'i' or 'install'
We then create our entry point file called index.js
```text
touch index.js
```
We then import the Express module and create an instance of an express app

```js
const express = require('express');
const app = express();
```
## Creating Routes Within the express app
To create a Home route on the express app
```js
app.get('/', (req, res) => {
    res.send('Hello, world');
});

app.listen(8000);
```

## Sending text from the server back to the client
We can create other routes in the app as well
```js
app.get('/about', (req, res) => {
    res.send('About me')
})
```
We can also have parameters in the routes as well
```js
app.get('/:input', (req, res) => {
    res.send('Hello ' + req.params.input + '!')
})
```
We can combine paths and parameters
```js
app.get('/greet/:name', (req, res) => {
    res.send('Hello' + req.params.name + 'once more');
})
```

## Sending html to the client using a view template

First we create a folder that houses our html files. In the folder we create any number of html files you need. For this example we created 3
```text
mkdir views
touch index.html about.html blog.html
```
Add basic html to see if it works and in the routes of your entry point replace **res.send**
```js
app.get('/', (req, res) => {
    res.sendFile(__dirname+'/views/index.html');
})
```
You would have to do this for all three routes. Which are index, about and blog
```js
app.get('/', (req, res) => {
    res.sendFile(__dirname+'/views/about.html');
})
app.get('/', (req, res) => {
    res.sendFile(__dirname+'/views/blog.html');
})
```
We can also use a Template engine to inhect values into the HTML and even script logic. We first need to install ejs in the terminal
```text
npm install ejs
```
In your index.js file you will need to add 
```js
app.set('view engine', 'ejs');
```
Once thats done we need to change our routes to ejs files and replace our res.sendFile statements with res.render statements. Our index.js file should look like this now
```js
app.get('/', (req, res) => {
    res.render('index')
});
app.get('/about', (req, res) => {
    res.render('about')
});
app.get('/blog', (req, res) => {
    res.render('blog')
});
```

## Referencing variables in view template

To reference variables you create an object with at least one key-value pair and pass the object in as the second argument to the render function. In the index.js file
```js
app.get('/', (req, res) => {
    res.render('index', {name: 'Anonymous'})
});
```
We can now access this name variable in our index.ejs file by embedding it with snowcones <% %> The equal sign means the value will be printed on the screen <%= %>
```ejs
<%= name %>
```