# 객체

- 원시형 = 오직 하나의 데이터만 담을수 있을때
- **객체형** = 다양한 데이터를 담을수 있을때, entity 로 저장 가능

객체는 중괄호 `{}`를 이용해 만들 수 있습니다. 중괄호 안에는 '키(key): 값(value)' 쌍으로 구성된 _프로퍼티(property)_ 를 여러 개 넣을 수 있는데, `키`엔 문자형, `값`엔 모든 자료형이 허용됩니다.

- property = key : value
- 서랍장 = 이름표 : 파일

`key = 이름표 = 프로퍼티 이름 = 식별자`

복잡한 서랍장 안에서 이름표를 보고 원하는 파일을 쉽게 찾을 수 있듯이, 객체에선 키를 이용해 프로퍼티를 쉽게 찾을 수 있습니다.

![](object.svg)

빈 객체(빈 서랍장)를 만드는 방법은 두 가지가 있습니다.

```js
let user = new Object(); // '객체 생성자' 문법
let user = {}; // '객체 리터럴' 문법
```

![](object-user-empty.svg)

## 객체 리터럴 문법

`let user = {};`

중괄호 `{...}`를 이용해 객체를 선언하는 것을 _객체 리터럴(object literal)_ 이라고 부릅니다. 객체를 선언할 땐 주로 이 방법을 사용합니다.

## 리터럴과 프로퍼티

중괄호 `{...}` 안에는 '키: 값' 쌍으로 구성된 프로퍼티가 들어갑니다.

```js
let user = {
  // 객체
  name: "John", // 키: "name",  값: "John"
  age: 30, // 키: "age", 값: 30
};
```

객체 `user`에는 프로퍼티가 두 개 있습니다.

1. 첫 번째 프로퍼티 -- `"name"`(이름)과 `"John"`(값)
2. 두 번째 프로퍼티 -- `"age"`(이름)과 `30`(값)

서랍장(객체 `user`) 안에 파일 두 개(프로퍼티 두 개)가 담겨있는데, 각 파일에 "name", "age"라는 이름표가 붙어있다고 생각하시면 쉽습니다.

![user object](object-user.svg)

서랍장에 파일을 추가하고 뺄 수 있듯이 개발자는 프로퍼티를 추가, 삭제할 수 있습니다.

## 점 표기법(dot notation)

점 표기법(dot notation)을 이용하면 프로퍼티 값을 읽는 것도 가능합니다.

```js
// 프로퍼티 값 얻기
alert(user.name); // John
alert(user.age); // 30
```

### 불린형 프로퍼티를 추가

```js
user.isAdmin = true;
```

![user object 2](object-user-isadmin.svg)

### `delete` 연산자를 사용하여 프로퍼티를 삭제

```js
delete user.age;
```

![user object 3](object-user-delete.svg)

프로퍼티 이름이 2개 이상인 경우 경우엔 프로퍼티 이름을 "따옴표"로 묶어줘야 합니다.
`"likes birds": true`

```js
let user = {
  name: "John",
  age: 30,
  "likes birds": true, // 복수의 단어는 따옴표로 묶어야 합니다.
};
```

![](object-user-props.svg)

마지막 프로퍼티 끝은 쉼표로 끝날 수 있습니다.

```js
let user = {
  name: "John",
  age: 30*!*,*/!*
}
```

````smart header="상수 객체는 수정될 수 있습니다."
주의하세요. `const`로 선언된 객체는 수정될 수 있습니다.

예시:

```js run
const user = {
  name: "John"
};

*!*
user.name = "Pete"; // (*)
*/!*

alert(user.name); // Pete
```

`user.name=...` 으로 내용을 수정가능합니다.
하지만 `const`는 `user=...`를 전체적으로 설정하려고 할 때는 오류가 발생합니다.

````

## 대괄호 표기법

두개 이상의 단어를 사용할때,
키가 유효한 변수 식별자가 아닌 경우엔 점 표기법 대신에 '대괄호 표기법(square bracket notation)'이라 불리는 방법을 사용할 수 있습니다. 대괄호 표기법은 키에 어떤 문자열이 있던지 상관없이 동작합니다.

```js run
let user = {};

// set
user["likes birds"] = true;

// get
alert(user["likes birds"]); // true

// delete
delete user["likes birds"];
```

이제 문법 에러가 발생하지 않네요. 대괄호 표기법 안에서 문자열을 사용할 땐 문자열을 따옴표로 묶어줘야 한다는 점에 주의하시기 바랍니다. 따옴표의 종류는 상관없습니다.

