BROWSER COMPATIBILITY兼容性 AND TRANSPILATION
-Introduction

The reasons above imply there is a period before a software update is released when there are security vulnerabilities and unsupported language syntax.
In this lesson, you will learn about two important tools for addressing browser compatibility issues.
caniuse.com — A website that provides data on web browser compatibility for HTML, CSS, and JavaScript features. You will learn how to use it to look up ES6 feature support.
Babel — A Javascript library that you can use to convert new, unsupported JavaScript (ES6), into an older version (ES5) that is recognized by most modern browsers.
-caniuse.com I
https://caniuse.com/#home
-caniuse.com II
// Set the variable below to a number
let esFivePercentageSupport = 97;
// Set the variable below to a number
let esSixTemplateLiterals = 78;
-Why ES6?
Three reasons for the ES5 to ES6 updates are listed below:
A similarity to other programming languages — JavaScript ES6 is syntactically more similar to other object-oriented programming languages. This leads to less friction when experienced, non-JavaScript developers want to learn JavaScript.
Readability and economy of code — The new syntax is often easier to understand (more readable) and requires fewer characters to create the same functionality (economy of code).
Addresses sources of ES5 bugs — Some ES5 syntax led to common bugs. With ES6, Ecma introduced syntax that mitigates some of the most common pitfalls.
ES6
var pasta = "Spaghetti"; // ES5 syntax
const meat = "Pancetta"; // ES6 syntax
let sauce = "Eggs and cheese"; // ES6 syntax
// Template literals, like the one below, were introduced in ES6
const carbonara = `You can make carbonara with ${pasta}, ${meat}, and a sauce made with ${sauce}.`;


ES5 sample to compare those as above
var pasta = "Spaghetti"; // ES5 syntax
var meat = "Pancetta"; // ES6 syntax
var sauce = "Eggs and cheese"; // ES6 syntax
// Template literals, like the one below, were introduced in ES6
var carbonara = "You can make carbonara with " + pasta + ", " + meat + ", " + " and a sauce made with " + sauce + ".";
-Transpilation With Babel
Transpilation is the process of converting one programming language to another.

-npm init
In the last exercise, you wrote one command in your terminal to transpile ES6 code to ES5. In the next five exercises you will learn how to setup a JavaScript project that transpiles code when you run npm run build from the root directory of a JavaScript project.
The first step is to place your ES6 JavaScript file in a directory called src. From your root directory, the path to the ES6 file is ./src/main.js
The initial JavaScript project file structure is:
project
|_ src
|___ main.js
Before we install Babel, we need to setup our project to use the node package manager (npm). Developers use npm to access and manage Node packages. Node packages are directories that contain JavaScript code written by other developers. You can use these packages to reduce duplication of work and avoid bugs.
A package.json file contains information about the current JavaScript project. Some of this information includes:
Metadata — This includes a project title, description, authors, and more.
A list of node packages required for the project — If another developer wants to run your project, npm looks inside package.json and downloads the packages in this list.
Key-value pairs for command line scripts — You can use npm to run these shorthand scripts to perform some process. In a later exercise, we will add a script that runs Babel and transpiles ES6 to ES5.
After you run npm init your directory structure will contain the following files and folders:
project
|_ src
|___ main.js
|_ package.j
-Install Node Packages
To install Babel, we need to npm install two packages, babel-cli and babel-preset-env. However, npm installs over one hundred other packages that are dependencies for Babel to run properly.
We install Babel with the following two commands:
$ npm install babel-cli -D
$ npm install babel-preset-env -D
The babel-cli package includes command line Babel tools, and the babel-preset-env package has the code that maps any JavaScript feature, ES6 and above (ES6+), to ES5.
The -D flag instructs npm to add each package to a property called devDependencies in package.json. Once the project’s dependencies are listed in devDependencies, other developers can run your project without installing each package separately. Instead, they can simply run npm install — it instructs npm to look inside package.json and download all of the packages listed in devDependencies.
Once you npm install packages, you can find the Babel packages and all their dependencies in the node_modules folder. The new directory structure contains the following:
project
|_ node_modules
|___ .bin
|___ ...
|_ src
|___ main.js
|_ package.json
The ... in the file structure above is a placeholder for 100+ packages that npm installed.
-.babelrc
You can specify the initial JavaScript version inside of a file named .babelrc. In your root directory, you can run touch .babelrc to create this file.
Your project directory contains the following folders and files:
project
|_ node_modules
|___ .bin
|___ ...
|_ src
|___ main.js
|_ .babelrc
|_ package.json
Usually, you want to transpile JavaScript code from versions ES6 and later (ES6+) to ES5. From this point on, we will refer to our source code as ES6+, because Ecma introduces new syntax with each new version of JavaScript.
To specify that we are transpiling code from an ES6+ source, we have to add the following JavaScript object into .babelrc:
{
  "presets": ["env"]
}
When you run Babel, it looks in .babelrc to determine the version of the initial JavaScript file. In this case, ["env"] instructs Babel to transpile any code from versions ES6 and later.
-Babel Source Lib
...
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1"
}, …
In the code above, the "scripts" property contains an object with one property called "test". Below the "test" property, we will add a script that runs Babel like this:
...
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1",
  "build": "babel src -d lib"
}
In the "scripts" object above, we add a property called "build". The property’s value, "babel src -d lib", is a command line method that transpiles ES6+ code to ES5. Let’s consider each argument in the method call:
babel — The Babel command call responsible for transpiling code.
src — Instructs Babel to transpile all JavaScript code inside the src directory.
-d — Instructs Babel to write the transpiled code to a directory.
lib — Babel writes the transpiled code to a directory called lib.
Eg
{
  "name": "learning-babel",
  "version": "1.0.0",
  "description": "Use Babel to transpile JavaScript ES6 to ES5",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "babel-cli": "^6.26.0",
    "babel-preset-env": "^1.7.0"
   
  }
  "scripts":{
  "test"
   "build":"babel src -d lib"
}
}

