# Date 객체와 날짜

Date 객체를 활용하면 생성 및 수정 시간을 저장하거나 시간을 측정할 수 있고, 현재 날짜를 출력하는 용도 등으로도 활용할 수 있습니다.

## 객체 생성하기

`new Date()`를 호출하면 새로운 `Date` 객체가 만들어지는데, `new Date()`는 다음과 같은 형태로 호출할 수 있습니다.

`new Date()`
: 인수 없이 호출하면 현재 날짜와 시간이 저장된 `Date` 객체가 반환됩니다.

    ```js run
    let now = new Date();
    alert( now ); // 현재 날짜 및 시간이 출력됨
    ```

`new Date(milliseconds)`
: UTC 기준(UTC+0) 1970년 1월 1일 0시 0분 0초에서 `milliseconds` 밀리초(1/1000 초) 후의 시점이 저장된 `Date` 객체가 반환됩니다.

    ```js run
    // 1970년 1월 1일 0시 0분 0초(UTC+0)를 나타내는 객체
    let Jan01_1970 = new Date(0);
    alert( Jan01_1970 );

    // 1970년 1월 1일의 24시간 후는 1970년 1월 2일(UTC+0)임
    let Jan02_1970 = new Date(24 * 3600 * 1000);
    alert( Jan02_1970 );
    ```

### timestamp

    1970년의 첫날을 기준으로 흘러간 밀리초를 나타내는 정수는 *타임스탬프(timestamp)* 라고 부릅니다.

    타임스탬프를 사용하면 날짜를 숫자 형태로 간편하게 나타낼 수 있습니다. `new Date(timestamp)`를 사용해 타임스탬프를 사용해 특정 날짜가 저장된 `Date` 객체를 손쉽게 만들 수 있고 `date.getTime()` 메서드를 사용해 `Date` 객체에서 타임스탬프를 추출하는 것도 가능합니다(자세한 사항은 아래에서 다루도록 하겠습니다).

    1970년 1월 1일을 기준으로 이전 날짜에 해당하는 타임스탬프 값은 음수입니다. 예시를 살펴봅시다.

    ```js
    // 31 Dec 1969
    let Dec31_1969 = new Date(-24 * 3600 * 1000);
    alert( Dec31_1969 );
    ```

`new Date(datestring)` 문자열 자동 구문 분석
: 인수가 하나인데, 문자열이라면 해당 문자열은 자동으로 구문 분석(parsed)됩니다. 구문 분석에 적용되는 알고리즘은 `Date.parse`에서 사용하는 알고리즘과 동일한데, 자세한 내용은 아래에서 다루도록 하겠습니다.

    ```js run
    let date = new Date("2017-01-26");
    alert(date);
    // 인수로 시간은 지정하지 않았기 때문에 GMT 자정이라고 가정하고
    // 코드가 실행되는 시간대(timezone)에 따라 출력 문자열이 바뀝니다.
    // 따라서 얼럿 창엔
    // Thu Jan 26 2017 11:00:00 GMT+1100 (Australian Eastern Daylight Time)
    // 혹은
    // Wed Jan 25 2017 16:00:00 GMT-0800 (Pacific Standard Time)등이 출력됩니다.
    ```

`new Date(year, month, date, hours, minutes, seconds, ms)`
: 주어진 인수를 조합해 만들 수 있는 날짜가 저장된 객체가 반환됩니다(지역 시간대 기준). 첫 번째와 두 번째 인수만 필수값입니다.

    - `year`는 반드시 네 자리 숫자여야 합니다. `2013`은 괜찮고 `98`은 괜찮지 않습니다.
    - `month`는 `0`(1월)부터 `11`(12월) 사이의 숫자여야 합니다.
    - `date`는 일을 나타내는데, 값이 없는 경우엔 1일로 처리됩니다.
    - `hours/minutes/seconds/ms`에 값이 없는 경우엔 `0`으로 처리됩니다.

    예시:

    ```js
    new Date(2011, 0, 1, 0, 0, 0, 0); // 2011년 1월 1일, 00시 00분 00초
    new Date(2011, 0, 1); // hours를 비롯한 인수는 기본값이 0이므로 위와 동일
    ```

    최소 정밀도는 1밀리초(1/1000초)입니다.

    ```js run
    let date = new Date(2011, 0, 1, 2, 3, 4, 567);
    alert( date ); // 2011년 1월 1일, 02시 03분 04.567초
    ```

## 날짜 구성요소 얻기

