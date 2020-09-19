## JavaScript Algorithms and Data Structures Projects: Palindrome Checker

Return `true` if the given string is a palindrome. Otherwise, return `false`.

A palindrome is a word or sentence that's spelled the same way both forward and backward, ignoring punctuation, case, and spacing.

**Note**
You'll need to remove **all non-alphanumeric characters** (punctuation, spaces and symbols) and turn everything into the same case (lower or upper case) in order to check for palindromes.

We'll pass strings with varying formats, such as `"racecar"`, `"RaceCar"`, and `"race CAR"` among others.

We'll also pass strings with special symbols, such as `"2A3*3a2"`, `"2A3 3a2"`, and `"2_A3*3#A2"`.



#### My solution 



``````javascript
function palindrome(str) {

str = str.replace(/[\W_]+/gi,"").toLowerCase();
str = str.split("")

let strreversed = [...str]
strreversed.reverse()

let truecount = 0

for (let i = 0; i < str.length; i++){
str[i] === strreversed[i] ? truecount++ : false
  }

  return truecount === str.length ? true : false 
}

let result = palindrome("1234")
console.log(result)
``````

First, I use `.replace()` to replace all non-alphanumeric characters with empty string `""` and I set all characters to lowercase. 

next I change the string into and array split but each character using `.split("")`. 

Then I create a variable called strreversed to be the reversed string. 

I create a truecount variable to be used later in a loop. 

I use a for loop to check every element inside the array and use the ternary operator to check if the first element in are array is equal to the reversed string. If they are the same element then the truecount is increased by 1 for each element if not nothing happens. 

lastly, I return a Boolean value. I check if truecount is equal to the length of the string if it is that the input is a palindrome if its false than it is not a palindrome. 