-Build
"build": "babel src -d lib"
Now, we need to call "build" from the command line to transpile and write ES5 code to a directory called lib.
From the command line, we type:

npm run build
The command above runs the build script in package.json.
Babel writes the ES5 code to a file named main.js (it’s always the same name as the original file), inside of a folder called lib. The resulting directory structure is:

project
|_ lib
|___ main.js
|_ node_modules
|___ .bin
|___ ...
|_ src
|___ main.js
|_ .babelrc
|_ package.json
(eg
var pasta = "Spaghetti"; // ES5 syntax
const meat = "Pancetta"; // ES6 syntax
let sauce = "Eggs and cheese"; // ES6 syntax
// Template literals, like the one below, were introduced in ES6
const carbonara = `You can make carbonara with ${pasta}, ${meat}, and a sauce made with ${sauce}.`;
)
-Review
In this lesson, you learned about browser compatibility and transpilation. Let’s review the key concepts:
ES5 — The old JavaScript version that is supported by all modern web browsers.
ES6 — The new(er) JavaScript version that is notsupported by all modern web browsers. The syntax is more readable, similar to other programming languages, and addresses the source of common bugs in ES5.
caniuse.com — a website you can use to look up HTML, CSS, and JavaScript browser compatibility information.
Babel — A JavaScript package that transpiles JavaScript ES6+ code to ES5.
npm init — A terminal command that creates a package.json file.
package.json — A file that contains information about a JavaScript project.
npm install — A command that installs Node packages.
babel-cli — A Node package that contains command line tools for Babel.
babel-preset-env — A Node package that contains ES6+ to ES5 syntax mapping information.
.babelrc — A file that specifies the version of the JavaScript source code.
"build" script — A package.json script that you use to tranpsile ES6+ code to ES5.
npm run build — A command that runs the build script and transpiles ES6+ code to ES5.
For future reference, here is a list of the steps needed to set up a project for transpilation:
Initialize your project using npm init and create a directory called src
Install babel dependencies by running
npm install babel-cli -D
npm install babel-preset-env -D
3.Create a .babelrc file inside your project and add the following code inside it:
{
  "presets": ["env"]
}
4. Add the following script to your scripts object in package.json:
"build": "babel src -d lib"
5.Run npm run build whenever you want to transpile your code from your src to lib directories.


