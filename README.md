# Javascript-Modules

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

How to use the Node.js module.exports object to export code from a file - meaning its functions and/or data can be used by other files/modules.<br>
How to use the Node.js require() function to import functions and/or data from another module.<br>

Every JavaScript file that runs in a Node environment is treated as a distinct module that exports values and funciton to be used by other modules.<br>
These resources are must be exported and imported.<br>
When a program is executed in the Node environment, process.argv is an array holding the arguments provided.<br>
Creating a module to export export solves the problem of having to write the same code in each of the other files.<br>

##### To Create a Module.exports
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
###### To export a value from a Node module, you can assign a value to the module.exports object like so:<br>
// Export a named function.<br>

    module.exports.functionToExport = functionToExport;

// or... export a function expression.<br>
    
    module.exports.functionToExport = () => {};
    
Or you can assign module.exports to an object of the exported values:

    module.exports = {
      functionToExportA,
      functionToExportB
    };

######/* converters.js */

    function celsiusToFahrenheit(celsius) {
      return celsius + 1;
    }
    module.exports.celsiusToFahrenheit = celsiusToFahrenheit;
    module.exports.fahrenheitToCelsius = function(fahrenheit) {
      return (fahrenheit - 32) * (5/9);
    };

`module.exports` is an object that is built-in to the Node.js runtime environment. <br>
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


