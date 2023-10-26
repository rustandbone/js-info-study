# Object.keys, values, entries

순회(iteration)에 관해 이야기 나누어봅시다.

`keys()`, `values()`, `entries()`를 사용할 수 있는 자료구조는 다음과 같습니다.

- `Map`
- `Set`
- `Array`

일반 객체에도 순회 관련 메서드가 있긴 한데, `keys()`, `values()`, `entries()`와는 문법에 차이가 있습니다.

## Object.keys, values, entries

일반 객체엔 다음과 같은 메서드를 사용할 수 있습니다.

- [Object.keys(obj)](mdn:js/Object/keys) -- 객체의 키만 담은 배열을 반환합니다.
- [Object.values(obj)](mdn:js/Object/values) -- 객체의 값만 담은 배열을 반환합니다.
- [Object.entries(obj)](mdn:js/Object/entries) -- `[키, 값]` 쌍을 담은 배열을 반환합니다.

예시:

```js
let user = {
  name: "John",
  age: 30,
};
```

- `Object.keys(user) = ["name", "age"]`
- `Object.values(user) = ["John", 30]`
- `Object.entries(user) = [ ["name","John"], ["age",30] ]`

아래 예시처럼 `Object.values`를 사용하면 프로퍼티 값을 대상으로 원하는 작업을 할 수 있습니다.

```js run
let user = {
  name: "Violet",
  age: 30,
};

// 값을 순회합니다.
for (let value of Object.values(user)) {
  alert(value); // Violet과 30이 연속적으로 출력됨
}
```

## 객체 변환하기

객체엔 `map`, `filter` 같은 배열 전용 메서드를 사용할 수 없습니다.

하지만 `Object.entries`와 `Object.fromEntries`를 순차적으로 적용하면 객체에도 배열 전용 메서드 사용할 수 있습니다. 적용 방법은 다음과 같습니다.

1. `Object.entries(obj)`를 사용해 객체의 키-값 쌍이 요소인 배열을 얻습니다.
2. 1.에서 만든 배열에 `map` 등의 배열 전용 메서드를 적용합니다.
3. 2.에서 반환된 배열에 `Object.fromEntries(array)`를 적용해 배열을 다시 객체로 되돌립니다.

이 방법을 사용해 가격 정보가 저장된 객체 prices의 프로퍼티 값을 두 배로 늘려보도록 합시다.

```js run
let prices = {
  banana: 1,
  orange: 2,
  meat: 4,
};

*!*
let doublePrices = Object.fromEntries(
  // 객체를 배열로 변환해서 배열 전용 메서드인 map을 적용하고 fromEntries를 사용해 배열을 다시 객체로 되돌립니다.
  Object.entries(prices).map(([key, value]) => [key, value * 2])
);
*/!*

alert(doublePrices.meat); // 8
```

근데 왜 굳이 이렇게 하는지는 모르겠습니다.
여기서 Object.fromEntries() 란?

## Object.fromEntries()

Object.fromEntries() 메서드는 키값 쌍의 목록을 객체로 바꿉니다.

```jsx
const entries = new Map([
  ["foo", "bar"],
  ["baz", 42],
]);

const obj = Object.fromEntries(entries);

console.log(obj);
// Expected output: Object { foo: "bar", baz: 42 }
```