-New chapter JS modules
-introduction
Modules are particularly useful for a number of reasons. By separating code with similar logic into files called modules, we can:
find, fix, and debug code more easily;
reuse and recycle defined logic in different parts of our application;
keep information private and protected from other modules;
and, importantly, prevent pollution of the global namespace and potential naming collisions, by cautiously selecting variables and behavior we load into a program.
-module.exports
Eg
let Menu={};
Menu.specialty="Roasted Beet Burger with Mint Sauce";
module.exports= Menus;
Let’s consider what this code means.
let Menu = {}; creates the object that represents the module Menu. The statement contains an uppercase variable named Menu which is set equal to an object.
Menu.specialty is defined as a property of the Menu module. We add data to the Menu object by setting properties on that object and giving the properties a value.
"Roasted Beet Burger with Mint Sauce"; is the value stored in the Menu.specialty property.
module.exports = Menu; exports the Menu object as a module. module is a variable that represents the module, and exports exposes the module as an object.


The pattern we use to export modules is thus:
Define an object to represent the module.
Add data or behavior to the module.
Export the module.
Eg
let Airplane={};
Airplane.myAirplane="StarJet";
module.exports=Airplane;
-require()
To make use of the exported module and the behavior we define within it, we import the module. A common way to do this is with the require() function.
For instance, say we want the module to control the menu’s data and behavior, and we want a separate file to handle placing an order. We would create a separate file order.js and import the Menu module from menu.js to order.js using require():
In order.js we would write:
const Menu = require('./menu.js');
function placeOrder(){
  console.log('My order is:' + Menu.specialty);
}
placeOrder();
n order.js we import the module by creating a variable with const called Menu and setting it equal to the value of the require() function. We can set this variable to any variable name we like, such as menuItems.
require() is a JavaScript function that enables a module to load by passing in the module’s filepath as a parameter.
'./menu.js' is the argument we pass to the require() function.
The placeOrder() function then uses the Menumodule in its function definition. By calling Menu.specialty, we access the property specialty defined in the Menu module.
We can then invoke the function using placeOrder()
Eg
const Airplane = require('./1-airplane.js');
function displayAirplane() {
  console.log(Airplane.myAirplane);
}
displayAirplane();
//StarJet
-module.exports II
We can also wrap any collection of data and functions in an object, and export the object using module.exports. In menu.js, we could write:
let Menu={};
module.exports={
  specialty: "Roasted Beet Burger with Mint sauce",
  getSpecialty: function(){
    return this.specialty;
  } };
In the above code, notice:
module.exports exposes the current module as an object.
specialty and getSpecialty are properties on the object.
Then in order.js, we write:
const Menu=require('./menu.js');
console.log(Menu.getSpecialty());
Here we can still access the behavior in the Menumodule.
Full sample:
In the 2-airplane.js
let Airplane={};
module.exports={
  myAirplane:"CloudJet",
  displayAirplane: function(){
    return this.myAirplane;
  }
};
In the 2-missionControl.js
const Airplane=require('./2-airplane.js');
console.log(Airplane.displayAirplane());

-export default
default export and named exports
similarly to the module.exports syntax, allowing us to export one module per file.
let Menu={};
export default Menu;
Good sample
let Airplane = {};

Airplane.availableAirplanes = [
  {
  name: 'AeroJet',
  fuelCapacity: 800
 }, 
 {name: 'SkyJet',
  fuelCapacity: 500
 }  
];
-import
import Menu from './menu';
The import keyword begins the statement.
The keyword Menu here specifies the name of the variable to store the default export in.
from specifies where to load the module from.
'./menu' is the name of the module to load. When dealing with local files, it specifically refers to the name of the file without the extension of the file.
import Airplane from './airplane';

functzion displayFuelCapacity() {
  Airplane.availableAirplanes.forEach(function(element){
  console.log('Fuel Capacity of ' + element.name + ': ' + element.fuelCapacity);
  });
}

displayFuelCapacity();
//print: Fuel Capacity of AeroJet: 800
Fuel Capacity of SkyJet: 500

-Named Exports
Let’s see how this works. In menu.js we would be sure to give each piece of data a distinct variable name:
export default Airplane;
let specialty='';
function isVegetarian(){
};
function isLowSodium(){
 };