대괄호 표기법을 사용하면 아래 예시에서 변수를 키로 사용한 것과 같이 문자열뿐만 아니라 모든 표현식의 평가 결과를 프로퍼티 키로 사용할 수 있습니다.

```js
let key = "likes birds";

// user["likes birds"] = true; 와 같습니다.
user[key] = true;
```

## key 자체로 로 접근할때 (점 표기법은 .key 불가능)

변수 `key`는 런타임에 평가되기 때문에 사용자 입력값 변경 등에 따라 값이 변경될 수 있습니다. 어떤 경우든, 평가가 끝난 이후의 결과가 프로퍼티 키로 사용됩니다. 이를 응용하면 코드를 유연하게 작성할 수 있습니다.

예시:

```js run
let user = {
  name: "John",
  age: 30,
};

let key = prompt("사용자의 어떤 정보를 얻고 싶으신가요?", "name");

// 변수로 접근
alert(user[key]); // John (프롬프트 창에 "name"을 입력한 경우)
```

그런데 점 표기법은 이런 방식이 불가능합니다.

```js run
let user = {
  name: "John",
  age: 30,
};

let key = "name";
alert(user.key); // undefined
```

### 계산된 프로퍼티 []

객체를 만들 때 객체 리터럴 안의 프로퍼티 키가 [대괄호]로 둘러싸여 있는 경우, 이를 _계산된 프로퍼티(computed property)_ 라고 부릅니다.

예시:

```js run
let fruit = prompt("어떤 과일을 구매하시겠습니까?", "apple");

let bag = {
*!*
  [fruit]: 5, // 변수 fruit에서 프로퍼티 이름을 동적으로 받아 옵니다.
*/!*
};

alert( bag.apple ); // fruit에 "apple"이 할당되었다면, 5가 출력됩니다.
```

위 예시에서 `[fruit]`는 프로퍼티 이름을 변수 `fruit`에서 가져오겠다는 것을 의미합니다.

사용자가 프롬프트 대화상자에 `apple`을 입력했다면 `bag`엔 `{apple: 5}`가 **할당**되었을 겁니다.

아래 예시는 위 예시와 동일하게 동작합니다.

```js run
let fruit = prompt("어떤 과일을 구매하시겠습니까?", "apple");
let bag = {};

// 변수 fruit을 사용해 프로퍼티 이름을 만들었습니다.
bag[fruit] = 5;
```

두 방식 중 계산된 프로퍼티를 사용한 예시가 더 깔끔해 보이네요.

한편, 다음 예시처럼 대괄호 안에는 복잡한 표현식이 올 수도 있습니다.

```js
let fruit = "apple";
let bag = {
  [fruit + "Computers"]: 5, // bag.appleComputers = 5
};
```

대괄호 표기법은 프로퍼티 이름과 값의 제약을 없애주기 때문에 점 표기법보다 훨씬 강력합니다. 그런데 작성하기 번거롭다는 단점이 있습니다.

## 단축 프로퍼티

key 와 value 값이 동일 할때

```
name: name,
age: age,
```

단축 프로퍼티 구문으로 코드를 짧게 줄일 수 있습니다.

```
name, // name: name 과 같음
age,
```

실무에선 프로퍼티 값을 기존 변수에서 받아와 사용하는 경우가 종종 있습니다.

예시:

```js run
function makeUser(name, age) {
  return {
    name: name,
    age: age,
    // ...등등
  };
}

let user = makeUser("John", 30);
alert(user.name); // John
```

위 예시의 프로퍼티들은 이름과 값이 변수의 이름과 동일하네요. 이렇게 변수를 사용해 프로퍼티를 만드는 경우는 아주 흔한데, _프로퍼티 값 단축 구문(property value shorthand)_ 을 사용하면 코드를 짧게 줄일 수 있습니다.

`name:name` 대신 `name`만 적어주어도 프로퍼티를 설정할 수 있죠.

```js
function makeUser(name, age) {
*!*
  return {
    name, // name: name 과 같음
    age,  // age: age 와 같음
    // ...
  };
*/!*
}
```

한 객체에서 일반 프로퍼티와 단축 프로퍼티를 함께 사용하는 것도 가능합니다.

```js
let user = {
  name, // name: name 과 같음
  age: 30,
};
```

## 프로퍼티 이름의 제약사항

아시다시피 변수 이름(키)엔 'for', 'let', 'return' 같은 예약어를 사용하면 안됩니다.

**그런데 객체 프로퍼티엔 이런 제약이 없습니다.**

