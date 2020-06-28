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
