JS - Coding questions 2

# 1. Give an example where call apply bind is. required?
=> Call
```js
var person1 = {firstName: 'Jon', lastName: 'Kuperman'};
var person2 = {firstName: 'Kelly', lastName: 'King'};

function say(greeting) {
    console.log(greeting + ' ' + this.firstName + ' ' + this.lastName);
}

say.call(person1, 'Hello'); // Hello Jon Kuperman
say.call(person2, 'Hello'); // Hello Kelly King
```
Apply
```js
var person1 = {firstName: 'Jon', lastName: 'Kuperman'};
var person2 = {firstName: 'Kelly', lastName: 'King'};

function say(greeting) {
    console.log(greeting + ' ' + this.firstName + ' ' + this.lastName);
}

say.apply(person1, ['Hello']); // Hello Jon Kuperman
say.apply(person2, ['Hello']); // Hello Kelly King
```
Bind
```js
var person1 = {firstName: 'Jon', lastName: 'Kuperman'};
var person2 = {firstName: 'Kelly', lastName: 'King'};

function say() {
    console.log('Hello ' + this.firstName + ' ' + this.lastName);
}

var sayHelloJon = say.bind(person1);
var sayHelloKelly = say.bind(person2);

sayHelloJon(); // Hello Jon Kuperman
sayHelloKelly(); // Hello Kelly King
```

# 2. What is the difference between readFile and readFileSync?
=> readFileSync() is synchronous and blocks execution until finished. These return their results as return values. readFile() are asynchronous and return immediately while they function in the background. You pass a callback function which gets called when they finish.

```js
var fs = require('fs');
fs.readFile(filename, "utf8", function(err, data) {
        if (err) throw err;
        console.log(data);
});
```
```js
var fs = require('fs');
function readFileAsSync(){
    new Promise((resolve, reject)=>{
        fs.readFile(filename, "utf8", function(err, data) {
                if (err) throw err;
                resolve(data);
        });
    });
}

async function callRead(){
    let data = await readFileAsSync();
    console.log(data);
}

callRead();
```
```js
'use strict'
var fs = require("fs");

/***
 * implementation of readFileSync
 */
var data = fs.readFileSync('input.txt');
console.log(data.toString());
console.log("Program Ended");

/***
 * implementation of readFile 
 */
fs.readFile('input.txt', function (err, data) {
    if (err) return console.error(err);
   console.log(data.toString());
});

console.log("Program Ended");
```

# 3. What does process in node.js mean?
=> The process object in Node. js is a global object that can be accessed inside any module without requiring it. There are very few global objects or properties provided in Node. js and process is one of them. It is an essential component in the Node.
```js
// Including the module into out project
var process = require('process');
  
// It will return the current working directory
console.log('this is the working directory --> ' + process.cwd());
  
// It will return the version of process we are using
console.log('this is the process version --> ' + process.version);
  
// It will return the type of OS we are using at that time.
console.log('current OS we are using --> ' + process.platform);
```

# 4. Explain what node.js is?
=>  - Node.js is an open source server environment
    - Node.js is free
    - Node.js runs on various platforms (Windows, Linux, Unix, - Mac OS X, etc.)
    - Node.js uses JavaScript on the server


=> Node. js (Node) is an open source development platform for executing JavaScript code server-side. Node is useful for developing applications that require a persistent connection from the browser to the server and is often used for real-time applications such as chat, news feeds and web push notifications.

**OR**

Node. js is primarily used for non-blocking, event-driven servers, due to its single-threaded nature. It's used for traditional web sites and back-end API services, but was designed with real-time, push-based architectures in mind.

About Node.js : <a href="https://www.w3schools.com/nodejs/nodejs_intro.asp">Click Here</a>

# 5. What is the difference of JS from browser to JS on node.js

=> - Both the browser and Node.js use JavaScript as their programming language.
- Building apps that run in the browser is a completely different thing than building a Node.js application.
- From the perspective of a frontend developer who extensively uses JavaScript, Node.js apps bring with them a huge advantage: the comfort of programming everything - the frontend and the backend - in a single language.
- In the browser, most of the time what you are doing is interacting with the DOM, or other Web Platform APIs like Cookies. Those do not exist in Node.js, of course. You don't have the document, window and all the other objects that are provided by the browser.
- And in the browser, we don't have all the nice APIs that Node.js provides through its modules, like the filesystem access functionality.
- Another big difference is that in Node.js you control the environment. Unless you are building an open source application that anyone can deploy anywhere, you know which version of Node.js you will run the application on. Compared to the browser environment, where you don't get the luxury to choose what browser your visitors will use, this is very convenient.
- You can use Babel to transform your code to be ES5-compatible before shipping it to the browser, but in Node.js, you won't need that.
- Another difference is that Node.js uses the CommonJS module system, while in the browser we are starting to see the ES Modules standard being implemented.
- In practice, this means that for the time being you use require() in Node.js and import in the browser.

