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