`Date` 객체의 메서드를 사용하면 연, 월, 일 등의 값을 얻을 수 있습니다.

[getFullYear()](mdn:js/Date/getFullYear)
: 연도(네 자릿수)를 반환합니다.

[getMonth()](mdn:js/Date/getMonth)
: 월을 반환합니다(**0 이상 11 이하**).

[getDate()](mdn:js/Date/getDate)
: 일을 반환합니다(1 이상 31 이하).

[getHours()](mdn:js/Date/getHours), [getMinutes()](mdn:js/Date/getMinutes), [getSeconds()](mdn:js/Date/getSeconds), [getMilliseconds()](mdn:js/Date/getMilliseconds)
: 시, 분, 초, 밀리초를 반환합니다.

```warn header="`getYear()`말고 `getFullYear()`를 사용하세요."
여러 자바스크립트 엔진이 더는 사용되지 않는(deprecated) 비표준 메서드 `getYear()`을 구현하고 있습니다. 이 메서드는 두 자릿수 연도를 반환하는 경우가 있기 때문에 절대 사용해선 안 됩니다. 연도 정보를 얻고 싶다면 `getFullYear()`를 사용하세요.

````

이 외에도 요일을 반환해주는 메서드도 있습니다.

[getDay()](mdn:js/Date/getDay)
: 일요일을 나타내는 `0`부터 토요일을 나타내는 `6`까지의 숫자 중 하나를 반환합니다. 몇몇 나라에서 요일의 첫날이 일요일이 아니긴 하지만, getDay에선 항상 `0`이 일요일을 나타냅니다. 이를 변경할 방법은 없습니다.

**위에서 소개해드린 메서드 모두는 현지 시간 기준 날짜 구성요소를 반환합니다.**

위 메서드 이름에 있는 'get' 다음에 'UTC'를 붙여주면 표준시(UTC+0) 기준의 날짜 구성 요소를 반환해주는 메서드 [getUTCFullYear()](mdn:js/Date/getUTCFullYear), [getUTCMonth()](mdn:js/Date/getUTCMonth), [getUTCDay()](mdn:js/Date/getUTCDay)를 만들 수 있습니다.

현지 시간대가 UTC 시간대와 다르다면 아래 예시를 실행했을 때 얼럿창엔 다른 값이 출력됩니다.

```js run
// 현재 일시
let date = new Date();

// 현지 시간 기준 시
alert( date.getHours() );

// 표준시간대(UTC+0, 일광 절약 시간제를 적용하지 않은 런던 시간) 기준 시
alert( date.getUTCHours() );
````

아래 두 메서드는 위에서 소개한 메서드와 달리 표준시(UTC+0) 기준의 날짜 구성 요소를 반환해주는 메서드가 없습니다.

[getTime()](mdn:js/Date/getTime)
: 주어진 일시와 1970년 1월 1일 00시 00분 00초 사이의 간격(밀리초 단위)인 타임스탬프를 반환합니다.

[getTimezoneOffset()](mdn:js/Date/getTimezoneOffset)
: 현지 시간과 표준 시간의 차이(분)를 반환합니다.

    ```js run
    // UTC-1 시간대에서 이 예시를 실행하면 60이 출력됩니다.
    // UTC+3 시간대에서 이 예시를 실행하면 -180이 출력됩니다.
    alert( new Date().getTimezoneOffset() );

    ```

## 날짜 구성요소 설정하기

아래 메서드를 사용하면 날짜 구성요소를 설정할 수 있습니다.

- [`setFullYear(year, [month], [date])`](mdn:js/Date/setFullYear)
- [`setMonth(month, [date])`](mdn:js/Date/setMonth)
- [`setDate(date)`](mdn:js/Date/setDate)
- [`setHours(hour, [min], [sec], [ms])`](mdn:js/Date/setHours)
- [`setMinutes(min, [sec], [ms])`](mdn:js/Date/setMinutes)
- [`setSeconds(sec, [ms])`](mdn:js/Date/setSeconds)
- [`setMilliseconds(ms)`](mdn:js/Date/setMilliseconds)
- [`setTime(milliseconds)`](mdn:js/Date/setTime) (1970년 1월 1일 00:00:00 UTC부터 밀리초 이후를 나타내는 날짜를 설정)

`setTime()`을 제외한 모든 메서드는 `setUTCHours()`같이 표준시에 따라 날짜 구성 요소를 설정해주는 메서드가 있습니다.

