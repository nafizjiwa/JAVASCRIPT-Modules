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

Every JavaScript file that runs in a Node environment is treated as a distinct module<br>
The functions and data defined within each module can be used by any other module, as long as those resources are properly exported and imported.<br>
When a program is executed in the Node environment, process.argv is an array holding the arguments provided.<br>
Creating a module that exports a function which is used by many other modules would solve the problem of having to write the same code in each of the other files.<br>

##### module.exports



