## Intermediate Algorithm Scripting: Make a Person

Fill in the object constructor with the following methods below:

`````javascript
getFirstName()
getLastName()
getFullName()
setFirstName(first)
setLastName(last)
setFullName(firstAndLast)
`````

Run the tests to see the expected output for each method. The methods that take an argument must accept only one argument and it has to be a string. These methods must be the only available means of interacting with the object.

`````javascript
var Person = function(firstAndLast) {
  // Only change code below this line
  // Complete the method below and implement the others similarly
  this.getFullName = function() {
    return "";
  };
  return firstAndLast;
};

var bob = new Person('Bob Ross');
bob.getFullName();
`````



#### My solution 



`````javascript
var Person = function(firstAndLast) {

  this.getFullName = function() {
    return firstAndLast;
  };

  this.getFirstName = function(){
    let first = (firstAndLast.match(/\w+/))
    return first[0]
  };

  this.getLastName = function(){
    let last = (firstAndLast.match(/\s\w+/))
    return last[0].trim()
  }

  this.setFullName = function(newfirstAndLast){
    firstAndLast = newfirstAndLast;
    return firstAndLast 
  }

  this.setFirstName = function(first){
    let replaceFirst = firstAndLast.replace(/\w+/, first)
    firstAndLast = replaceFirst.trim()
    return replaceFirst.trim()
  }

  this.setLastName = function(last){
     let replaceLast = firstAndLast.replace(/\s\w+/, " "+ last)
     firstAndLast = replaceLast
    return replaceLast
  }
}; 

var bob = new Person('Bob Ross');

let result = bob.setLastName("Marley");   
console.log(result) // Bob Marley
`````

For this challenge I have to give the object constructor 6 method (aka functions). 

<u>How I coded each method.</u> 

`getFullName()` was simple to complete all I done with return the input given. 

`getLastName()` To complete this I used regex method `.match(/\s\w+/)` to match all words together starting with a space.  

`getFirstName()`To complete this I used regex method `.match(/\w+/)` to match all words together until a space.    

`setFirstName(first)` I used `.replace()` to change the string with same regex as `getFirstName` to find the first name and then set the `firstAndLast` parameter to the `replaceFirst.trim()`, The `.trim()` is used to get rid of whitespace. 

`setLastName(last)` I used .`replace()` again and used the same regex as the last name. then I set `firstAndLast` to the updated version and I add a space as the replace returns both words joined without space. `firstAndLast.replace(/\s\w+/, " "+ last)`

`setFullName(firstAndLast)` This was very simple I just set `firstAndLast` to the inputted text and returned it. 