# Engineering Questions
Engineering questions I couldn't answer on the spot.

## In JavaScript, how do you verify an object is an array?
I initially answered by using console.log() with typeof.  Unfortunately, arrays are objects and the type will return as an ```object```. Luckily, there is a typechecker built into JavaScript's ```Array object```.  The method is ```isArray()```   Here's an example of how that works.
```
var myArray = [];
Array.isArray(myArray) //This will return true or false depending on if myArray is an array
```