export{specialty, isVegetarian};
Notice that, when we use named exports, we are not setting the properties on an object. Each export is stored in its own variable.
specialty is a string object, while isVegetarianand isLowSodium are objects in the form of functions. Recall that in JavaScript, every function is in fact a function object.
export { specialty, isVegetarian }; exports objects by their variable names. Notice the keyword export is the prefix.
specialty and isVegetarian are exported, while isLowSodium is not exported, since it is not specified.
let availableAirplanes = [{
 name: 'AeroJet',
 fuelCapacity: 800,
 availableStaff: ['pilots', 'flightAttendants', 'engineers', 'medicalAssistance', 'sensorOperators'],
}, 
{name: 'SkyJet',
 fuelCapacity: 500,
 availableStaff: ['pilots', 'flightAttendants']
}];

let flightRequirements = {
  requiredStaff: 4,
};

function meetsStaffRequirements(availableStaff, requiredStaff) {
  if (availableStaff.length >= requiredStaff) {
    return true;
  } else {
    return false;
  }
};

export { availableAirplanes, flightRequirements, meetsStaffRequirements};
-Named Imports
import { specialty, isVegetarian } from './menu';
       console.log(specialty);
Here specialty and isVegetarian are imported.
If we did not want to import either of these variables, we could omit them from the importstatement.
We can then use these objects as in within our code. For example, we would use specialtyinstead of Menu.specialty.
import {availableAirplanes, flightRequirements, meetsStaffRequirements} from './airplane';

function displayFuelCapacity() {
  availableAirplanes.forEach(function(element) {
    console.log('Fuel Capacity of ' + element.name + ': ' + element.fuelCapacity);
  });
}

displayFuelCapacity();

function displayStaffStatus() {
  availableAirplanes.forEach(function(element) {
   console.log(element.name + ' meets staff requirements: ' + meetsStaffRequirements(element.availableStaff, flightRequirements.requiredStaff) );
  });
}

displayStaffStatus();
//print: Fuel Capacity of AeroJet: 800
Fuel Capacity of SkyJet: 500
AeroJet meets staff requirements: true
SkyJet meets staff requirements: false

-Export Named Exports
Named exports are also distinct in that they can be exported as soon as they are declared, by placing the keyword export in front of variable declarations.
export let specialty = '';
export function isVegetarian() {
}; 
function isLowSodium() {
}; 
The export keyword allows us to export objects upon declaration, as shown in export let specialty and export function isVegetarian() {}.
We no longer need an export statement at the bottom of our file, since this behavior is handled above.
export let availableAirplanes = [
{name: 'AeroJet',
 fuelCapacity: 800,
 availableStaff: ['pilots', 'flightAttendants', 'engineers', 'medicalAssistance', 'sensorOperators'],
 maxSpeed: 1200,
 minSpeed: 300
}, 
{name: 'SkyJet',
 fuelCapacity: 500,
 availableStaff: ['pilots', 'flightAttendants'],
 maxSpeed: 800,
 minSpeed: 200
}
];

export let flightRequirements = {
  requiredStaff: 4,
  requiredSpeedRange: 700
};

export function meetsStaffRequirements(availableStaff, requiredStaff) {
  if (availableStaff.length >= requiredStaff) {
    return true;
  } else {
    return false;
  }
};

export function meetsSpeedRangeRequirements(maxSpeed, minSpeed, requiredSpeedRange) {
  let range = maxSpeed - minSpeed;
  if (range > requiredSpeedRange) {
    return true;
    } else {
    return false;
  }
};

-Import Named Imports
import { specialty, isVegetarian } from 'menu';
Eg
import {availableAirplanes, flightRequirements, meetsStaffRequirements, meetsSpeedRangeRequirements} from './airplane';

function displayFuelCapacity() {
  availableAirplanes.forEach(function(element) {
    console.log('Fuel Capacity of ' + element.name + ': ' + element.fuelCapacity);
  });
}

displayFuelCapacity();

function displayStaffStatus() {
  availableAirplanes.forEach(function(element) {
   console.log(element.name + ' meets staff requirements: ' + meetsStaffRequirements(element.availableStaff, flightRequirements.requiredStaff) );
  });
}

displayStaffStatus();

function displaySpeedRangeStatus() {
  availableAirplanes.forEach(function(element) {
   console.log(element.name + ' meets speed range requirements:' + meetsSpeedRangeRequirements(element.maxSpeed, element.minSpeed, flightRequirements.requiredSpeedRange));
  });
}

