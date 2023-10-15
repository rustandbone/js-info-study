함수 표현식
```js
function sayHi() {   // (1) create
  alert( "Hello" );
}

let func = sayHi;    // (2) copy

func(); // Hello     // (3) run the copy (it works)!
sayHi(); // Hello    //     this still works too (why wouldn't it)
```

```js
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

function showOk() {
  alert( "You agreed." );
}

function showCancel() {
  alert( "You canceled the execution." );
}

// usage: functions showOk, showCancel are passed as arguments to ask
ask("Do you agree?", showOk, showCancel);
```

```js
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

ask(
  "Do you agree?",
  function() { alert("You agreed."); },
  function() { alert("You canceled the execution."); }
);
```

함수 선언: 기본 코드 흐름에서 별도의 문으로 선언된 함수
```js
// Function Declaration
function sum(a, b) {
  return a + b;
}
```
함수 표현식: 표현식 내부 또는 다른 구문 구조 내부에서 생성된 함수입니다. 여기서 함수는 "할당 표현식"의 오른쪽에 생성됩니다 =.
```js
// Function Expression
let sum = function(a, b) {
  return a + b;
};
```

함수 표현식은 실행이 도달하면 생성되며 그 순간부터만 사용할 수 있습니다.
함수 선언은 정의되기 전에 호출될 수 있습니다.



엄격 모드에서 함수 선언이 코드 블록 내에 있으면 해당 블록 내부 어디에서나 볼 수 있습니다. 하지만 그 밖은 아닙니다.
```js
let age = prompt("What is your age?", 18);

// conditionally declare a function
if (age < 18) {

  function welcome() {
    alert("Hello!");
  }

} else {

  function welcome() {
    alert("Greetings!");
  }

}

// ...use it later
welcome(); // Error: welcome is not defined
```
함수 선언(함수 표현식이 아닌)을 조건문 내에서 직접 선언

```js
let age = prompt("What is your age?", 18);

let welcome;

if (age < 18) {

  welcome = function() {
    alert("Hello!");
  };

} else {

  welcome = function() {
    alert("Greetings!");
  };

}

welcome(); // ok now
```
welcome 변수를 선언하고 함수 표현식(anonymous function expression)으로 초기화합니다. 이것은 함수가 변수에 할당되고 나중에 호출

