# Javascript-Modules
PATH DESCRIPTION

    `./ `---> indicates that the file being referenced is in the same folder as the file it is being imported into 
    `../`---> indicates that the file being referenced is in the same folder as the parent folder (one folder above)

###### In JavaScript, programs are written within a `my_app.js` file. <br>
These programs have components and functions evaluating different tasks. Separating these components into modules allows them to handle the different task separately.<br>
                            `So, modules are files that export code.`
For example, <br>
`my_app.js` can be broken into 2 components/modules. <br>

        1st module =====> `database_logic.js` --------> code to store and retrieve data from a database.
        2nd module ======> `date_formatting.js` -----------> function code to convert values from one format to another.

# Implementing Modules in JAVASCRIPT
The SYNTAX we us depends on your RUNTIME ENVIRONMENT (RE) your code is excecuted in.<br>

    1. Node.js (RE) -  module.exports and require() syntax.
    2. Browser (RE) -  ES6 import/export syntax.

# Implementing Modules in Node.js

    To export code (files/modules to be used elsewhere) -----> `module.exports` object.
    To import code (functions or data from another modules) -----> `require()` imports. 

Every JavaScript file that runs in a Node environment is treated as a module that exports values and functions used by other modules, So must be exported and imported<br>
<br>
`process.argv` is an array which holds arguments when a program is executed Node.<br>

    Creating a module solves having to write repeated code in different files.

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

# Implementing Modules in the Browser

## ES6 Named Export Syntax
Exporting and importing using the ES6 export/import syntax!<br>
Named exports — each item (be it a function, const, etc.) has been referred to by its name upon export, and that name has been used to refer to it on import as well.
#### Syntax Example 
2 functions you wish to reuse using the named export syntax:<br>

    export { resourceToExportA, resourceToExportB, ...}
The name of each exported resource/data or function is listed between curly braces and separated by commas.<br>
<br>
#### Example 
`/* javascript-functions.js */`<br>

    const namedFunctionOne = (variable) => {
                    //function logic here omitted
                    } 
    const namedFunctionTwo = (variable) => {
                    //function logic here omitted
                    }
    export { namedFunctionOne, namedFunctionTwo };
These 2 functions or its data are exported using the ES6 export statement. They can be imported and used by other files/mudules!<br>

## ES6 Import Syntax
Importing named resources is similar to the export syntax:<br>

     import { exportedResourceA, exportedResourceB } from '/path/to/javascript-functions.js';
     
Use the import to update the module requiring the use of the exported functions so it imports functionality from javascript-functions.js. <br>
#### 2 Important Steps.<br>
###### 1<sup>st</sup> Update /* javascript-file-using-the-exported-functions.js */:<br>
/* javascript-file-using-the-exported-functions.js */<br>

    import { namedFunctionOne, namedFunctionTwo } from '../modules/dom-functions.js';<br>


In `javascript-file-using-exported-functions.js`<br>
Import the functions namedFunctionOne() and namedFunctionTwo() from the module `../modules/exported-file-with-functions.js.` <br>
The modules/ folder is in the same folder as the parent folder<br>

###### 2<sup>nd</sup> The addition to the <script></script> the attribute type which is equal to 'module' <br>

    <script `type="module"` src="./javascript-fileName.js"> </script>

#### Renaming Imports to Avoid Naming Collisions
When importing resources that share names with an existing value or another imported resource.<br> 
ES6 syntax for renaming imported resources is adding keyword as:<br>

        import { exportedResource as newlyNamedResource } from '/path/to/module'

The imported function can now be used with the `new identifier newlyNamedResource` <br>

#### Default Exports and Imports
Export a single value to represent the entire module called the default export. <br>
Export an object representing the module<br>

    const resources = { 
          namedFunctionOne,
          namedFunctionTwo
        }
    export { resources as default }; 
##### OR
    export default resources;
<br>

#### Importing default values

    import importedResources from '`javascript-file-using-exported-functions.js`';
Shorthand for:<br>

    import { default as importedResources } from 'module.js
The identifier importedResources can be chosen as see fit. <br>

![image](https://github.com/nafizjiwa/JAVASCRIPT-Modules/assets/56348190/15ad47c9-99a0-4843-8f8f-b64f697947af)



    





