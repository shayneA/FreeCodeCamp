## Intermediate Algorithm Scripting: Arguments Optional

Create a function that sums two arguments together. If only one argument is provided, then return a function that expects one argument and returns the sum.

For example, `addTogether(2, 3)` should return `5`, and `addTogether(2)` should return a function.

Calling this returned function with a single argument will then return the sum:

```
var sumTwoAnd = addTogether(2);
```

`sumTwoAnd(3)` returns `5`.

If either argument isn't a valid number, return undefined.

`````javascript
function addTogether() {
  return false;
}
addTogether(2,3);
`````



#### My solution  

`````javascript
function addTogether() {

if (typeof(arguments[0]) === "number" && arguments.length === 1){
  let onlyArg = arguments[0]
  return function(args2) {
      if(typeof(onlyArg) === "number" && typeof(args2) === "number"){
        return onlyArg + args2
      }
    return undefined
  }
}

let newArr = []
  for (let i = 0; i < arguments.length; i++) {
  if (typeof(arguments[i]) === "number"){
    newArr.push(arguments[i])
   } else
    return undefined
  }
 return newArr.reduce((a,b)=> a+b)
}

let result = addTogether(2,3)
console.log(result) // 5 
`````

The structure of the code is very important, the first if statement I check if the argument passed in the parameter is an number and I check if it has the length of 1. If it meets both conditions I save the value passed in and return another function which expects another argument to be inputted. Then that functions checks both arguments are numbers, if they are they are added and returned. If the conditions are not met then undefined is returned. 

If there are 2 arguments passed in I check if they are numbers and if they are they are added together. 



- I use if statements to check the arguments passed in the function are numbers if they are they are added if not then undefined is returned. 
- I use `typeof()` to test if the argument is a number and the `&&` and operator test both conditions. 
- I create a newArr for when 2 arguments are passed in they are all added to and array and `.reduce()` is used to added them together and remove the array container. 