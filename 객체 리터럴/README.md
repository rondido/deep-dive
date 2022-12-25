# 객체 리터럴

## 객체란?

자바스크립트는 객체 기반의 프로그래밍 언어이며, 자바스크립트를 구성하는 거의 “모든 것”이 객체다. 원시 값을 제외한 나머지 값(함수,배열, 정규 표현식 등)은 모두 객체다.

원시 타입은 단 하나의 값만 나타내지만 객체 타입은 다양한 타입의 값(원시 값 또는 다른 객체)을 하나의 단위로 구성한 복합적인 자료구조다. 또한 원시 타입의 값, 즉 원시 값은 변경 불가능한 값이지만 객체 타입의 값, 즉 객체는 변경 가능한 값이다.

객체는 0개 이상의 프로퍼티로 구성된 집합이며, 프토퍼티는 키와 값으로 구성

객체는 프로퍼티와 메서드로 구성된 집합체

- 프로퍼티: 객체의 상태를 나타내는 값
- 메서드: 프로퍼티(상태 데이터)를 참조하고 조작할 수 있는 동작

객체는 객체의 상태를 나타내는 값(프로퍼티)과 프로퍼티를 참조하고 조작할 수 있는 동작(메서드)을 모두 포함할 수 있기 때문에 상태와 동작을 하나의 단위로 구조화할 수 있어 유용

---

## 객체 리터럴에 의한 객체 생성

c++나 자바 같은 클래스 기반 객체지향 언어는 클래스를 사전에 정의하고 필요한 시점에 new 연산자와 함께 생성자를 호출하여 인스턴스를 생성하는 방식으로 객체를 생성

<aside>
💡 인스턴스란 클래스에 의해 생성되어 메모리에 저장된 실체를 말한다. 객체 지향 프로그래밍에서 객체는 클래스와 인스턴스를 포함한 개념. 클래스는 인스턴스를 생성하기 위한 템플릿의 역할을 한다. 인스턴스는 객체가 메모리에 저장되어 실제로 존재하느 것에 초첨을 맞춘 용어

</aside>

자바스크립트는 프로토타입 기반 객체지향 언어로서 클래스 기반 객체지향 언어와는 달리 다양한 객체 생성 방법을 지원

- 객체 리터럴
- Object 생성자 함수
- 생성자 함수
- Object.create 메서드
- 클래스(ES6)

```jsx
var person = {
	name:'Lee',
	sayHello:function (){
		console.log(`Hello! My name is ${this.name}.`);
	}
}

console.log(typeof person); //object
console.log(person); // {name:"Lee", sayHello:f}
```

---

## 프로퍼티

객체는 프로퍼티의 집합이며, 프로퍼티는 키와 값으로 구성

```jsx
var person ={
	name:'Lee',
	age:20
}
```

프로퍼티를 나열할 때는 쉼표(,)로 구분한다. 일반적으로 마지막 프로퍼티 뒤에는 쉼표를 사용하지 않으나 사용해도 좋다.

프로퍼티 키와 프로퍼티 값으로 사용할 수 있는 값은 다음과 같다.

- 프로퍼티 키: 빈 문자열을 포함하는 모든 문자열 또는 심벌 값
- 프로퍼티 값: 자바스크립트에서 사용할 수 있는 모든 값

식별자 네이밍 규칙을 따르지 않는 이름에는 반드시 따옴표를 사용해야 한다.

```jsx
var foo ={
	 '' : '' //빈 문자열도 프로퍼티 키도 사용할 수 있다.
}
console.log(foo); // {"":""}
```

프로퍼티 키에 문자열이나 심벌 값 외의 값을 사용하면 암묵적 타입 변환을 통해 문자열이 된다. 

이미 존재하는 프로퍼티 키를 중복 선언하면 나중에 선언한 프로퍼티가 먼저 선언한 프로퍼티를 덮어쓴다.

```jsx
var foo = {
	name:'Lee',
	name:'Kim'
}

console.log(foo); //{name:"kim"}
```

---

## 메서드

자바스크립트에서 사용할수 있는 모든 값은 프로퍼티 값으로 사용할 수 있다고 했다. 아직 살펴보지 않았지만 자바스크립트의 함수는 객체(일급 객체)다. 따라서 함수는 값으로 취급할 수 있기 때문에 프로퍼티 값으로 사용할 수 있다.

프로퍼티 값이 함수일 경우 일반 함수와 구분하기 위해 메서드라 부른다. 즉 메서드는 객체에 묶여 있는 함수를 의미한다.

```jsx
var circle = {
	radius: 5,
	getDiameter:function (){
		return 2 * this.radius; // this는 circle을 가리킨다.
	}
}

console.log(circle.getDiameter()); //10
```

메서드 내부에서 사용한 this 키워도는 개체 자신을 가리키는 참조변수다.

---

## 프로퍼티 접근

프로퍼티에 접근하는 방법은 다음과 같이 두 가지다.