```js run
// 예약어를 키로 사용해도 괜찮습니다.
let obj = {
  for: 1,
  let: 2,
  return: 3,
};

alert(obj.for + obj.let + obj.return); // 6
```

이와 같이 프로퍼티 이름엔 특별한 제약이 없습니다. 어떤 문자형, 심볼형 값도 프로퍼티 키가 될 수 있죠(식별자로 쓰이는 심볼형에 대해선 뒤에서 다룰 예정입니다).

문자형이나 심볼형에 속하지 않은 값은 문자열로 자동 형 변환됩니다.

예시를 살펴봅시다. 키에 숫자 `0`을 넣으면 문자열 `"0"`으로 자동변환됩니다.

```js run
let obj = {
  0: "test", // "0": "test"와 동일합니다.
};

// 숫자 0은 문자열 "0"으로 변환되기 때문에 두 얼럿 창은 같은 프로퍼티에 접근합니다,
alert(obj["0"]); // test
alert(obj[0]); // test (동일한 프로퍼티)
```

## 'in' 연산자로 프로퍼티 존재 여부 확인하기

자바스크립트 객체의 중요한 특징 중 하나는 다른 언어와는 달리, 존재하지 않는 프로퍼티에 접근하려 해도 에러가 발생하지 않고 `undefined`를 반환한다는 것입니다.

이런 특징을 응용하면 프로퍼티 존재 여부를 쉽게 확인할 수 있습니다.

### 일치 연산자로 존재 여부 확인하기

```js run
let user = {};

alert(user.noSuchProperty === undefined); // true는 '프로퍼티가 존재하지 않음'을 의미합니다.
```

이렇게 `undefined`와 비교하는 것 이외에도 연산자 `in`을 사용하면 프로퍼티 존재 여부를 확인할 수 있습니다.

문법은 다음과 같습니다.

```js
"key" in object;
```

예시:

```js run
let user = { name: "John", age: 30 };

alert("age" in user); // user.age가 존재하므로 true가 출력됩니다.
alert("blabla" in user); // user.blabla는 존재하지 않기 때문에 false가 출력됩니다.
```

`in` 왼쪽엔 반드시 *프로퍼티 이름*이 와야 합니다. 프로퍼티 이름은 보통 따옴표로 감싼 문자열입니다.

따옴표를 생략하면 아래 예시와 같이 엉뚱한 변수가 조사 대상이 됩니다.

```js run
let user = { age: 30 };

let key = "age";
alert( *!*key*/!* in user ); // true, 변수 key에 저장된 값("age")을 사용해 프로퍼티 존재 여부를 확인합니다.
```

그런데 이쯤 되면 "`undefined`랑 비교해도 충분한데 왜 `in` 연산자가 있는 거지?"라는 의문이 들 수 있습니다.

대부분의 경우, 일치 연산자를 사용해서 프로퍼티 존재 여부를 알아내는 방법(`"=== undefined"`)은 꽤 잘 동작합니다. 그런데 가끔은 이 방법이 실패할 때도 있습니다. 이럴 때 `in`을 사용하면 프로퍼티 존재 여부를 제대로 판별할 수 있습니다.

프로퍼티는 존재하는데, 값에 `undefined`를 할당한 예시를 살펴봅시다.

```js run
let obj = {
  test: undefined,
};

alert(obj.test); // 값이 `undefined`이므로, 얼럿 창엔 undefined가 출력됩니다. 그런데 프로퍼티 test는 존재합니다.

alert("test" in obj); // `in`을 사용하면 프로퍼티 유무를 제대로 확인할 수 있습니다(true가 출력됨).
```

`obj.test`는 실제 존재하는 프로퍼티입니다. 따라서 `in` 연산자는 정상적으로 true를 반환합니다.

`undefined`는 변수는 정의되어 있으나 값이 할당되지 않은 경우에 쓰기 때문에 프로퍼티 값이 `undefined`인 경우는 흔치 않습니다. 값을 '알 수 없거나(unknown)' 값이 '비어 있다는(empty)' 것을 나타낼 때는 주로 `null`을 사용합니다. 위 예시에서 `in` 연산자는 자리에 어울리지 않는 초대손님처럼 보이네요.

## 'for..in' 반복문

`for..in` 반복문을 사용하면 객체의 모든 키를 순회할 수 있습니다. `for..in`은 앞서 학습했던 `for(;;)` 반복문과는 완전히 다릅니다.

문법:

```js
for (key in object) {
  // 각 프로퍼티 키(key)를 이용하여 본문(body)을 실행합니다.
}
```

