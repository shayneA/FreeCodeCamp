## JavaScript Algorithms and Data Structures Projects: Telephone Number Validator

Return `true` if the passed string looks like a valid US phone number.

The user may fill out the form field any way they choose as long as it has the format of a valid US number. The following are examples of valid formats for US numbers (refer to the tests below for other variants):



> 555-555-5555
> (555)555-5555
> (555) 555-5555
> 555 555 5555
> 5555555555
> 1 555 555 5555



For this challenge you will be presented with a string such as `800-692-7753` or `8oo-six427676;laskdjf`. Your job is to validate or reject the US phone number based on any combination of the formats provided above. The area code is required. If the country code is provided, you must confirm that the country code is `1`. Return `true` if the string is a valid US phone number; otherwise return `false`.

#### My solution 

`````javascript
function telephoneCheck(str) {

    let count = str.length
    let digitCount = 0
    let parenthesesCount = 0

    while (count >= 0) {
        if (/[0-9]/g.test(str[count])) {
            digitCount++
        }
        if (/[()]/g.test(str[count])) {
            parenthesesCount++
        }
        if (/[()]/g.test(str[count]) && count >= 7) {
            return false
        }
        count--
    }

    if (parenthesesCount == 1 || parenthesesCount > 2) {
        return false
    }

    if (digitCount === 11 && str[0] === "1") {
        return true
    } else if (digitCount === 10) {
        return true
    } else {
        return false
    }
}

let result = telephoneCheck("1 (555)-555-5555");
`````

For my solution, I used if statements to check different conditions. This passes the test however its not good enough to be put in production. 

First I create 3 variables, count which is set to the inputted strings length. digitCount to check the amount of numbers passed in and parenthesesCount to count the parentheses.

I use a while loop and set it to run while count is equal to or greater than 0, each loop count losses 1 from its original value of `str.length`.  

Next I use an if statement to check if there are any numbers in the sting at position count that is 0-9. I used regex to check the range form 0-9. If there is than digitCount is increased by 1. 

I then use similar code to check the parentheses and add to parenthesesCount.

Lastly, I check if there are any parentheses that come after position 6 if there are I return false and code ends. 

Then I use another if statement to check if the parentheses Coun is equal to 1 or greater than 2 if they are I return false and code ends. 

The last if statement chain I check the digitCount to see if there are 11 digits and if the first is equal to`"1"`, if they are I return true. If there is 10 digits return True and for anything else return false. 

#### Better solution

`````javascript
function telephoneCheck(str) {
  var regex = /^(1\s?)?(\(\d{3}\)|\d{3})[\s\-]?\d{3}[\s\-]?\d{4}$/;
  return regex.test(str);
}
telephoneCheck("555-555-5555");
`````

This solution is pure regex with a test to get the boolean value. 

#### Code Explanation

- `^` denotes the beginning of the string.
- `(1\s?)?` allows for “1” or "1 " if there is one.
- `\d{n}` checks for exactly n number of digits so `\d{3}` checks for three digits.
- `x|y` checks for either x OR y so `(\(\d{3}\)|\d{3})` checks for either three digits surrounded by parentheses, or three digits by themselves with no parentheses.
- `[\s\-]?` checks for spaces or dashes between the groups of digits.
- `$` denotes the end of the string. In this case the beginning `^` and end of the string `$` are used in the regex to prevent it from matching any longer string that might contain a valid phone number (eg. “s 555 555 5555 3”).
- Lastly we use `regex.test(str)` to test if the string adheres to the regular expression, it returns `true` or `false`.

