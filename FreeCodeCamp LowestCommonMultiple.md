## Intermediate Algorithm Scripting: Smallest Common Multiple

- Find the smallest common multiple of the provided parameters that can be evenly divided by both, as well as by all sequential numbers in the range between these parameters.

- The range will be an array of two numbers that will not necessarily be in numerical order.

- For example, if given 1 and 3, find the smallest common multiple of both 1 and 3 that is also evenly divisible by all numbers *between* 1 and 3. The answer here would be 6.


````javascript
function smallestCommons(arr) { 
  return arr;
}
smallestCommons([1,5]);

````



### My 1st solution  



`````javascript
function smallestCommons(arr) {
// Getting the Lowest and highest Values in Array
  let smallNum = Math.min(...arr)
  let bigNum = Math.max(...arr)
  
// creating a mutiples variable to be used in for Loop
  let mutiples = 0
// create range variable to get the range in Array
  let range = getRange(smallNum, bigNum)

// For loop to get common multiples
  for (let i = 1; i < 100000; i++){
    mutiples = (smallNum * i) * bigNum;
    
    let truecount = 0
    // loop winthin a loop to check common multiples against 
    // numbers in the range array & see if it is evenly divisible
    for (let j = 0; j < range.length; j++){
      if (mutiples % range[j] ===0){
        truecount++
      } 
    }
   // finds the lowest common multiple and returns it
    if (truecount === range.length){
    return mutiples
    } 

  }

  // A function to get the Range of between highest num and lowest 
  function getRange(lowN, highN){
    let resultRanage = []
    while (lowN <= highN){
      resultRanage.push(lowN)
      lowN++
    }
    return resultRanage
  }

// loop has a limit of iterates 100000 times.
  return "passed 100000 iterations";
}



smallestCommons([1,5]);

`````

My solution is one of the simplest ways to complete this challenge, it can pass this challenge but is not good enough to be used for anything else as there is a limit on how big numbers can be and the process to find the answer is not efficient. 

First I find the lowest and highest number in the array given and set them to the smallNum & BigNum. 

  `let smallNum = Math.min(...arr)`
  `let bigNum = Math.max(...arr)`

next I create a multiples variable to be used later in a loop to get the answer, this will be a common multiple between all numbers in the range from biggest to smallest number.   

`let mutiples = 0` 

I create a range variable that hold a function that creates an array of all numbers from smallNum to BigNum. 

`let range = getRange(smallNum, bigNum)` 

next I use the multiples variable and set it to a common multiple between smallNum and BigNum and the value of i.

This is where the limit on the code is it will only find common multiples 100000 times. 

  `for (let i = 1; i < 100000; i++){`
    `mutiples = (smallNum * i) * bigNum;`

Now, I test the common multiples to see if they are evenly divisible by all numbers in the range array, I create another for loop inside the previous for loop to test if the common multiple held inside the multiples variable is divisible by all numbers in the range array. 

`let truecount = 0`

​    ``for (let j = 0; j < range.length; j++){`
​      `if (mutiples % range[j] ===0){`
​        `truecount++   }  }` 
​    

I needed to create a truecount variable to check if the common multiple is divisible by all numbers in the range array. I set it to 0(zero) outside of the range for loop so it resets after checking all numbers in range array. 

    if (truecount === range.length){
    return mutiples
    } 
This is the range variables function: 

  `function getRange(lowN, highN){`
    `let resultRanage = []`
    `while (lowN <= highN){`
      `resultRanage.push(lowN)`
      `lowN++`  `}`
    `return resultRanage` ` }`

 lastly, I added a final return in case a number too big is entered.

`return "passed 100000 iterations";   } `

`smallestCommons([1,5]); `