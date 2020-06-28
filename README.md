# Learn Modern JavaScript

### Explore Differences Between the var and let Keywords

- let은 여러 번 선언할 수 없다.

```js
var catName = "Quincy";
var quote;

var catName = "Beau";

function catTalk() {
  "use strict";

  catName = "Oliver";
  quote = catName + " says Meow!";
}
catTalk();
```

```js
let catName = "Quincy";
let quote;

let catName = "Beau"; // => Error

function catTalk() {
  "use strict";

  catName = "Oliver";
  quote = catName + " says Meow!";
}
catTalk();
```

### Compare Scopes of the var and let Keywords

```js
function checkScope() {
  "use strict";
  var i = "function scope";
  if (true) {
    i = "block scope";
    console.log("Block scope i is: ", i);
  }
  console.log("Function scope i is: ", i);
  return i;
}

checkScope();
//Block scope i is: block scope
//Function scope i is: block scope
```

```js
function checkScope() {
  "use strict";
  let i = "function scope";
  if (true) {
    let i = "block scope";
    console.log("Block scope i is: ", i);
  }
  console.log("Function scope i is: ", i);
  return i;
}

checkScope();
//Block scope i is: block scope
//Function scope i is: function scope
```

```js
function checkScope() {
  "use strict";
  // let i = "function scope";
  if (true) {
    let i = "block scope";
    console.log("Block scope i is: ", i);
  }
  console.log("Function scope i is: ", i); // => Error (i is not defined)
  return i;
}

checkScope();
//Block scope i is: block scope
//Function scope i is: function scope
```

### Declare a Read-Only Variable with the const Keyword

- let과 const의 유일한 차이점: const는 읽기만 가능(변경 불가능)
- const는 주로 대문자로 선언한다.

```js
function printManyTimes(str) {
  "use strict";

  let sentence = str + " is cool!";

  sentence = str + " is amazing!";

  for (let i = 0; i < str.length; i += 2) {
    console.log(sentence);
  }
}

printManyTimes("freeCodeCamp");
```

```js
function printManyTimes(str) {
  "use strict";

  const SENTENCE = str + " is cool!";

  SENTENCE = str + " is amazing!"; // => Error ("SENTENCE" is read-only)

  for (let i = 0; i < str.length; i += 2) {
    console.log(SENTENCE);
  }
}

printManyTimes("freeCodeCamp");
```

### Mutate an Array Declared with const

```js
const s = [5, 7, 2];
function editInPlace() {
  "use strict";

  s = [2, 5, 7]; // => Error
}
editInPlace();

console.log(s);
```

```js
const s = [5, 7, 2];
function editInPlace() {
  "use strict";

  s[0] = 2;
  s[1] = 5;
  s[2] = 7;
}
editInPlace();

console.log(s);
```

### Prevent Object Mutation

```js
function freezeObj() {
  "use strict";
  const MATH_CONSTANTS = {
    PI: 3.14,
  };

  try {
    MATH_CONSTANTS.PI = 99;
  } catch (ex) {
    console.log(ex);
  }

  return MATH_CONSTANTS.PI;
}

const PI = freezeObj();

console.log(PI); //99
```

```js
function freezeObj() {
  "use strict";
  const MATH_CONSTANTS = {
    PI: 3.14,
  };

  Object.freeze(MATH_CONSTANTS);

  try {
    MATH_CONTANTS.PI = 99;
  } catch (ex) {
    console.log(ex);
  }

  return MATH_CONSTANTS.PI;
}

const PI = freezeObj();

console.log(PI); //3.14
```

### Use Arrow Functions to Write Concise Anonymous Functions

```js
var magic = function () {
  return new Date();
};
```

```js
var magic = () => {
  return new Date();
};
```

```js
const magic = () => new Date();
```

### Write Arrow Functions with Parameters

```js
var myConcat = function (arr1, arr2) {
  return arr1.concat(arr2);
};

console.log(myConcat([1, 2], [3, 4, 5])); //[1, 2, 3, 4, 5]
```

```js
const myConcat = (arr1, arr2) => arr1.concat(arr2);

console.log(myConcat([1, 2], [3, 4, 5])); //[1, 2, 3, 4, 5]
```

### Write Higher Order Arrow Functions

```js
const realNumberArray = [4, 5.6, -9.8, 3.14, 42, 6, 8.34, -2];

const squareList = (arr) => {
  const squaredIntegers = arr
    .filter((num) => Number.isInteger(num) && num > 0)
    .map((x) => x * x);
  return squaredIntegers;
};

const squaredIntegers = squareList(realNumberArray);
console.log(squaredIntegers);
```

### Set Default Parameters for Your Functions

```js
const increment = (function () {
  return function increment(number, value = 1) {
    return number + value;
  };
})();
console.log(increment(5, 2));
console.log(increment(5));
```

### Use the Rest Operator with Function Parameters

```js
const sum = (function () {
  return function sum(x, y, z) {
    const args = [x, y, z];
    return args.reduce((a, b) => a + b, 0);
  };
})();
console.log(sum(1, 2, 3));
```

```js
const sum = (function () {
  return function sum(...args) {
    return args.reduce((a, b) => a + b, 0);
  };
})();
console.log(sum(1, 2, 3));
```

## Use the Spread Operator to Evaluate Arrays In-Place

```js
const arr1 = ["JAN", "FEB", "MAR", "APR", "MAY"];
let arr2;
(function () {
  arr2 = arr1; // change this line
  arr1[0] = "potato";
})();
console.log(arr2); //["potato", "FEB", "MAR", "APR", "MAY"]
```

```js
const arr1 = ["JAN", "FEB", "MAR", "APR", "MAY"];
let arr2;
(function () {
  arr2 = [...arr1]; // change this line
  arr1[0] = "potato";
})();
console.log(arr2); //["JAN", "FEB", "MAR", "APR", "MAY"]
```

### Use Destructuring Assignment to Assign Variables from Objects

```js
var voxel = { x: 3.6, y: 7.4, z: 6.54 };

var x = voxel.x; // x = 3.6
var y = voxel.y; // y = 7.4
var z = voxel.z; // z = 6.54

const { x: a, y: b, z: c } = voxel; // a = 3.6, b = 7.4, c = 6.54

const AVG_TEMPERATURES = {
  today: 77.5,
  tomorrow: 79,
};

function getTempOfTmrw(avgTemperatures) {
  "use strict";
  // change code below this line
  const { tomorrow: tempOfTomorrow } = avgTemperatures; // change this line
  // change code above this line
  return tempOfTomorrow;
}

console.log(getTempOfTmrw(AVG_TEMPERATURES)); // should be 79
```

### Use Destructuring Assignment to Assign Variables from Nested Objects

```js
const LOCAL_FORECAST = {
  today: { min: 72, max: 83 },
  tomorrow: { min: 73.3, max: 84.6 },
};

function getMaxOfTmrw(forecast) {
  "use strict";

  const {
    tomorrow: { max: maxOfTomorrow },
  } = forecast;

  return maxOfTomorrow;
}

console.log(getMaxOfTmrw(LOCAL_FORECAST));
```

### Use Destructuring Assignment to Assign Variables from Arrays

```js
const [z, x, , y] = [1, 2, 3, 4, 5, 6];
console.log(z, x, y); // 1, 2, 4

let a = 8;
let b = 6;
(() => {
  "use strict";
  [a, b] = [b, a];
})();
console.log(a); // 6
console.log(b); // 8
```