`setHours`와 같은 메서드는 여러 개의 날짜 구성요소를 동시에 설정할 수 있는데, 메서드의 인수에 없는 구성요소는 변경되지 않습니다.

예시:

```js run
let today = new Date();

today.setHours(0);
alert(today); // 날짜는 변경되지 않고 시만 0으로 변경됩니다.

today.setHours(0, 0, 0, 0);
alert(today); // 날짜는 변경되지 않고 시, 분, 초가 모두 변경됩니다(00시 00분 00초).
```

## 자동 고침

`Date` 객체엔 _자동 고침(autocorrection)_ 이라는 유용한 기능이 있습니다. 범위를 벗어나는 값을 설정하려고 하면 자동 고침 기능이 활성화되면서 값이 자동으로 수정됩니다.

예시:

```js run
let date = new Date(2013, 0, *!*32*/!*); // 2013년 1월 32일은 없습니다.
alert(date); // 2013년 2월 1일이 출력됩니다.
```

입력받은 날짜 구성 요소가 범위를 벗어나면 초과분은 자동으로 다른 날짜 구성요소에 배분됩니다.

'2016년 2월 28일'의 이틀 뒤 날짜를 구하고 싶다고 가정해봅시다. 답은 3월 2일 혹은 3월 1일(윤년)이 될 텐데, 2016년이 윤년인지 아닌지 생각할 필요 없이 단순히 이틀을 더해주기만 하면 답을 구할 수 있습니다. 나머지 작업은 `Date` 객체가 **알아서 처리해 주기 때문이죠.**

```js run
let date = new Date(2016, 1, 28);
*!*
date.setDate(date.getDate() + 2);
*/!*

alert( date ); // 2016년 3월 1일
```

자동 고침은 일정 시간이 지난 후의 날짜를 구하는데도 종종 사용됩니다. '지금부터 70초 후'의 날짜를 구해봅시다.

```js run
let date = new Date();
date.setSeconds(date.getSeconds() + 70);

alert(date); // 70초 후의 날짜가 출력됩니다.
```

0이나 음수를 날짜 구성요소에 설정하는 것도 가능합니다. 예시를 살펴봅시다.

```js run
let date = new Date(2016, 0, 2); // 2016년 1월 2일

date.setDate(1); // 1일로 변경합니다.
alert(date); // 01 Jan 2016

date.setDate(0); // 일의 최솟값은 1이므로 0을 입력하면 전 달의 마지막 날을 설정한 것과 같은 효과를 봅니다.
alert(date); // 31 Dec 2015
```

## Date 객체를 숫자로 변경해 시간차 측정하기

`(+date) 와 date.getTime()` 는 같은 결과값 `1698138010994` 을 낸다.

`Date` 객체를 숫자형으로 변경하면 타임스탬프(`date.getTime()`을 호출 시 반환되는 값)가 됩니다.

```js run
let date = new Date();
alert(+date); // 타임스탬프(date.getTime()를 호출한 것과 동일함)
```

이를 응용하면 날짜에 마이너스 연산자를 적용해 밀리초 기준 시차를 구할 수 있습니다.

시차를 측정해 나만의 스톱워치를 만들어봅시다.

```js run
let start = new Date(); // 측정 시작

// 원하는 작업을 수행
for (let i = 0; i < 100000; i++) {
  let doSomething = i * i * i;
}

let end = new Date(); // 측정 종료

alert(`반복문을 모두 도는데 ${end - start} 밀리초가 걸렸습니다.`);
```

## Date.now()

**`Date` 객체를 만들지 않고도 시차를 측정할 방법이 있습니다. 그래서 성능이 더 좋습니다.**

현재 타임스탬프를 반환하는 메서드 `Date.now()`를 응용하면 됩니다.

`Date.now()`는 `new Date().getTime()`과 의미론적으로 동일하지만 중간에 `Date` 객체를 만들지 않는다는 점이 다릅니다. 따라서 `new Date().getTime()`를 사용하는 것보다 빠르고 가비지 컬렉터의 일을 덜어준다는 장점이 있습니다.

자바스크립트를 사용해 게임을 구현한다던가 전문분야의 애플리케이션을 구현할 때와 같이 성능이 중요한 경우에 `Date.now()`가 자주 활용됩니다. 물론 편의를 위해 활용되기도 하죠.

위 예시를 `Date.now()`를 사용해 변경하면 성능이 더 좋습니다.

