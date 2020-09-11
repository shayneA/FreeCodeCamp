## Intermediate Algorithm Scripting: Binary Agents

Return an English translated sentence of the passed binary string.

The binary string will be space separated.

`````javascript
function binaryAgent(str) {
  return str;
}
binaryAgent("01000001 01110010 01100101 01101110 00100111 01110100 00100000 01100010 01101111 01101110 01100110 01101001 01110010 01100101 01110011 00100000 01100110 01110101 01101110 00100001 00111111");
`````



#### My solution

`````javascript
function binaryAgent(str) {

  let strArr = str.split(" ")
  let newArr = []
  for (let i = 0; i < strArr.length; i++){
    newArr.push(String.fromCharCode(parseInt(strArr[i],2)))
  }

  return newArr.join("")
}

let result = binaryAgent("01000001 01110010 01100101 01101110 00100111 01110100 00100000 01100010 01101111 01101110 01100110 01101001 01110010 01100101 01110011 00100000 01100110 01110101 01101110 00111111 10111111");
console.log(result) //  Aren't bonfires fun?¿
`````

1. Separate the string into an array of strings separated by whitespace using `.split(" ")` .
2. Create some variables that are used along the way - the names are self explanatory for the most part.
3. Iterate through each binary string in the new array using a for loop.
4. Convert to decimal by using `parseInt(StrArr, 2)`. Use the second parameter to specify the base of the input numbers.
5. At the end, return the converted message using `.join("")`. 

Relevant link: [parseInt](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt) 

#### Best solution 

`````javascript
const binaryAgent = str => str.replace(/\d+./g, char => String.fromCharCode(`0b${char}`));
       
binaryAgent("01000001 01110010 01100101 01101110 00100111 01110100 00100000 01100010 01101111 01101110 01100110 01101001 01110010 01100101 01110011 00100000 01100110 01110101 01101110 00100001 00111111");
`````

#### Code Explanation

- Find all groups of one or more digits followed by one other character
- Replace with a string created from the specified sequence of UTF-16 code units
- Use `0b` to lead the code unit to express that a binary integer literal is being converted.

#### Relevant Links

- [String.fromCharCode()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/fromCharCode)
- [String.prototype.replace()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replace)
- [Convert a string of binary characters to the ASCII equivalents](https://codegolf.stackexchange.com/questions/35096/convert-a-string-of-binary-characters-to-the-ascii-equivalents)
- [Grammar and types/Numeric Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#Numeric_literals)