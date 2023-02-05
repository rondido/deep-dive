# 함수와 일급객체

---

## 일급 객체

---

다음과 같은 조건을 만족하는 객체를 일급 객체라 한다.

1. 무명의 리터럴로 생성할 수 있다. 즉, 런타임에 생성이 가능하다.
2. 변수나 자료구조(객체,배열 등)에 저장할 수 있다.
3. 함수의 매개변수에 전달할 수 있다.
4. 함수의 반환값으로 사용할 수 있다.

```tsx
const increase = function (num) {
  return ++num;
};

const decrease = function (num) {
  return --num;
};

const auxs = { increase, decrease };

function makeCounter(aux) {
  let num = 0;
  return function () {
    num = aux(num);
    return num;
  };
}

const increaser = makeCounter(auxs.increase);
console.log(increaser()); //1
console.log(increaser()); //2

const decreaser = makeCounter(auxs.decrease);
console.log(decreaser()); // -1
console.log(decreaser()); // -2
```

함수가 일급 객체라는 것은 함수를 객체와 동일하게 사용할 수 있다는 의미다. 객체는 값이므로 함수는 값과 동일하게 취급할 수 있다. 따라서 함수는 값을 사용할 수 있는 곳(변수 할당문, 객체의 프로퍼티 값, 배열의 요소, 함수 호출의 인수, 함수 반환문)이라면 어디서든지 리터럴로 정의할 수 있으며 런타임에 함수 객체로 평가된다.

일급 객체로서 함수가 가지는 가장 큰 특징은 일반 객체와 같이 함수의 매개변수에 전달할 수 있으며, 함수의 반환값으로 사용할 수도 있다는 것이다. 이는 함수형 프로그래밍을 가능케 하는 자바스크립트의 장점 중 하나다. 함수는 객체이지만 일반 객체와는 차이가 있다. 일반 객체는 호출할 수 없지만 함수 객체는 호출할 수 있다. 그리고 함수 객체는 일반 객체에는 없는 함수 고유의 프로퍼티를 소유한다.

## 함수 객체의 프로퍼티

---

함수는 객체다. 따라서 함수도 프로퍼티를 가질 수 있다.

```tsx
function square(number) {
  return number * number;
}
console.dir(square);
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/52acb2d9-62a5-49f6-b548-ef9e31bb2180/Untitled.png)

### arguments 프로퍼티

함수 객체의 arguments 프로퍼티 값은 arguments 객체다. arguments 객체는 함수 호출 시 전달된 인수들의 정보를 담고 있는 순회 가능한 유사 배열 객체이며, 함수 내부에서 지역 변수처럼 사용된다. 즉 함수 외부에서는 참조할 수 없다.

함수 객체의 arguments 프로퍼티는 현재 일부 브라우저에서 지원하고 있지만 ES3부터 표준에서 폐지되었다. 따라서 function.arguments와 같은 사용법은 권장되지 않으며 함수 내부에서 지역 변수처럼 사용할 수 있는 arguments 객체를 참조하도록 한다.

```tsx
function multiply(x, y) {
  console.log(arguments);
  return x * y;
}
console.log(multiply()); //NaN
console.log(multiply(1)); //NaN
console.log(multiply(1, 2)); //2
console.log(multiply(1, 2, 3)); //2
```

함수를 정의할 때 선언한 매개변수는 함수 몸체 내부에서 변수와 동일하게 취급된다. 즉, 함수가 호출되면 함수 몸체 내에서 암묵적으로 매개변수가 선언되고 undefined로 초기화된 이후 인수가 할당된다.

선언된 매개변수의 개수보다 인수를 적게 전달했을 경우 인수가 전달되지 않은 매개변수는 undefined로 초기화된 상태를 유지한다. 매개변수의 개수보다 인수를 더 많이 전달한 경우 초과된 인수는 무시한다.

그렇다고 초과된 인수가 그냥 버려지는 것은 아니다. 모든 인수는 암묵적으로 arguments객체의 프로퍼티로 보관된다.

arguments 객체는 인수를 프로퍼티 값으로 소유하며 프로퍼티 키는 인수의 순서를 나타낸다. arguments 객체의 callee 프로퍼티는 호출되어 arguments 객체를 생성한 함수, 즉 함수 자신을 가리키고 arguments 객체의 length 프로퍼티는 인수의 개수를 가리킨다.

선언된 매개변수의 개수와 함수를 호출할 때 전달하는 인수의 개수를 확인하지 않는 자바스크립트의 특성 때문에 함수가 호출되면 인수 개수를 확인하고 이에 따라 함수의 동작을 달리 정의할 필요가 있을 수 있다. 이때 유용하게 사용되는 것이 argumetns 객체다.

argumetns 객체는 매개변수 개수를 확정할 수 없는 가변 인자 함수를 구현할 때 유용하다.

```tsx
function sum() {
  let res = 0;
  for (let i = 0; i < arguments.length; i++) {
    res += argumnets[i];
  }
  return res;
}
console.log(sum()); //0
console.log(sum(1, 2)); //3
console.log(sum(1, 2, 3)); //6
```

arguments 객체는 배열 형태로 인자 정보를 담고 있지만 실제 배열이 아닌 유사 배열 객체다. 유사 배열 객체란 length 프로퍼티를 가진 객체로 for 문으로 순회할 수 있는 객체를 말한다.

유사 배열 객체는 배열이 아니므로 배열 메서드를 사용할 경우 에러가 발생한다. 따라서 배열 메서드를 사용하려면 Function.prototype.call.Function.prototype.apply를 사용해 간접 호출해야 하는 번거로움이 있다.

```tsx
function sum() {
  //arguments 객체를 배열로 변환
  const array = Array.prototype.silce.call(arguments);
  return array.reduce(function (pre, cur) {
    return pre + cur;
  }, 0);
}

