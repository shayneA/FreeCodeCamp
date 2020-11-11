## JavaScript Algorithms and Data Structures Projects: Cash Register

Design a cash register drawer function `checkCashRegister()` that accepts purchase price as the first argument (`price`), payment as the second argument (`cash`), and cash-in-drawer (`cid`) as the third argument.

`cid` is a 2D array listing available currency.

The `checkCashRegister()` function should always return an object with a `status` key and a `change` key.

Return `{status: "INSUFFICIENT_FUNDS", change: []}` if cash-in-drawer is less than the change due, or if you cannot return the exact change.

Return `{status: "CLOSED", change: [...]}` with cash-in-drawer as the value for the key `change` if it is equal to the change due.

Otherwise, return `{status: "OPEN", change: [...]}`, with the change due in coins and bills, sorted in highest to lowest order, as the value of the `change` key.



|    Currency Unit    |       Amount       |
| :-----------------: | :----------------: |
|        Penny        |   $0.01 (PENNY)    |
|       Nickel        |   $0.05 (NICKEL)   |
|        Dime         |    $0.1 (DIME)     |
|       Quarter       |  $0.25 (QUARTER)   |
|       Dollar        |      $1 (ONE)      |
|    Five Dollars     |     $5 (FIVE)      |
|     Ten Dollars     |     $10 (TEN)      |
|   Twenty Dollars    |    $20 (TWENTY)    |
| One-hundred Dollars | $100 (ONE HUNDRED) |



See below for an example of a cash-in-drawer array:

```js
[
  ["PENNY", 1.01],
  ["NICKEL", 2.05],
  ["DIME", 3.1],
  ["QUARTER", 4.25],
  ["ONE", 90],
  ["FIVE", 55],
  ["TEN", 20],
  ["TWENTY", 60],
  ["ONE HUNDRED", 100]
]
```

`````javascript
function checkCashRegister(price, cash, cid) {

}

checkCashRegister(19.5, 20, [["PENNY", 1.01], ["NICKEL", 2.05], ["DIME", 3.1], ["QUARTER", 4.25], ["ONE", 90], ["FIVE", 55], ["TEN", 20], ["TWENTY", 60], ["ONE HUNDRED", 100]]);

`````



#### My 1st Solution

