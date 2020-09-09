## Intermediate Algorithm Scripting: Drop it

Given the array `arr`, iterate through and remove each element starting from the first element (the 0 index) until the function `func` returns `true` when the iterated element is passed through it.

Then return the rest of the array once the condition is satisfied, otherwise, `arr` should be returned as an empty array.

`````javascript
function dropElements(arr, func) {
return arr; }
dropElements([1, 2, 3], function(n) {return n < 3; }); 
`````

### My solution 

`````javascript
function dropElements(arr, func) {

  let newarr = []
  for (let i = 0; i < arr.length; i++){ 
    if(func(arr[i])) {
      newarr.push(...arr.splice(i))
    }
    
  }
  return newarr;
}

let result = dropElements([0, 1, 0, 1], function(n) {return n === 1;});
console.log(result) 
`````

First I create a newarr variable and set it to an empty array to be returned later.

Next, I use a for loop to check every element inside of the array given and then I use an if statement to check if the element will pass the function given, if it meets the conditions then it is pushed into the empty array. If no conditions are met then the empty array will be returned.