console.log(sum(1, 2)); //3
console.log(sum(1, 2, 3, 4, 5)); //15
```

ES6에서는 Rest 파라미터를 도입했다.

```tsx
function sum(...args) {
  return args.reducer((pre, cur) => pre + cur, 0);
}
console.log(sum(1, 2)); //3
console.log(sum(1, 2, 3, 4, 5)); //15
```

### caller 프로퍼티

caller 프로퍼티는 EMCAscript 사양에 포함되지 않은 비표준 프로퍼티다. 이후 표준화될 예정도 없는 프로퍼티이므로 사용하지 말고 참고로만 알아두자. 관심이 없다면 지나쳐도 좋다.

```tsx
function foo(func) {
  return func();
}
function bar() {
  return "caller :" + bar.caller;
}

//브라우저에서의 실행 결과
console.log(foo(bar)); //caller:function foo(func){...}
console.log(bar()); //caller:null
```

함수 호출 foo(bar)의 경우 bar 함수를 foo 함수 내에서 호출했다. 이때 bar 함수의 caller 프로퍼티는 bar 함수를 호출한 foo 함수를 가리킨다. 함수 호출 bar()의 경우 bar 함수를 호출한 함수는 없다. 따라서 caller 프로퍼티는 null을 가리킨다.

### length 프로퍼티

함수 객체의 length 프로퍼티는 함수를 정의할 때 선언한 매개변수의 개수를 가리킨다.

```tsx
function foo() {
  console.log(foo.length); // 0
  function bar(x) {
    return x;
  }
  console.log(bar.length); //1
  function baz(x, y) {
    return x + y;
  }
}
console.log(baz.length); //2
```

arguments 객체의 length 프로퍼티는 인자의 개수를 가리키고, 함수 객체의 length 프로퍼티는 매개 변수의 개수를 가리킨다.

### name 프로퍼티

익명 함수 표현식의 경우 ES5에서 name 프로퍼티는 빈 문자열을 값으로 갖는다. ES6에서는 함수 객체를 가리키는 식별자를 값으로 갖는다.

```tsx
var namedFunc = function foo(){}
console.log(namedFunc.name); //foo

var anonymousFunc = funcion() {}
console.log(anonymousFunc.name); // anonymousFunc

function bar() {}
console.log(bar.name); //bar

```

### proto 접근자 프로퍼티

```tsx
const obj = { a: 1 };

console.log(obj.__proto__ === object.prototype); // true
console.log(obj.hasOwnProperty("a")); // true
console.log(obj.hasOwnProperty("__proto__")); //false
```

### prototype 프로퍼티

prototype 프로퍼티는 생성자 함수로 호출할 수 있는 함수 객체, 즉 constructor만이 소유하는 프로퍼티다.

```tsx
(function () {}).hasOwnProperty('prototype'); //->ture
({}.hasOwnPrototype('prototype');//false
```