Found solution on [Youtube](https://www.youtube.com/watch?v=f7Jv5qgMS3A) UsefulProgrammer.

`````javascript
const DENOMINATIONS = [
 ["PENNY", 1], ["NICKEL", 5], ["DIME", 10],
 ["QUARTER", 25], ["ONE", 100], ["FIVE",500],
 ["TEN", 1000], ["TWENTY", 2000], ["ONE HUNDRED", 10000]
 ]

function checkCashRegister(price, cash, cid) {

  let amountToReturn = Math.round(cash * 100) - Math.round(price * 100);
  let cashOnHand = {}
  let cashToGive = {}

  cid.forEach(cidTimesTen => {  
      cashOnHand[cidTimesTen[0]] = Math.round(cidTimesTen[1] * 100)
  })

  let index = DENOMINATIONS.length -1;

  while (index >= 0 && amountToReturn > 0) {
    let cashValue = DENOMINATIONS[index][1]
    let cashName = DENOMINATIONS[index][0]
    

    if (amountToReturn - cashValue > 0) {
       
      cashToGive[cashName] = 0
    
    while(cashOnHand[cashName] > 0 && amountToReturn - cashValue >= 0) {
       cashOnHand[cashName] -= cashValue
       cashToGive[cashName] += cashValue
       amountToReturn -= cashValue
       }
    }  
    index--
  }

    
 
  if (amountToReturn === 0){
    let isCidEmpty = true 

    Object.keys(cashOnHand).map(moneyType => {
      if (cashOnHand[moneyType] > 0) {
        isCidEmpty = false
      }
    })

    if (isCidEmpty) {
      return {status: "CLOSED", change: cid}
    }
  
  
    let changeArray = []
    Object.keys(cashToGive).map(moneyType => {
       if (cashToGive[moneyType] > 0) { 
      changeArray.push([moneyType, cashToGive[moneyType] / 100])
       }
    })
      return {status: "OPEN", change: changeArray}
  }
  return {status: "INSUFFICIENT_FUNDS", change:[] }
} 



let cid =[["PENNY", 0.5], ["NICKEL", 0], ["DIME", 0], ["QUARTER", 0], ["ONE", 0], ["FIVE", 0], ["TEN", 0], ["TWENTY", 0], ["ONE HUNDRED", 0]]

let result = checkCashRegister(19.5, 20, cid)
`````



### Explanation 

First I created an array called `DENOMINATIONS` outside of the function`checkCashRegister(...)` . I set it to the currency unit amount. e.g penny is $0.01, nickel $0.05 etc. I multiplied all the numbers by 100 as JavaScript is not good with decimal numbers. 

`````javascript
const DENOMINATIONS = [
 ["PENNY", 1], ["NICKEL", 5], ["DIME", 10],
 ["QUARTER", 25], ["ONE", 100], ["FIVE",500],
 ["TEN", 1000], ["TWENTY", 2000], ["ONE HUNDRED", 10000]
 ]
`````

Next I create 3 key variable's `amountToReturn`, `cashOnHand` and `cashToGive`. `amountToCheck` is the price minus the cash given multiplied by 100 and rounded.  

`````javascript
  let amountToReturn = Math.round(cash * 100) - Math.round(price * 100);
  let cashOnHand = {}
  let cashToGive = {}
`````

Then I set the `cashOnHand` object to the same values given in the cid(Cash-In-Draw) array multiplied by 100 and rounded. 

`````javascript
  cid.forEach(cidTimesTen => {  
      cashOnHand[cidTimesTen[0]] = Math.round(cidTimesTen[1] * 100)
  })
`````

Next is the hard part. This is where the change for the item purchased is sorted out. 

First I create a variable called `index` set it to the `DENOMINATIONS.length -1` this will be used in a while loop to get the values in the DENOMINATIONS array from highest to lowest. 

I then create a while loop. The index value will drop by 1 each loop. the while loop keeps running while the index is greater than or equal to 0 and the `amountToReturn` is greater than 0.

I then create another 2 variables called `cashValue` and `CashName`. The `cashValue` is the value of the currency unit amount. For example in the first loop it will be equal to 100 then 20 then 10 then etc. The `cashName`is the name of the amount e.g hundred dollars, twenty dollars, then dollars etc.   

`````javascript
  let index = DENOMINATIONS.length -1;

  while (index >= 0 && amountToReturn > 0) {
    let cashValue = DENOMINATIONS[index][1]
    let cashName = DENOMINATIONS[index][0]
`````

Now for the second half of the while loop I create an If statement to check if the `amountToReturn - cashValue > 0` if this is true then I give the `cashToGive`object a key value pair. The key is the `cashName` and the value is set to 0.  

Inside of the if statement I create another while loop that keeps running aslong as the `cashOnHand` is greater than 0 and aslong as `amountToReturn - CashValue >=0` amount to return minus the cash value is greater than or equal to 0. 

While this is true the `cashOnHand` at the position of `cashName` subtracted by the `cashValue`.

The `cashToGive` at the same position of `cashName` is added by `cashValue`. 

The `AmountToReturn` is then subtracted by `cashValue`. 

lastly the index is subtracted by 1 and it will keep looping while all the conditions are true. 

`````javascript
    if (amountToReturn - cashValue > 0) {

      cashToGive[cashName] = 0
           
    while(cashOnHand[cashName] > 0 && amountToReturn - cashValue >= 0) {
       cashOnHand[cashName] -= cashValue
       cashToGive[cashName] += cashValue
       amountToReturn -= cashValue
       }
    }  
    index--
  }
`````

For the final bit of code I work out the `status` key and a `change` key. 

First I check if the Cash-In-Draw(cid) is empty.

I use an if statement to check if the `amountToReturn` is equal to 0. Then I create a variable called `isCidEmpty` and set it to true. I check all of the values inside in the `cashOnHand` if they are greater than 0 I set `isCidEmpty` to false. 

I then create another if statement to check if `isCidEmpty`. if it is true then, I return and object with 2 keys. The status key holds string of `"CLOSED"` and the change key with value of cid. 

`````javascript
 if (amountToReturn === 0){
    let isCidEmpty = true 

    Object.keys(cashOnHand).map(moneyType => {

      if (cashOnHand[moneyType] > 0) {
        isCidEmpty = false
      }
    })

    if (isCidEmpty) {
      return {status: "CLOSED", change: cid}
    }
`````

For the second half of the if statement I create an variable called `changeArray` and set it to an empty array. then I add another if statement to check if the `cashToGive` is greater than 0 if it is. I add the value to the `changeArray`. It loops from highest values to lowest. Lastly I return the status "OPEN" with the change set to `changeArray`. 

`````javascript
 let changeArray = []
    Object.keys(cashToGive).map(moneyType => {
       if (cashToGive[moneyType] > 0) { 
      changeArray.push([moneyType, cashToGive[moneyType] / 100])
       }
    })
  
      return {status: "OPEN", change: changeArray}
  }
`````

Finally I return INSUFFICIENT_FUNDS if they value of `amountToReturn` is greater than 0. 

`````javascript
  return {status: "INSUFFICIENT_FUNDS", change:[] }
`````