아래 예시를 실행하면 객체 `user`의 모든 프로퍼티가 출력됩니다.

```js run
let user = {
  name: "John",
  age: 30,
  isAdmin: true,
};

for (let key in user) {
  // 키
  alert(key); // name, age, isAdmin
  // 키에 해당하는 값
  alert(user[key]); // John, 30, true
}
```

`for..in` 반복문에서도 `for(;;)`문처럼 반복 변수(looping variable)를 선언(`let key`)했다는 점에 주목해 주시기 바랍니다.

반복 변수명은 자유롭게 정할 수 있습니다. `'for (let prop in obj)'`같이 `key` 말고 다른 변수명을 사용해도 괜찮습니다.

### 객체 정렬 방식

"프로퍼티엔 순서가 있을까?"

- 정수 프로퍼티(integer property)는 자동으로 정렬되고,
- 그 외의 프로퍼티는 객체에 추가한 순서 그대로 정렬됩니다.

아래 객체엔 국제전화 나라 번호가 담겨있습니다.

```js run
let codes = {
  "49": "독일",
  "41": "스위스",
  "44": "영국",
  // ..,
  "1": "미국"
};

*!*
for (let code in codes) {
  alert(code); // 1, 41, 44, 49
}
*/!*
```

현재 개발 중인 애플리케이션의 주 사용자가 독일인이라고 가정해 봅시다. 나라 번호를 선택하는 화면에서 `49`가 맨 앞에 오도록 하는 게 좋을 겁니다.

그런데 코드를 실행해 보면 예상과는 전혀 다른 결과가 출력됩니다.

- 미국(1)이 첫 번째로 출력됩니다.
- 그 뒤로 스위스(41), 영국(44), 독일(49)이 차례대로 출력됩니다.

이유는 나라 번호(키)가 정수이어서 `1, 41, 44, 49` 순으로 프로퍼티가 자동 정렬되었기 때문입니다.

한편, 키가 정수가 아닌 경우엔 작성된 순서대로 프로퍼티가 나열됩니다. 예시를 살펴봅시다.

```js run
let user = {
  name: "John",
  surname: "Smith"
};
user.age = 25; // 프로퍼티를 하나 추가합니다.

*!*
// 정수 프로퍼티가 아닌 프로퍼티는 추가된 순서대로 나열됩니다.
*/!*
for (let prop in user) {
  alert( prop ); // name, surname, age
}
```

위 예시에서 49(독일 나라 번호)를 가장 위에 출력되도록 하려면 나라 번호가 정수로 취급되지 않도록 속임수를 쓰면 됩니다. 각 나라 번호 앞에 `"+"`를 붙여봅시다.

아래 같이 말이죠.

```js run
let codes = {
  "+49": "독일",
  "+41": "스위스",
  "+44": "영국",
  // ..,
  "+1": "미국",
};

for (let code in codes) {
  alert(+code); // 49, 41, 44, 1
}
```

이제 원하는 대로 독일 나라 번호가 가장 먼저 출력되는 것을 확인할 수 있습니다.

## 요약

객체는 몇 가지 특수한 기능을 가진 연관 배열(associative array)입니다.

객체는 프로퍼티(키-값 쌍)를 저장합니다.

- "프로퍼티 키"는 문자열이나 심볼이어야 합니다. 보통은 **문자열**입니다.
- 값은 **어떤 자료형**도 가능합니다.

아래와 같은 방법을 사용하면 프로퍼티에 접근할 수 있습니다.

- 점 표기법: `obj.property`
- 대괄호 표기법 `obj["property"]`. 대괄호 표기법을 사용하면 `obj[varWithKey]`같이 변수에서 키를 가져올 수 있습니다.

객체엔 다음과 같은 추가 연산자를 사용할 수 있습니다.

- 프로퍼티를 삭제하고 싶을 때: `delete obj.prop`
- 해당 key를 가진 프로퍼티가 객체 내에 있는지 확인하고자 할 때: `"key" in obj`
- 프로퍼티를 나열할 때: `for (let key in obj)`

지금까진 '순수 객체(plain object)'라 불리는 일반 `객체`에 대해 학습했습니다.

자바스크립트에는 일반 객체 이외에도 다양한 종류의 객체가 있습니다.

- `Array` -- 정렬된 데이터 컬렉션을 저장할 때 쓰임
- `Date` -- 날짜와 시간 정보를 저장할 때 쓰임
- `Error` -- 에러 정보를 저장할 때 쓰임
- 기타 등등
