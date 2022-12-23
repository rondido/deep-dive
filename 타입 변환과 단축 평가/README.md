# 타입 변환과 단축 평가

## 타입 변환이란?

자바스크립트의 모든 값은 타입이 있다. 값의 타입은 개발자의 의도에 따라 다른 타입으로 변환할 수 있다. 개발자가 의도적으로 값의 타입을 변환하는 것을 명시적 타입 변환 또는 타입 캐스팅이라 한다.

```jsx
var x = 10;

var str = x.toString();
console.log(typeof str, str); //string 10

console.log(typeof x, x); //number 10
```

개발자의 의도와는 상관없이 표현식을 평가하는 도중에 자바스크립트 엔진에 의해 암묵적으로 타입이 자동변환기도 한다. 이를 암묵적 타입 변환 또는 타입 강제 변환이라 한다.

```jsx
var x = 10;
var str = x  + '';
console.log(type of str,str); // string 10
```

명시적 타입 변환이나 암묵적 타입 변환이 기존 원시 값을 직접 변경하는 것은 아니다. 원시 값은 변경 불가능한 값이므로 변경할 수 없다. 타입 변환이란 기존 원시 값을 사용해 다른 타입의 새로운 원시 값을 생성하는 것

암묵적 타입 변환은 기존 변수 값을 재당할하여 변경하는 것이 아니다. 자바스크립트 엔진은 표현식을 에러 없이 평가하기 위해 피연산자의 값을 암묵적 타입 변환해 새로운 타입의 값을 만들어 단 한번 사용하고 버림.

---

## 암묵적 타입 변환

자바스크립트 엔진은 표현식을 평가할 때 개발자의 의도와는 상관없이 코드의 문맥을 고려해 암묵적으로 데이터 타입을 강제 변환 할 때가 있다.

```jsx
"10" + 2; // '102'
5 * "10"; // 50
```

프로그래밍 언어에 따라 에러를 발생시키도 하지만 자바스크립트는 가급적 에러를 발생시키지 않도록 암묵적 타입 변환을 통해 표현식을 평가

### 문자열 타입으로 변환

```jsx
1 + "2"; // "12"
```

위 예제의 + 연산자는 피연산자 중 하나 이상이 문자열이므로 문자열 연결 연산자로 동작한다. 문자열 연산자의 역할은 문자열 값을 만드는 것 따라서 문자열 연산자의 모든 피연산자는 코드의 문맥상 모두 문자열 타입이어야 함.

자바스크립트 엔진은 문자열 연결 연산자 표현식을 평가하기 위해 문자열 연결 연산자의 피연산자 중에서 문자열 타입이 아닌 피연산자를 문자열 타입으로 암묵적 타입 변환

### 숫자 타입으로 변환

```jsx
1 - "1"; // 0
1 * "10"; // 10
1 / "one"; // NaN
```

위 예제에서 사용한 연산자는 모두 산술 연산자 산술 연산자의 역할은 숫자 값을 만드는 것

산술 연산자의 모든 피연산자는 코드 문맥상 모두 숫자 타입이어야 함.

자바스크립트 엔진은 산술 연산자 표현식을 평가하기 위해 산술 연산자의 피연산자 중에서 숫자 타입이 아닌 피연산자를 숫자 타입으로 암묵적 타입 변환 이때 피연산자를 숫자 타입으로 변환할 수 없는 경우는 산술 연산을 수행할 수 없으므로 표현식의 평가 결과는 NaN이 된다.

```jsx
"1" > 0; // true
```

비교 연산자의 역할은 불리언 값을 만드는 것 > 비교 연산자는 크기를 비교하므로 모든 피연산자는 코드의 문맥상 모두 숫자 타입어야 함. 자바스크립트 엔진은 비교 연산자 표현식을 평가하기 위해 비교 연산자의 피연산자 중에서 숫자 타입이 아닌 피연산자를 숫자 타입으로 암묵적 타입 변환

---

## 명시적 타입 변환

