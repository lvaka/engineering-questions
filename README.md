# Engineering Questions
Engineering questions I've received in interviews.

## In JavaScript, how do you verify an object is an array?
I initially answered by using console.log() with typeof.  Unfortunately, arrays are objects and the type will return as an ```object```. Luckily, there is a typechecker built into JavaScript's ```Array object```.  The method is ```isArray()```   Here's an example of how that works.
```
var myArray = [];
Array.isArray(myArray) //This will return true or false depending on if myArray is an array
```

## In PHP, how would you use ```$_SESSION``` to store an authenticated user information?
As someone who mainly uses frameworks, I was stumped by this question as I wasn't sure what the optimum way to tackle this.  My first thought would be to grant a SessionID token and store it into ```$_SESSION['token']```, this is similar in how JWT's are generated server side.  Then I would authenticate the token each request before returning information through AJAX.  My main concern was the security of ```$_SESSION``` in PHP.  After doing more reading, I find that $_SESSION should be safe enough for most applications as long as I don't ```var_dump($_SESSION)```. 

So for this example, after user is authenticated, I would open a session with ```session_start();``` and then store the user information sans password into the ```$_SESSION``` ie ```$_SESSION['user'] = $user;```


## Code Challenge from SEER
```
Palindrome Index
Utilizing the compilable language of your choice - given a string, S, of lowercase letters, determine the index of the character whose removal will make S a palindrome. If S is already a palindrome or no such character exists, then print -1 . There will always be a valid solution, and any correct answer is acceptable.
Input Format
The first line contains an integer, T, denoting the number of test cases. Each line i of the T subsequent lines (where 0 < i < T) describes a test case in the form of a single string, Si.
Constraints
All characters are lowercase English letters. 1 <= T <= 20 . 1 <= |S| <= 10^5 + 5 .
Output Format
Print an integer denoting the zero-indexed position of the character that makes S not a palindrome; if S is already a palindrome or no such character exists, print -1.
As part of this exercise, please complete the following steps:
• Write code in the compilable language of your choice to complete the excercise, adhering to guidelines in the previous section
• Submit your solution via a Code REPL
```

I wrote the following code in Python3.  I optimized it further from my initial submission.  Originally, I created substrings from the entire test case with the omission of a non-matching char.  I realized that the other chars that have already been matched are unnecessary to test again, so this final code omits them.
```
class Palindrome:
  """
    Palindrome Class.  Initializes with 
    a multiline string, itterates through 
    string and prints index of letter who's
    removal would result in a palindrome.
    -1 is printed if string is already a palindrome.

      testcases - multiline string - first line is 
      number of cases.
  """

  def __init__(self, testcases):
    """Splits the test cases into a list on init."""
    test_list = testcases.split('\n')[1:]
    self.test_cases = test_list

  def is_palindrome(self, case):
    """Confirms string is palindrome."""
    front = 0
    back = len(case) - 1

    while front < back:
      head = case[front]
      tail = case[back]

      if head != tail:
        return False
      
      front += 1
      back -= 1
    
    return True

  def palindrome_outlier(self, case):
    """Iterate through string from front to back and back to front.
      When the head and tail do not match, two substrings will be 
      generated.  One starting after the char to the head until the char 
      at the tail, the other starting at the head until the char before tail.
      Each substring will be tested.  If the first substring is 
      a palindrome, method will set the head index to outlier_i and 
      break the loop.  If first substring fails the palindrome test,
      the second substring will be tested.  If the second substring 
      passes, the tail index will be set to outlier_i and the loop will 
      be broken.  In the case that both substrings fail, the loop will 
      be broken as the string cannot be turned into a palindrome with 
      the removal of a single char.

      Notes:
      There are some cases of even numbered strings can have 
      2 variations that will be palindromes with the removal of a single 
      char.  In those cases, the lowest index of the two will be returned
    """
    front = 0
    back = len(case) - 1
    outlier_i = -1

    while front < back:
      head = case[front]
      tail = case[back]

      if head != tail:
        alt_s_1 = case[front+1:back+1]
        alt_s_2 = case[front:back]
        if self.is_palindrome(alt_s_1):
          outlier_i = front
          break
        
        elif self.is_palindrome(alt_s_2):
          outlier_i = back
          break

        else:
          break
      front += 1
      back -= 1

    return outlier_i

  def print_cases(self):
    """Iterate through test cases and run palindrome_outlier."""
    for case in self.test_cases:
      outlier_i = self.palindrome_outlier(case)
      print(outlier_i)

testcases = '4\nwoop\nreiaer\ntorirot\nmoom\ntenet\nwow\np\ntolozt\narduous'

palindromes = Palindrome(testcases)
palindromes.print_cases()
```

## In React, what are the rule of Hooks? 
Only Call Hooks at the Top Level. Don’t call Hooks inside loops, conditions, or nested functions. Instead, always use Hooks at the top level of your React function. By following this rule, you ensure that Hooks are called in the same order each time a component renders. That’s what allows React to correctly preserve the state of Hooks between multiple useState and useEffect calls.  Calling a hook in a nested function creates an error.  This error is avoided if you make sure a hook is only called within a React function.
