# Javascript-Modules
PATH DESCRIPTION
    ./ ---> indicates that the file being reference is in the same folder as the file it is imported to 
    ../ ---> indicates that the file being reference is in the same folder as the parent folder (one folder above)

###### In JavaScript, programs are written within a `my_app.js` file. <br>
This program may have different components which have different functions evaluating different things. <br>
Hovever if we can take the different components of a program and break them up into separate modules. <br>
They can each handle a particular task.<br>
For example, <br>
The program `my_app.js` can be broken into 2 additional components. <br>

    FIRST module =====> `database_logic.js` which contains code to store and retrieve data from a database.
    SECOND module ======> `date_formatting.js` which contains functions to convert date values from one format to another.
This shows modules requires some management. <br>

# Implementing Modules in JAVASCRIPT
The SYNTAX we us depends on your RUNTIME ENVIRONMENT (RE) your code is excecuted in.<br>

    1. Node.js (RE) -  module.exports and require() syntax.
    2. Browser (RE) -  ES6 import/export syntax.

## Implementing Modules in Node.js
How to use the Node.js module.exports object to export code from a file - meaning its functions and/or data can be used by other files/modules.<br>
How to use the Node.js require() function to import functions and/or data from another module.<br>

Every JavaScript file that runs in a Node environment is treated as a distinct module that exports values and funciton to be used by other modules.<br>
These resources are must be exported and imported.<br>
When a program is executed in the Node environment, process.argv is an array holding the arguments provided.<br>
Creating a module to export export solves the problem of having to write the same code in each of the other files.<br>

### To Create a Module.exports
    -> Create a file
    -> Declare the function to use
    -> Make function available to other files
        -> How? Add them as properties to the built-in module.exports object.
    -> Ultimately storing a function or value in the object allows us to retrieve it.
    
2 ways to export a function or a file from a module:<br>
SYNTAX: <br> 
        ` module.exports = literal | function | object` <br>
        `module.exports.variable = literal | function | object`
        
    module.exports.functionName = declared functionName;
    moduel.exports.newFunctionName = new function expression;
<br>

### To export from a Node module, assign a value to the module.exports object like so:<br>
// Export a named function.<br>

    module.exports.functionToExport = functionToExport;

// Export a function expression.<br>
    
    module.exports.functionToExport = () => {};
    
// Export an object of the values assigned module.exports:

    module.exports = {
      functionToExportA,
      functionToExportB
    };

#### EXAMPLE /* converters.js */

    function celsiusToFahrenheit(celsius) {
      return celsius + 1;
    }
    module.exports.celsiusToFahrenheit = celsiusToFahrenheit;                //named function
    module.exports.fahrenheitToCelsius = function(fahrenheit) {              //function expression
      return (fahrenheit - 32) * (5/9);
    };

##### `module.exports` is an object that is built-in to the Node.js runtime environment. <br>
Other files can import this object, and make use of functions or value.<br> 
Lets examine the global module object which has an exports property<br>

        console.log(module)
        // {
        //   id: ".",
        //   path: "...",
        //   exports: {}, ...
        // }
        
To use the imported items use another built-in Node.js feature: `the require() function`<br>
The require() function accepts a string as an argument. The file path to the module you would like to import.<br>


        const declaredVariable = require('string');
        EX. const myModule = require('path/to/myModule.js');
            const converters = require('./converters.js');     <---- importing js file from above 
        
The entire module.exports object is returned and stored in the variable declaredVariable.<br>

Modules export files which may contain a large number of functions but only one or two of them are needed.<br>
SOLUTION: 
    Use object destructuring to extract only the needed functions.<br>
    
        const { needed function to import } = require('./file_name.js');

#### AFTER IMPORTING AN OBJECT FROM ANOTHER MODULE USING REQUIRE().<BR>
There are a few ways to extract values out of an object. 
The quickest is with object destructuring syntax:<BR>

        const object = require('./fileName.js');
        const { valueA, valueB, valueC } = object;

You can extract each value one at a time:<BR>

            const valueA = object.valueA(function we are importing from object);
            const valueB = object.valueB(anther function we are importing from object);

Use object destructuring to import multiple values from a module:<BR>

    const { valueA, valueB, valueC } = require('/path/to/myModule');

### Implementing Modules in the Browser

## ES6 Named Export Syntax
Basics of exporting and importing using the ES6 export and import syntax!
the functions you wish to reuse can be exported using the named export syntax below:<br>

`export { resourceToExportA, resourceToExportB, ...}`<br>
the name of each exported resource is listed between curly braces and separated by commas.<br>
/* javascript-functions.js */<br>
const namedFunctionOne = (variable) => {//function logic here omitted} <br>
const namedFunctionTwo = (variable) => {//function logic here omitted}<br>
The two functions are exported using the ES6 export statement.<br>
export { namedFunctionOne, namedFunctionTwo };<br>
These exported functions are now available to be imported and used by other files!<br>

## ES6 Import Syntax
The ES6 syntax for importing named resources from modules is similar to the export syntax:<br>

     import { exportedResourceA, exportedResourceB } from '/path/to/javascript-functions.js';
Let’s update the secret-messages program such that it now imports functionality from dom-functions.js. Doing so requires two important steps.<br>
First, update /* javascript-file-using-exported-funcitons.js */:<br>
/* javascript-file-using-exported-funcitons.js */<br>

    import { namedFunctionOne, namedFunctionTwo } from '../modules/dom-functions.js';<br>


In javascript-file-using-exported-functions.js, the functions namedFunctionOne() and namedFunctionTwo() are imported from the module ../modules/exported-file-with-functions.js.<br>
The ../ indicates that the modules/ folder is in the same folder as the parent folder, secret-messages/.<br>

    <script type="module" src="./secret-messages.js"> </script>

the addition of the attribute type='module' to the <script>