개발자의 의도에 따라 명시적으로 타입을 변경하는 방법은 다양. 표준 빌트인 생성자 함수(String, Number, Boolean)를 new 연산자 없이 호출하는 방법과 빌트인 메서드를 사용하는 방법

### 문자열 타입으로 변환

문자열 타입이 아닌 값을 문자열 타입으로 변환하는 방법

1. String 생성자 함수를 new 연산자 없이 호출하는 방법
2. Object.prototype.toString메서드를 사용하는 방법
3. 문자열 연결 연산자를 이용하는 방법

```jsx
//string 생성자 함수를 new 연산자 없이 호출하는 방법
// 숫자 타입 -> 문자열타입
String(1); // 1
String(NaN); //NaN
String(Infinity); //Infinity
// 불리언 타입 -> 문자열 타입
String(true); //true
String(false); //false

// Object.prototype.toString 메서드를 사용하는 방법
// 숫자 타입 -> 문자열 타입
(1).toString(); // "1"
NaN.toString(); //"NaN"
Infinity.toString(); //"Infinity"
// 불리언 -> 문자열
true
  .toString()(
    // "true
    false
  )
  .toString(); // false

// 숫자 타입 -> 문자열 타입
1 + ""; // "1"
NaN + ""; // "NaN"
Infinity + ""; // "Infinity"
true + ""; // "true"
false + ""; // "false"
```

### 숫자 타입으로 변환

숫자 타입이 아닌 값을 숫자 타입으로 변환하는 방법

1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
2. parseInt, parseFloat함수를 사용하는 방법(문자열만 숫자 타입으로 변환 가능)
3. +단항 연산자를 이용하는 방법
4. \*산술 연산자를 이용하는 방법

```jsx
Number("0"); //0
Number("-1"); // -1
Number("10.53"); // 10.53
Number(true); // 1
Number(false); // 0

parseInt("0"); //0
parseInt("-1"); // -1
parseFloat("10.53") + // 10.53
  "0"; //0
+"-1"; // -1
+"10.53"; //10.53

+true + // 1
  false; // 0

"0" * 1; //0
"-1" * 1; //-1
"10.53" * 1; //10.53

true * 1; // 1
false * 1; // 0
```

---

### 불리언 타입으로 변환

불리언 타입이 아닌 값을 불리언 타입으로 변환하는 방법

1. Boolean 생성자 함수를 new 연산자 없이 호출
2. ! 부정 논리 연산자를 두 번 사용하는 방법

```jsx
Boolean("x"); //true
Boolean(""); //false
Boolean("false"); //true
Boolean(0); //false
Boolean(1); //true
Boolean(NaN); //false
Boolean(Infinity); //true
Boolean(null); //false
Boolean(undefined); //false
Boolean({}); //true
Boolean([]); //true

//!부정

!!"x"; //true
!!""; //false
!!"false"; //true

!!0; //false
!!1; //true
!!NaN; //false
!!Infinity; //true
!!null; //false
!!undefined; //false
!!{}; //true
!![]; //true
```

---

## 단축 평가

### 논리 연산자를 사용한 단축 평가

```jsx
"Cat" && "Dog"; // "Dog"
```

논리곱(&&) 연산자는 두 개의 피연산자가 모두 true로 평가될 때 true를 반환한다. 논리곱 연산자는 좌항에서 우항으로 평가

첫번째 피연산자 ‘Cat’은 Truthy 값이므로 true로 평가 하지만 이 시점까지는 위 표현식을 평가할 수 없다. 두 번째 피연산자까지 평가해 보아야 위 표현식을 평가. 다시 말해, 두 번째 피연산자가 논리곱 연산자 표현식의 평가 결과를 결정 이때 논리곱 연산자는 논리 연산의 결과를 결정하는 두번째 피연산자, 즉 문자열 ‘Dog’를 그대로 반환

```jsx
"Cat" || "Dog"; //Cat
```

논리합(||) 연산자는 두 개의 피연산자 중 하나만 true로 평가되어도 true를 반환. 논리합 연산자도 좌항에서 우항으로 평가가 진행

