화살표 함수
```js
let func = (arg1, arg2, ..., argN) => expression;
```
```js
let double = n => n * 2;
// roughly the same as: let double = function(n) { return n * 2 }

alert( double(3) ); // 6
```
인수가 없으면

```js
let sayHi = () => alert("Hello!");

sayHi();
```

```js
let age = prompt("What is your age?", 18);

let welcome = (age < 18) ?
  () => alert('Hello!') :
  () => alert("Greetings!");

welcome();
```

```js
// 일반 함수
function add(a, b) {
  return a + b;
}

// 화살표 함수
const add = (a, b) => a + b;
```