# 6. Write three different ways to reverse a string in Javascript? a. using inbuilt method, b. iteratively, c. recursively
=> a. using inbuilt method:
```js
function reverseString(str) {
    return str.split("").reverse().join("");
}
reverseString("hello");
```

b. iteratively:
```js
function reverseString(str) {
    var newString = "";
    for (var i = str.length - 1; i >= 0; i--) {
        newString += str[i];
    }
    return newString;
}
reverseString('hello');
```

c. recursively:
```js
function reverseString(str) {
  if (str === "")
    return "";
  else
    return reverseString(str.substr(1)) + str.charAt(0);
}
reverseString("hello");

// or

function reverseString(str) {
  return (str === '') ? '' : reverseString(str.substr(1)) + str.charAt(0);
}
reverseString("hello");
```

# 7. Write a program to check two objects are equal ( deep equal )
=> 
```js
function checkObjEqual(obj1,obj2){
for(let key in obj1){
  if(!(key in obj2 )) return false;
  if(obj1[key]!==obj2[key])return false;
}
return true;
}

console.log(checkObjEqual({maroon:'#800000',purple :'#800080'},{purple :'#800080',maroon:'#800000'})) //true

// or

const obj1 = {
        name: 'Ram',
        age: 21
    };
  
    const obj2 = {
        name: 'Ram',
        age: 21
    };
  
    const haveSameData = function (obj1, obj2) {
        const obj1Length = Object.keys(obj1).length;
        const obj2Length = Object.keys(obj2).length;
  
        if (obj1Length === obj2Length) {
            return Object.keys(obj1).every(
                key => obj2.hasOwnProperty(key)
                    && obj2[key] === obj1[key]);
        }
        return false;
    }
    console.log(haveSameData(obj1, obj2));
```

# 8. What is shallow equal?
=> A function for performing a shallow comparison between two objects or arrays. Two values have shallow equality when all of their members are strictly equal to the corresponding member of the other.

**OR**

React-Redux uses shallow equality checking to determine whether the component it's wrapping needs to be re-rendered. To do this, it assumes that the wrapped component is pure; that is, that the component will produce the same results given the same props and state.

# 9. Using classes write a program to build a Parking Lot.
=>  
```js
class Spot {
  constructor({ size, vehicle } = {}) {
    this.size = size
    this.vehicle = vehicle
  }

  addVehicle(vehicle) {
    if(this.isOccupied()) return false
    this.vehicle = vehicle
    return true
  }

  isOccupied() {
      return !!this.vehicle
  }

  getVehicle() {
    return this.vehicle
  }

  releaseVehicle() {
    const currentVehicle = this.vehicle
    this.vehicle = null

    return currentVehicle
  }
}

class ParkingLotAssistant {
  constructor({ floors: { floor1Spot, floor2Spot, floor3Spot } }) {
    this.emptySpots = Array.from({ length: 3 }, (_, i) => {
        if(this._getfloorIndex(1) === i) return Array.from({length: floor1Spot}, () => (new Spot({size: size++})))
        if(this._getfloorIndex(2) === i) return Array.from({length: floor2Spot}, () => (new Spot({size: size++})))
        if(this._getfloorIndex(3) === i) return Array.from({length: floor3Spot}, () => (new Spot({size: size++})))
    })

    this.vehicles = new Map()
  }

  placeVehicle(vehicle) {
      if(this.hasVehicle(vehicle.licenseId)) throw new Error('duplicate vehicle found')
    const floorIndex = this._getfloorIndex(vehicle.floor)
    for (let i = floorIndex; i < this.emptySpots.length; i++) {
      if (this.emptySpots[i].length > 0) {
        const spot = this.emptySpots[i].pop()
        spot.addVehicle(vehicle)
        this.vehicles.set(vehicle.licenseId, spot)
        return true
      }
    }

    return false
  }

  _getfloorIndex(floor) {
    return floor - 1
  }

  hasVehicle(licenseId) {
      return this.vehicles.has(licenseId)
  }

  removeVehicle(vehicle) {
    if (!this.hasVehicle(vehicle.licenseId)) return false
    const spot = this.vehicles.get(vehicle)
    spot.releaseVehicle()
    this.vehicles.delete(vehicle)
    this.emptySpots[this._getfloorIndex(this.spot.size)].push(spot)

    return true
  }
}

class Vehicle {
  constructor(id) {
    this.licenseId = id
  }
}

class Car extends Vehicle {
  constructor(id) {
    super(id)
    this.floor = 2
  }
}

const parkingLotAssistant = new ParkingLotAssistant({
    floors: {
        floor1Spot: 10,
        floor2Spot: 10,
        floor3Spot: 10,
    }
})

const car1 = new Car('car1')
const car2 = new Car('car2')
const car3 = new Car('car3')

parkingLotAssistant.placeVehicle(car1)
parkingLotAssistant.placeVehicle(car2)
parkingLotAssistant.placeVehicle(car3)

console.log(parkingLotAssistant);
```