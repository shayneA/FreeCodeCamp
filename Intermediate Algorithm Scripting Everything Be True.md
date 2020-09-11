## Intermediate Algorithm Scripting: Everything Be True

Check if the predicate (second argument) is truthy on all elements of a collection (first argument).

In other words, you are given an array collection of objects. The predicate `pre` will be an object property and you need to return `true` if its value is `truthy`. Otherwise, return `false`.

In JavaScript, `truthy` values are values that translate to `true` when evaluated in a Boolean context.

Remember, you can access object properties through either dot notation or `[]` notation.

`````javascript
function truthCheck(collection, pre) {  return pre;  }

truthCheck([{"user": "Tinky-Winky", "sex": "male"}, {"user": "Dipsy", "sex": "male"}, {"user": "Laa-Laa", "sex": "female"}, {"user": "Po", "sex": "female"}], "sex");
`````

#### My solution 

`````javascript
function truthCheck(collection, pre) {

let trueCount = 0

  for (let i = 0; i < collection.length; i++) {
    if (collection[i].hasOwnProperty(pre) && collection[i][pre]){
      trueCount++
    }
  }
return trueCount === collection.length
}

let result = truthCheck([{"name": "Pete", "onBoat": true}, {"name": "Repeat", "onBoat": true, "alias": "Repete"}, {"name": "FastForward", "onBoat": true}], "onBoat")
console.log(result) // True

let result2 = truthCheck([{"user": "Tinky-Winky", "sex": "male", "age": 0}, {"user": "Dipsy", "sex": "male", "age": 3}, {"user": "Laa-Laa", "sex": "female", "age": 5}, {"user": "Po", "sex": "female", "age": 4}], "age") 
console.log(result2) // False
`````

- First I create a trueCount variable to check how many cases are actually true.
- Then I use a for loop with an If statement to check each object inside the collections array. For the trueCount to increase, the collection object must have the property of pre `collection[i].hasOwnProperty(pre)` and the value at `collection[i][pre]` must be truthy.  
- Outside the loop, I check to see if the trueCount variable has the same value as the length of **collection**, if true then return **true**, otherwise, return **false**