## Intermediate Algorithm Scripting: Steamroller

Flatten a nested array. You must account for varying levels of nesting.

`````javascript
function steamrollArray(arr) {
  return arr;
}
steamrollArray([1, [2], [3, [[4]]]]); // [ 1, [ 2 ], [ 3, [ [Object] ] ] ]
`````

#### My solution 

`````javascript
function steamrollArray(arr) {
  
  let arrays = [...arr]
  let newArr = []

  while(arrays.length){
    let next = arrays.pop()
    if (Array.isArray(next)){
      arrays.push(...next)
    } else {
      newArr.unshift(next)
    }
  }
  return newArr
}
let result = steamrollArray([1, [2], [3, [[4]]]]);
console.log(result) // [ 1, 2, 3, 4 ]
`````

1. This is a simple solution. First, I create an arrays variable and set it to arr using the spread operator `[...arr]`.   This allows me to edit the array without modifying the original array inputted. 
2. Then, I create an newArr variable, set it to an empty array to be returned with the data inside the nested arr later. 
3. Next, I use a while loop that keeps running while arrays.length is over 1.
4. Inside the while loop I create a variable called next it's used each loop, I use .pop or the arrays variable to break off a layer and give it to the variable next.
5. An If statement is used to check if the next variable is just an empty array or does it have another data type inside, If there is no data the next array next array loses a layer of brackets. If there is an sting, number etc, then the data is pushed into the newArr array using .unshift(). If push() is used then it will be in reverse order. 
6. This keeps looping while arrays variable still has a length greater than 1. 



#### Best solution

``````javascript
function steamrollArray(arr) {
  return arr.flat(Infinity);
}
let result = steamrollArray([1, [2], [3, [[4]]]]);
console.log(result) // [ 1, 2, 3, 4 ] 
``````

