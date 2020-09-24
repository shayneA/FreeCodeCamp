## JavaScript Algorithms and Data Structures Projects: Caesars Cipher

One of the simplest and most widely known ciphers is a Caesar cipher, also known as a shift cipher. In a shift cipher the meanings of the letters are shifted by some set amount.

A common modern use is the [ROT13](https://en.wikipedia.org/wiki/ROT13) cipher, where the values of the letters are shifted by 13 places. Thus 'A' ↔ 'N', 'B' ↔ 'O' and so on.

Write a function which takes a [ROT13](https://en.wikipedia.org/wiki/ROT13) encoded string as input and returns a decoded string.

All letters will be uppercase. Do not transform any non-alphabetic character (i.e. spaces, punctuation), but do pass them on.

#### My solution 

`````javascript
function rot13(str) {

  let decoded = ""

  for (let i = 0; i < str.length; i++){
    
    let tempIndex = str.charCodeAt(i)

    if (tempIndex >= 65 && tempIndex <= 77){
       decoded += String.fromCharCode(tempIndex + 13)
    } else if (tempIndex >= 78 && tempIndex <= 90) {
       decoded += String.fromCharCode(tempIndex -13)
    } else { 
       decoded += String.fromCharCode(tempIndex)
    }
  }
  return decoded
}

let result = rot13("SERR PBQR PNZC")
console.log(result) // FREE CODE CAMP
`````

To complete this I used `.charCodeAt()` and `fromCharCode()` to complete this challenge. 



first I create an array called decoded. This is where I place the decoded characters and what I will return last. 

Next, I use a for loop to loop over all characters passed into the string. 

Inside the for loop I create a variable called `tempIndex` this will be the temporary index of every individual letter.  

Then I use an if statement to check if the tempIndex and see if it's Unicode is within the range 65 to 90.

If the Unicode value is greater than or equal to 65 but less than or equal to 77 then the univode value is skipped 13 letter and that letter is placed in the decoded sting. 

If the Unicode value is greater than or equal to 78 and less than or equal to 90 then the Unicode value is rediced by 13 and the letter is placed in the decoded sting. 

else the character is added to the decoded sting with no changes. 