displaySpeedRangeStatus();
//print: Fuel Capacity of AeroJet: 800
Fuel Capacity of SkyJet: 500
AeroJet meets staff requirements: true
SkyJet meets staff requirements: false
AeroJet meets speed range requirements:true
SkyJet meets speed range requirements:false

-Export as
Named exports also conveniently offer a way to change the name of variables when we export or import them. We can do this with the as keyword.
let specialty = '';
let isVegetarian = function() {
}; 
let isLowSodium = function() {
}; 
export { specialty as chefsSpecial, isVegetarian as isVeg, isLowSodium };
The as keyword allows us to give a variable name an alias as demonstrated in specialty as chefsSpecial and isVegetarian as isVeg.
Since we did not give isLowSodium an alias, it will maintain its original name.
Eg
let availableAirplanes = [
{name: 'AeroJet',
 fuelCapacity: 800,
 availableStaff: ['pilots', 'flightAttendants', 'engineers', 'medicalAssistance', 'sensorOperators'],
 maxSpeed: 1200,
 minSpeed: 300
}, 
{name: 'SkyJet',
 fuelCapacity: 500,
 availableStaff: ['pilots', 'flightAttendants'],
 maxSpeed: 800,
 minSpeed: 200
}
];

let flightRequirements = {
  requiredStaff: 4,
  requiredSpeedRange: 700
};

function meetsStaffRequirements(availableStaff, requiredStaff) {
  if (availableStaff.length >= requiredStaff) {
    return true;
  } else {
    return false;
  }
};

function meetsSpeedRangeRequirements(maxSpeed, minSpeed, requiredSpeedRange) {
  let range = maxSpeed - minSpeed;
  if (range > requiredSpeedRange) {
    return true;
    } else {
    return false;
  }
};

export { availableAirplanes as aircrafts, flightRequirements as flightReqs, meetsStaffRequirements as meetsStaffReqs, meetsSpeedRangeRequirements as meetsSpeedRangeReqs };
-Import as
To import named export aliases with the as keyword, we add the aliased variable in our import statement.
import { chefsSpecial, isVeg } from './menu';
We import chefsSpecial and isVeg from the Menu object.
Here, note that we have an option to alias an object that was not previously aliased when exported. For example, the isLowSodium object that we exported could be aliased with the askeyword when imported: import {isLowSodium as saltFree} from 'Menu';
Another way of using aliases is to import the entire module as an alias:
import * as Carte from './menu';
          Carte.chefsSpecial;
Carte.isVeg();
Carte.isLowSodium(); 
This allows us to import an entire module from menu.js as an alias Carte.
In this example, whatever name we exported would be available to us as properties of that module. For example, if we exported the aliases chefsSpecial and isVeg, these would be available to us. If we did not give an alias to isLowSodium, we would call it as defined on the Carte module.
import {availableAirplanes, flightRequirements, meetsStaffRequirements, meetsSpeedRangeRequirements} from './airplane';

function displayFuelCapacity() {
  availableAirplanes.forEach(function(element) {
    console.log('Fuel Capacity of ' + element['name'] + ': ' + element['fuelCapacity']);
  });
}

displayFuelCapacity();

function displayStaffStatus() {
  availableAirplanes.forEach(function(element) {
   console.log(element['name'] + ' meets staff requirements: ' + meetsStaffRequirements(element['availableStaff'], flightRequirements['requiredStaff']) );
  });
}

displayStaffStatus();

function displaySpeedRangeStatus() {
  availableAirplanes.forEach(function(element) {
   console.log(element['name'] + ' meets speed range requirements:' + meetsSpeedRangeRequirements(element['maxSpeed'], element['minSpeed'], flightRequirements['requiredSpeedRange']));
  });
}

displaySpeedRangeStatus();
You will see an error in the console, but we’ll fix this in the next exercise.
-What is import * doing?
Answer: Answer
import *, syntax: import * as name from 'path/to/moduleToExport.js';, is importing all the the named exports from the moduleToExport.js file, including the default export.
Example:
moduleToExport.js:
const myDefaultExport = {
  name: 'default export'
}

const myObj = {
  prop1: 'prop 1',
  prop2: 'prop 2'
};


