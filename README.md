# Engineering Questions
Engineering questions I couldn't answer on the spot.

## In JavaScript, how do you verify an object is an array?
I initially answered by using console.log() with typeof.  Unfortunately, arrays are objects and the type will return as an ```object```. Luckily, there is a typechecker built into JavaScript's ```Array object```.  The method is ```isArray()```   Here's an example of how that works.
```
var myArray = [];
Array.isArray(myArray) //This will return true or false depending on if myArray is an array
```

## In PHP, how would you use ```$_SESSION``` to store an authenticated user information?
As someone who mainly uses frameworks, I was stumped by this question as I wasn't sure what the optimum way to tackle this.  My first thought would be to grant a SessionID token and store it into ```$_SESSION['token']```, this is similar in how JWT's are generated server side.  Then I would authenticate the token each request before returning information through AJAX.  My main concern was the security of ```$_SESSION``` in PHP.  After doing more reading, I find that $_SESSION should be safe enough for most applications as long as I don't ```var_dump($_SESSION)```. 

So for this example, after user is authenticated, I would open a session with ```session_start();``` and then store the user information sans password into the ```$_SESSION``` ie ```$_SESSION['user'] = $user;```