```js run
*!*
let start = Date.now(); // 1970년 1월 1일부터 현재까지의 밀리초
*/!*

// 원하는 작업을 수행
for (let i = 0; i < 100000; i++) {
  let doSomething = i * i * i;
}

*!*
let end = Date.now(); // done
*/!*

alert( `반복문을 모두 도는데 ${end - start} 밀리초가 걸렸습니다.` ); // Date 객체가 아닌 숫자끼리 차감함
```

## Date.parse와 문자열

메서드 [Date.parse(str)](mdn:js/Date/parse)를 사용하면 문자열에서 날짜를 읽어올 수 있습니다.

`YYYY-MM-DDTHH:mm:ss.sssZ`

단, 문자열의 형식은 `YYYY-MM-DDTHH:mm:ss.sssZ`처럼 생겨야 합니다.

- `YYYY-MM-DD` -- 날짜(연-월-일)
- `"T"` -- 구분 기호로 쓰임
- `HH:mm:ss.sss` -- 시:분:초.밀리초
- `'Z'`(옵션) -- `+-hh:mm` 형식의 시간대를 나타냄. `Z` 한 글자인 경우엔 UTC+0을 나타냄

`YYYY-MM-DD`, `YYYY-MM`, `YYYY`같이 더 짧은 문자열 형식도 가능합니다.

위 조건을 만족하는 문자열을 대상으로 `Date.parse(str)`를 호출하면 문자열과 대응하는 날짜의 타임스탬프가 반환됩니다.
**문자열의 형식이 조건에 맞지 않은 경우엔 `NaN`이 반환됩니다.**

예시:

```js run
let ms = Date.parse("2012-01-26T13:51:50.417-07:00");

alert(ms); // 1327611110417  (타임스탬프)
```

`Date.parse(str)`를 이용하면 타임스탬프만으로도 새로운 `Date` 객체를 바로 만들 수 있습니다.

```js run
let date = new Date(Date.parse("2012-01-26T13:51:50.417-07:00"));

alert(date);
```

## 요약

- 자바스크립트에선 [Date](mdn:js/Date) 객체를 사용해 날짜와 시간을 나타냅니다. `Date` 객체엔 '날짜만' 혹은 '시간만' 저장하는 것은 불가능하고, 항상 날짜와 시간이 함께 저장됩니다.
- 월은 0부터 시작합니다(0은 1월을 나타냅니다).
- 요일은 `getDay()`를 사용하면 얻을 수 있는데, 요일 역시 0부터 시작합니다(0은 일요일을 나타냅니다).
- 범위를 넘어가는 구성요소를 설정하려 할 때 `Date` 자동 고침이 활성화됩니다. 이를 이용하면 월/일/시간을 쉽게 날짜에 추가하거나 뺄 수 있습니다.
- 날짜끼리 빼는 것도 가능한데, 이때 두 날짜의 밀리초 차이가 반환됩니다. 이게 가능한 이유는 `Date` 가 숫자형으로 바뀔 때 타임스탬프가 반환되기 때문입니다.
- `Date.now()`를 사용하면 현재 시각의 타임스탬프를 빠르게 구할 수 있습니다.

자바스크립트의 타임스탬프는 초가 아닌 밀리초 기준이라는 점을 항상 유의하시기 바랍니다.

간혹 밀리초보다 더 정확한 시간 측정이 필요할 때가 있습니다. 자바스크립트는 마이크로초(1/1,000,000초)를 지원하진 않지만 대다수의 호스트 환경은 마이크로초를 지원합니다. 브라우저 환경의 메서드 [performance.now()](mdn:api/Performance/now)는 페이지 로딩에 걸리는 밀리초를 반환해주는데, 반환되는 숫자는 소수점 아래 세 자리까지 지원합니다.

```js run
alert(`페이지 로딩이 ${performance.now()}밀리초 전에 시작되었습니다.`);
// 얼럿 창에 "페이지 로딩이 34731.26000000001밀리초 전에 시작되었습니다."와 유사한 메시지가 뜰 텐데
// 여기서 '.26'은 마이크로초(260마이크로초)를 나타냅니다.
// 소수점 아래 숫자 세 개 이후의 숫자는 정밀도 에러때문에 보이는 숫자이므로 소수점 아래 숫자 세 개만 유효합니다.
```

Node.js에선 `microtime` 모듈 등을 사용해 마이크로초를 사용할 수 있습니다. 자바스크립트가 구동되는 대다수의 호스트 환경과 기기에서 마이크로초를 지원하고 있는데 `Date` 객체만 마이크로초를 지원하지 않습니다.
