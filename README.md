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

