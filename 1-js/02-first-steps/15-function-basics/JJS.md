함수선언
```js
function showMessage() {
    alert('Hello everyone!');
}
showMessage();
```

지역 변수
```js
function showMessage() {
    let message = a; // local variable

    alert(message);
}
showMessage(); // a

alert(message); // Error
```

외부변수
```js
let userName = 'JJS';

function showMessage() {
    let message = 'a, ' + userName;
    alert(message);
}
showMessage(); // a, JJS

```
```js
let userName = 'John';

function showMessage() {
  userName = "Bob";

  let message = 'Hello, ' + userName;
  console.log(message);
}

console.log( userName );

showMessage();

console.log( userName ); 
```

매개변수
```js
function showMessage(from, text) { // parameters: from, text
  alert(from + ': ' + text);
}

showMessage('Ann', 'Hello!'); // Ann: Hello! (*)
showMessage('Ann', "What's up?"); // Ann: What's up? (**)
```
매개변수를 사용하여 임의의 데이터를 함수에 전달

기본값
```js
function showMessage(from, text = "no text given") {
  alert( from + ": " + text );
}

showMessage("Ann"); // Ann: no text given
```
함수이름 지정 
"get…"– 값을 반환합니다.
"calc…"– 무언가를 계산하고,
"create…"– 뭔가를 창조하다,
"check…"– 무언가를 확인하고 부울 등을 반환합니다.
```js
showMessage(..)     // shows a message
getAge(..)          // returns the age (gets it somehow)
calcSum(..)         // calculates a sum and returns the result
createForm(..)      // creates a form (and usually returns it)
checkPermission(..) // checks a permission, returns true/false
```

min(a,b)
```js
min(2, 5) == 2
min(3, -1) == -1
min(1, 1) == 1
```
min(a,b)두 숫자 중 가장 작은 숫자 a와 를 반환하는 함수

pow(x,n)
```js
pow(3, 2) = 3 * 3 = 9
pow(3, 3) = 3 * 3 * 3 = 27
pow(1, 100) = 1 * 1 * ...* 1 = 1
```
거듭제곱 pow(x,n)을 반환하는 함수