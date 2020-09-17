## Intermediate Algorithm Scripting: Map the Debris

Return a new array that transforms the elements' average altitude into their orbital periods (in seconds).

The array will contain objects in the format `{name: 'name', avgAlt: avgAlt}`.

You can read about orbital periods [on Wikipedia](http://en.wikipedia.org/wiki/Orbital_period).

The values should be rounded to the nearest whole number. The body being orbited is Earth.

The radius of the earth is 6367.4447 kilometers, and the GM value of earth is 398600.4418 km3s-2.

`````javascript
function orbitalPeriod(arr) {
  var GM = 398600.4418;
  var earthRadius = 6367.4447;
  return arr;   
}
orbitalPeriod([{name: "iss", avgAlt: 413.6}, {name: "hubble", avgAlt: 556.7}, {name: "moon", avgAlt: 378632.553}])

//  should return  //

[{name : "iss", orbitalPeriod: 5557}, {name: "hubble", orbitalPeriod: 5734}, {name: "moon", orbitalPeriod: 2377399}]
`````



#### My solution 

`````javascript
function orbitalPeriod(arr) {
  var GM = 398600.4418;
  var earthRadius = 6367.4447;

  let   orbitialPeriodResultArray  = []

for (let i = 0; i < arr.length; i++){
 
    orbitialPeriodResultArray .push({name:"0", orbitalPeriod:0})
    orbitialPeriodResultArray[i].name = arr[i].name

    let twoTimesPie = Math.PI * 2
    let earthRadiusPlusAvgAltCube = Math.pow(earthRadius + arr[i].avgAlt,3)
    let numToSquare = earthRadiusPlusAvgAltCube / GM

    let squaredResult = Math.sqrt(numToSquare)
    let numToRound = twoTimesPie * squaredResult

    let result = Math.round(numToRound)

    orbitialPeriodResultArray[i].orbitalPeriod = result
}
  return orbitialPeriodResultArray;
}

let result = orbitalPeriod([{name: "iss", avgAlt: 413.6},
              {name: "hubble", avgAlt: 556.7}, 
              {name: "moon", avgAlt: 378632.553}])
console.log(result) // [{name : "iss", orbitalPeriod: 5557}, {name: "hubble", orbitalPeriod: 5734}, {name: "moon", orbitalPeriod: 2377399}]
`````

  The Math equation used to to get the orbital Period is According to [Kepler's Third Law](https://en.wikipedia.org/wiki/Kepler's_laws_of_planetary_motion). 
$$
2n \sqrt \frac{a^3}{μ}
$$
the  *T* (in seconds) of two point masses orbiting each other in a circular or [elliptic orbit](https://en.wikipedia.org/wiki/Elliptic_orbit) is:[[2\]](https://en.wikipedia.org/wiki/Orbital_period#cite_note-FOOTNOTEBateMuellerWhite197133-2)

where:

- *a* is the orbit's [semi-major axis](https://en.wikipedia.org/wiki/Semi-major_axis),
- μ =  *GM* is the [standard gravitational parameter](https://en.wikipedia.org/wiki/Standard_gravitational_parameter),
- *G* is the [gravitational constant](https://en.wikipedia.org/wiki/Gravitational_constant),
- *M* is the mass of the more massive body.
- For all ellipses with a given semi-major axis the orbital period is the same, regardless of eccentricity.



The above equation needs to be translated for the parameters in this challenge. I could not figure this out I found the answer at [Useful Programmer YT video](https://www.youtube.com/watch?v=37NSow_KFBE)   
$$
orbitialPeriod = 2n \sqrt \frac{earthRadius+avgAlt^3}{GM}
$$
This in simple maths is: 

1. earthRadius + avgAlt cubed (multiplied by itself 3 times).
2. The earthRadius+avgAlt cubed is then divided by GM.
3. Lastly, it is squared and multiplied by Pi * 2 to get the result.



##### <u>The code I used to complete this</u> 

First I created an empty array called orbitialPeriodResultArray. This is going to be the array returned at the end. 

Next, I used a for loop to iterate though all objects passed into the function, and to repeat the mathematical operations on all the objects passed in.  

I use `.push()` to add an object to the orbitialPeriodResultArray, I give the objects 2 keys: name and orbitialPeriod. I then I give them values just as placeholders to be changed later. 

I then use bracket notation to change the orbitialPeriodResultArray name value to the same as the one passed in.  `orbitialPeriodResultArray[i].name = arr[i].name`

Next I do the maths explained above: 

`````javascript
    let twoTimesPie = Math.PI * 2
    let earthRadiusPlusAvgAltCube = Math.pow(earthRadius + arr[i].avgAlt,3)
    let numToSquare = earthRadiusPlusAvgAltCube / GM

    let squaredResult = Math.sqrt(numToSquare)
    let numToRound = twoTimesPie * squaredResult

    let result = Math.round(numToRound)

    orbitialPeriodResultArray[i].orbitalPeriod = result
`````

The names are self explanatory.

Lastly, I return the orbitialPeriodResultArray and this will loop over for each object in the array passed in. 

`````javascript
let result = orbitalPeriod([{name: "iss", avgAlt: 413.6},
              {name: "hubble", avgAlt: 556.7}, 
              {name: "moon", avgAlt: 378632.553}])
console.log(result)/*
[ { name: 'iss', orbitalPeriod: 5557 },
  { name: 'hubble', orbitalPeriod: 5734 },
  { name: 'moon', orbitalPeriod: 2377399 } ] */ 
`````



