- 마침표 프로퍼티 접근 연산자를 마침표 표기법
- 대괄호 프로퍼티 접근 연산자를 사용하는 대괄호 표기법

```jsx
var person = {
	name:'Park'
};

console.log(person.name); //Park

console.log(person['name']); //Park
```

대괄호 표기법을 사용하는 경우 대괄호 프로퍼티 접근 연산자 내부에 지정하는 프로퍼티 키는 반드시 따음표로 감싼 문자열이여야 한다. 대괄호 프로퍼티 접근 연산자 내에 따옴표를 감싸지 않는 이름을 프로퍼티 키로 사요하면 에러가 발생

```jsx
var person = {
	name:'Park'
};

console.log(person[name]); //ReferenceError:name is not defined
```

객체에 존재하지 않는 프로퍼티에 접그하면 undefiend를 반환

```jsx
var person ={
	'last-name' : 'Park',
	1:10
}

person.'last-name'; // SyntaxError:unexpected string
person.last-name; // 브라우저 환경: NaN
									//node.js  환경: ReferenceError: name is not defiend
person[last-name]; //ReferenceError: last is not defiend
person['last-name']; //Park

//프로퍼티 키가 숫자로 이뤄진 문자열인 경우 따옴표를 생략할 수 있다.
person.1; // SyntaxError:unexpected number
person.'1'; //SyntaxError:unexpected string
person[1]; // 10 : person[1] -> person['1']
person['1']; // 10
```

---

## 프로퍼티 값 갱신

이미 존재하는 프로퍼티에 값을 할당하면 프로퍼티 값이 갱신된다.

```jsx
var person ={
	name:'Lee'
}

//person 객체에 name 프로퍼티가 존재하므로 name 프로퍼티의 값이 갱신
person.name= 'Kim';

console.log(person) // {name:"kim"}
```

---

## 프로퍼티 동적 생성

존재하지 않는 프로퍼티에 값을 할당하면 프로퍼티가 동적으로 생성되어 추가되고 프로퍼티 값이 할당된다.

```jsx
var person ={
	name:'Lee'
}
//person 객체에는 age 프로퍼티가 존재하지 않는다.
//따라서 person 객체에 age 프로퍼티가 동적으로 생성되고 값이 할당
person.age = 20;

console.log(person); // {name:"park", age:20}
```

---

## 프로퍼티 삭제

delete 연산자는 객체의 프로퍼티를 삭제한다. 이때 delete 연산자의 피연산자는 프로퍼티 값에 접근할 수 있는 표현식어야 한다. 만약 존재하지 않는 프로퍼티를 삭제하면 에러 없이 무시

```jsx
var person ={
	name:'Lee'
}

person.age = 20;
//person 객체에는 age 프로퍼티가 존재한다.
//따라서 delete 연산자로 age 프로퍼티를 삭제
delete person.age;

//person 객체에 address 프로퍼티가 존재하지 않는다.
//따라서 delete 연산자로 address 프로퍼티를 삭제할 수 없다. 이때 에러가 발생하지 않는다.
delete person.address;

console.log(person); // {name:"Lee"}
```

---

## ES6에서 추가된 객체 리터럴의 확장 기능

### 프로퍼티 축약 표현

```jsx
//ES6
let x = 1, y=2;

//프로퍼티 축약 표현

const obj = {x,y};

console.log(obj); //{x:1,y:2}
```

### 계산된 프로퍼티 이름

문자열 또는 문자열로 타입 변환할 수 있는 값으로 평가되는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수도 있다. 단, 프로퍼티 키로 사용할 표현식을 대괄호([…])로 묶어야 한다. 이를 계산된 프로퍼티 이름이라 한다.

```jsx
var prefix = 'prop';
var i =0;
var obj={};

obj[prefix + '-' + ++i] =i;
obj[prefix + '-' + ++i] =i;
obj[prefix + '-' + ++i] =i;

console.log(obj); //{prop-1:1, prop-2:2,prop-3:3}
```

ES6에서는 객체 리터럴 내부에서도 계산된 프로퍼티 이름으로 프로퍼티 키를 동적 생성할 수 있다.

```jsx
//ES6
const prefix = 'prop';
var i =0;

var obj ={
	[prefix + '-' + ++i] =i;
	[prefix + '-' + ++i] =i;
	[prefix + '-' + ++i] =i;
};

console.log(obj); //{prop-1:1, prop-2:2,prop-3:3}
```

### 메서드 축약 표현

ES5에서 메서드를 정의하려면 프로퍼티 값으로 함수를 할당

```jsx
var obj ={
	name:'Park',
	sayHi: function(){
		console.log('Hi' + this.name);
	}
}
obj.sayHi(); // Hi! Park
```

ES6에서는 메서드를 정의할 떄 function 키워드를 생략한 축약 표현을 사용할 수 있다.

```jsx
var obj ={
	name:'Park',
	sayHi(){
		console.log('Hi' + this.name);
	}
}
obj.sayHi(); // Hi! Park
```

---