첫 번째 피연산자 ‘Cat’은 Truthy 값이므로 true로 평가 이 시점에 두 번째 피연산자까지 평가해 보지 않아도 위 표현식을 평가할 수 있다. 이때 논리합 연산자는 논리 연산의 결과를 결정한 첫 번째 피연산자 즉, 문자열 ‘Cat’을 그대로 반환

이처럼 논리 연산의 결과를 결정하는 피연산자를 타입 변환하지 않고 그대로 반환한다. 이를 단축 평가라 한다. 단축 평가는 표현식을 평가하는 도중에 평가결과가 확정된 경우 나머지 평가 과정을 과정 생략하는 것을 말한다.

### 객체를 가르키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때

객체는 키와 값으로 구성된 프로퍼티의 집합. 객체를 가리키기를 기대하는 변수의 값이 객체가 아니라 null 또는 undefined인 경우 객체의 프로퍼티를 참조하면 타입 에러가 발생 에러가 발생하면 프로그램이 강제 종료

```jsx
var elem = null;
var value = elem.value;
```

단축 평가를 사용하면 에러를 발생시키지 않는다.

```jsx
var elem = null;
var value = elem && elem.value; // null
```

### 함수 매개변수에 기본값을 설정할 때

함수를 호출할 때 인수를 전달하지 않으면 매개변수에는 undefined가 할당. 이때 단축 평가를 사용해 매개변수의 기본값을 설정하면 undefined로 인해 발생할 수 있는 에러를 방지

### 옵셔널 체이닝 연산자

ES11에서 도입된 옵셔널 체이닝 연산자 ?.는 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고 그렇지 않다면 우항의 프로퍼티를 참조

```jsx
var elem = null;

var value = elem?.value;
console.log(value);
undefined;
```

옵셔널 체이닝 연산자 ?.는 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때 유용. 옵셔널 체이닝 연산자?.가 도입되기 이전에는 논리 연산자 &&를 사용한 단축 평가를 통해 변수가 null 또는 undefiend인지 평가

```jsx
var elem = null;

var value = elem && elem.value;
console.log(value);
null;
```

논리 연산자 &&는 좌항 피연산자가 false로 평가되는 Falsy 값(false, undefined, null, 0, -0, NaN,’’)이면 좌항 피연산자를 그대로 반환. 좌항 피연산자가 Falsy 값인 0이나 ‘’인 경우 마찬가지다. 하지만 0 이나 ‘은 객체로 평가될 때도 있다.

```jsx
var str = "";

var length = str && str.length;

console.log(length); // ''
```

하지만 옵셔널 체이닝 연산자 ?.는 좌항 연산자가 false로 평가되는 Falsy 값(false, undefined, null, 0, -0, NaN, ‘’)이라도 null 또는 undefined가 아니면 우항의 프로퍼티를 참조

```jsx
var str = "";
var length = str?.length;
console.log(length); //0
```

### null 병합 연산자

ES11에서 도입된 null 병합 연산자 ??는 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항이 피연산자를 반환 null 병합 연산자 ??는 변수에 기본값을 설정

```jsx
var foo = null ?? "default string";
console.log(foo); //'default string'
```

null 병합 연산자는 ??는 변수에 기본값을 설정할 때 유용하다. null 병합 연산자 ??가 도입되기 전에는 논리 연산자 ||를 사용한 단축 평가를 통해 기본값을 설정 논리 연산자 ||를 사용한 단축 평가의 경우 좌항의 피연산자가 false로 평가되는 falsy 값(false,undefined, null, 0, -1,NaN, ‘’)이면 우항의 피연산자를 반환. 만약 Falsy 값인 0이나 ‘’도 기본값으로서 유효하다면 예기치 않는 동작이 발생

```jsx
var foo = "" || "default string";
console.log(foo); //'default string'
```

하지만 null 병합 연산자 ??는 좌항의 피연산자가 false로 평가되는 Falsy값(false,undefined,nulll,0,-0,NaN,’’)이라도 null 또는 undefiend가 좌항의 피연산자를 그대로 반환

```jsx
var foo = "" ?? "default string";
console.log(foo); //""
```

---