export default myDefaultExport; //default export
export {myObj}; //named export

main.js:
import * as myImports from './moduleToExport.js'; //importing all named exports including default export

console.log(myImports.default); //the object `{name: "default export"}` is logged to the console
console.log(myImports.myObj); //the object `{prop1: "prop 1", prop2: "prop 2"}` is logged to the console


-Combining Export Statements
We can also use named exports and default exports together. In menu.js:

let specialty = '';
function isVegetarian() {
}; 
function isLowSodium() {
}; 
function isGlutenFree() {
};

export { specialty as chefsSpecial, isVegetarian as isVeg };
export default isGlutenFree;
Here we use the keyword export to export the named exports at the bottom of the file. Meanwhile, we export the isGlutenFree variable using the export defaultsyntax.
This would also work if we exported most of the variables as declared and exported others with the export default syntax.
export let Menu = {};
export let specialty = '';
export let isVegetarian = function() {
}; 
export let isLowSodium = function() {
}; 
let isGlutenFree = function() {
};

export default isGlutenFree;
Here we use the export keyword to export the variables upon declaration, and again export the isGlutenFree variable using the export default syntax
While it’s better to avoid combining two methods of exporting, it is useful on occasion. For example, if you suspect developers may only be interested in importing a specific function and won’t need to import the entire default export.
Sample:
export let availableAirplanes = [
{name: 'AeroJet',
 fuelCapacity: 800,
 availableStaff: ['pilots', 'flightAttendants', 'engineers', 'medicalAssistance', 'sensorOperators'],
 maxSpeed: 1200,
 minSpeed: 300
}, 
{name: 'SkyJet',
 fuelCapacity: 500,
 availableStaff: ['pilots', 'flightAttendants'],
 maxSpeed: 800,
 minSpeed: 200
}
];

export let flightRequirements = {
  requiredStaff: 4,
  requiredSpeedRange: 700
};

export function meetsStaffRequirements(availableStaff, requiredStaff) {
  if (availableStaff.length >= requiredStaff) {
    return true;
  } else {
    return false;
  }
};

export function meetsSpeedRangeRequirements(maxSpeed, minSpeed, requiredSpeedRange) {
  let range = maxSpeed - minSpeed;
  if (range > requiredSpeedRange) {
    return true;
    } else {
    return false;
  }
};

export default meetsSpeedRangeRequirements;
-Combining Import Statements
We can import the collection of objects and functions with the same data.
We can use an import keyword to import both types of variables as such:
import { specialty, isVegetarian, isLowSodium } from './menu';

import GlutenFree from './menu';
Sample
import { availableAirplanes, flightRequirements, meetsStaffRequirements} from './airplane';

import meetsSpeedRangeRequirements from './airplane';

function displayFuelCapacity() {
  availableAirplanes.forEach(function(element) {
    console.log('Fuel Capacity of ' + element.name + ': ' + element['fuelCapacity']);
  });
}

displayFuelCapacity();

function displayStaffStatus() {
  availableAirplanes.forEach(function(element) {
   console.log(element.name + ' meets staff requirements: ' + meetsStaffRequirements(element.availableStaff, flightRequirements.requiredStaff) );
  });
}

displayStaffStatus();

function displaySpeedRangeStatus() {
  availableAirplanes.forEach(function(element) {
   console.log(element.name + ' meets speed range requirements:' + meetsSpeedRangeRequirements(element.maxSpeed, element.minSpeed, flightRequirements.requiredSpeedRange));
  });
}

displaySpeedRangeStatus();
//print:Fuel Capacity of AeroJet: 800
Fuel Capacity of SkyJet: 500
AeroJet meets staff requirements: true
SkyJet meets staff requirements: false
AeroJet meets speed range requirements:true
SkyJet meets speed range requirements:false

-Review
We just learned how to use JavaScript modules. Let’s review what we learned:
Modules in JavaScript are reusable pieces of code that can be exported from one program and imported for use in another program.
module.exports exports the module for use in another program.
require() imports the module for use in the current program.
ES6 introduced a more flexible, easier syntax to export modules:
default exports use export default to export JavaScript objects, functions, and primitive data types.
named exports use the export keyword to export data in variables.
named exports can be aliased with the askeyword.
import is a keyword that imports any object, function, or data type.





 







