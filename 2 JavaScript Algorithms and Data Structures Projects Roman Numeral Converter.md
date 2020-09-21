## JavaScript Algorithms and Data Structures Projects: Roman Numeral Converter

Convert the given number into a roman numeral.

All [roman numerals](http://www.mathsisfun.com/roman-numerals.html) answers should be provided in upper-case.

#### Solution 

`````javascript
function convertToRoman(num) {
    
  let convertedNum = ""
  
  let romanNumObj = {
    "M": 1000, 
    "CM": 900,
    "D":  500,
    "CD": 400,
    "C":  100,
    "XC": 90,
    "L":  50,
    "XL": 40,
    "X":  10,
    "IX": 9,
    "V":  5,
    "IV": 4,
    "I":  1
  }

  for (let key in romanNumObj){
  while (romanNumObj[key] <= num) {
    convertedNum += key
    num -= romanNumObj[key]
      }
  }

 return convertedNum;
}

let result = convertToRoman(101);
console.log(result) // CI
`````

This is a very simple solution. 

First I create a variable called convertedNum and set it to an emtpy string later it will be the returned reman numerals. 

Next I create an object to hold the roman numerals and its values. The values are the equivalent with Arabic numerals.(digits 1 to 9 + 0). 

I use a for in loop to loop though the object. A while loop is placed inside the for in loop. The while loop keeps running while the number inserted is greater than or equal to the number values in the romanNumObj.

When a number that is equal to or greater than the numbers in the object. the roman symbol is added into the convertedNum string and the value is taken away from num. 

For this example. 101 is inputted the number the number is tested against 1000, 900, 500, 400 etc. until the inputted number is greater than or equal to the object value. For this example it will be equal to 100 so the key "C" will be added to the convertedNum and 100 will be taken away from num. The loop will keep running as num is greater than 1. same process "I" is added to convertedNum and value is taken away, as the num is now less than all values in the object the loop will end. 