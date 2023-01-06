# 프로퍼티 어트리뷰트

## 내부 슬롯과 내부 메서드

내부 슬롯과 내부 메서드는 자바스크립트 엔진의 구현 알고리즘을 설명하기 위해 ECMAscript 사양에서 사용하는 의사 프로퍼티와 의사 메서드다. ECMAscript 사양에 등장하는 이중 대괄호로 감싼 이름들이 내부 슬롯과 내부 메서드다.

내부 슬롯과 내부 메서드는 ECMAscript 사양에 정의된 대로 구현되어 자바스크립트 엔진에서 실제로 동작 하지만 개발자가 직접 접근할 수 있도록 외부로 공개된 객체의 프로퍼티는 아니다. 즉, 내부 슬롯과 내부 메서드는 자바스크립트 엔진의 내부 로직이므로 원칙적으로 자바스크립트는 내부 슬롯과 내부 메서드에 직접적으로 호출할 수 있는 방법을 제공하지 않는다. 단, 일부 내부 슬롯과 내부 메서드에 한하여 간접적으로 접근할 수 있는 수단을 제공한다.

모든 객체는 `[[Prototpype]]` 이라는 내부 슬롯을 갖는다. 내부 슬롯은 자바스크립트 엔진의 내부로직이므로 원칙적으로 직접 접근할 수 없지만 [[Prototype]] 내부 슬롯의 경우, `__proto__` 를 통해 간적접으로 접근 가능

```jsx
const o ={};

//내부 슬롯은 자바스크립트 엔진의 내부 로직이므로 직접 접근할 수 없다.
o.[[Prototpye]] // Uncaught SyntaxError: Unexpected token '['
//단, 일부 내부 슬롯과 내부 메서드에 한하여 간접적으로 접근할 수 있는 수단을 제공하기는 한다.

o.__proto__ //Object.prototype
```

---

## 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체

자바스크립트 엔진은 프로퍼티를 생성할 때 프로퍼티의 상태를 나타내는 프로퍼티 어트리뷰트를 기본값으로 자동 정의한다. 프로퍼티의 상태란 프로퍼티의 값, 값의 갱신 가능 여부, 열거 가능 여부, 재정의 가능 여부를 말한다.

프로퍼티 어트리뷰트는 자바사크립트 엔진이 관리하는 내부 상태 값인 내부 슬롯 [[value]],[[Writable]],[[Enuumerable]],[[Configurable]]이다. 따라서 프로퍼티 어트리뷰트에 직접 접근할 수 없지만 object.getOwnPropertyDescriptor 메서드를 사용하여 간접적으로 확인할 수는 있다.

```jsx
const person ={
	name:'Park'
};

//프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체를 반환
console.log(Object.getOwnPropertyDescriptor(person,'name');
//{value:"Park", writable:true, enumerable:true,configurable:true}
```

Object.getOwnPropertyDescriptor 메서드를 호출할 때 첫 번째 매개변수에는 객체의 참조를 전달하고, 두 번째 매개변수에는 프로퍼티 키를 문자열로 전달. 이때 Object.getOwnPropertDescriptor 메서드는 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체를 반환. 만약 존재하지 않는 프로퍼티나 상속받은 프로퍼티에 대한 프로퍼티 디스크립터를 요구하면 undefiend가 반환

Object.getOwnPropertyDescriptor 메서드는 하나의 프로퍼티에 대해 프로퍼티 디스크립터 객체를 반환하지만 ES8에서 도입된 obejct.getOwnPropertDescriptor 메서드는 모든 프로퍼티의 프로퍼티 어트리뷰트정보를 제공하는 프로퍼티 디스크립터 객체를 반환

```jsx
const person = {
  name: "park",
};

//프로퍼티 동적 생성
person.age = 20;

//모든 프로퍼티의 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체들을 반환
console.log(Object.getOwnPropertyDescriptors(person));
/*
{
	name:{ value:"park", writable:true, enumerable:true, configurable:true},
	age:{value:20, writable:true, enumerable:true, configurable:true}
}
*/
```

---

## 데이터 프로퍼티와 접근자 프로퍼티

프로퍼티는 데이터 프로퍼티와 접근자 프로퍼티로 구분할 수 있다.

- 데이터 프로퍼티

  키와 값으로 구성된 일반적인 프로퍼티다.

- 접근자 프로퍼티
  자체적으로는 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 접근자 함수로 구성된 프로퍼티다.

### 데이터 프로퍼티

데이터 프로퍼티는 다음과 같은 프로퍼티 어트리뷰를 갖는다. 이 프로퍼티 어트리뷰트는 자바스크립트 엔진이 프로퍼티를 생성할 때 기본값으로 자동 정의

프로퍼티 어트리뷰트

[[value]]

프로퍼티 디스크립터 객체의 프로퍼티

value

설명

- 프로퍼티 키를 통해 프로퍼티 값에 접근하면 반환되는 값
- 프로퍼티 키를 통해 프로퍼티 값을 변경하면 [[value]]에 값을 재할당 한다. 이때 프로퍼티가 없으면 프로퍼티를 동적 생성하고 생성된 프로퍼티의 [[value]]에 값을 저장한다.

프로퍼티 어트리뷰트

[[Writable]]

프로퍼티 디스크립터 객체의 프로퍼티

writable

설명

- 프로퍼티 값의 변경 가능 여부를 나타내며 불리언 값을 갖는다.
- [[Writable]]의 값이 false인 경우 해당 프로퍼티의 [[value]]의 값을 변경할 수 없는 읽기 전용 프로퍼티가 된다.

프로퍼티 어트리뷰트

[[Enumberable]]

프로퍼티 디스크립터 객체의 프로퍼티

Enumberable

설명

- 프로퍼티의 열거 가능 여부를 나타내며 불리언 값을 갖는다.
- [[Enumberable]]의 값이 false인 경우 해당 프로퍼티는 for…in문이나 object.keys메서등으로 열거할 수 없다.

프로퍼티 어트리뷰트

[[Configurable]]

프로퍼티 디스크립터 객체의 프로퍼티

Configurable

설명

- 프로퍼티의 열거 가능 여부를 나타내며 불리언 값을 갖는다.
- [[Configurable]]의 값이 false인 경우 해당 프로퍼티의 삭제, 프로퍼티 어트리뷰트 값의 변경이 금지된다. 단 [[Writable]]이 true인 경우 [[value]]의 변경과 [[Writable]]을 false로 변경하는 것은 허용

```jsx
const person ={
	name:'Park'
};
//프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체를 취득한다.
console.log(Object.getOwnPropertyDescriptor(person,'name');
//	name:{ value:"park", writable:true, enumerable:true, configurable:true}
```

Object.getOwnPropertyDescriptor 메서드가 반환한 프로퍼티 디스크립터 객체를 살펴보면 value 프로퍼티의 값은 ‘Park’이다. 이것은 프로퍼티 어트리뷰트 [[value]]의 값이 ‘Park’인 것을 의미한다. 그리고 Writable,Enumberable,Configurable 프로퍼티의 값은 모두 true다. 이것은 프로퍼티 어트리뷰트 [[Writable]],[[Enumberable]],[[Configurable]]의 값이 모두 true인 것을 의미

이처럼 프로퍼티가 생성될 때 [[value]]의 값은 프로퍼티 값으로 초기화되며 [[Writable]],[[Enumberable]],[[Configurable]]의 값은 true로 초기화된다.

```jsx
const person = {
  name: "park",
};

//프로퍼티 동적 생성
person.age = 20;

console.log(Object.getOwnPropertyDescriptors(person));
/*
{
	name:{ value:"park", writable:true, enumerable:true, configurable:true},
	age:{value:20, writable:true, enumerable:true, configurable:true}
}
*/
```

### 접근자 프로퍼티

접근자 프로퍼티는 자체적으로 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수로 구성된 프로퍼티

접근자 프로퍼티는 다음과 같은 프로퍼티 어트리뷰트를 갖는다.

프로퍼티 어트리뷰트

[[get]]

프로퍼티 디스크립터 객체의 프로퍼티

get

설명

접근자 프로퍼티를 통해 데이터 프로퍼티의 값을 읽을 때 호출되는 접근자 함수다. 즉, 접근자 프로퍼티 키로 프로퍼티 값에 접근하면 프로퍼티 어트리뷰트 [[get]]의 값, 즉 getter 함수가 호출되고 그 결과가 프로퍼티 값으로 반환

프로퍼티 어트리뷰트

[[set]]

프로퍼티 디스크립터 객체의 프로퍼티

set

설명

접근자 프로퍼티를 통해 데이터 프로퍼티의 값을 저장할 때 호출되는 접근자 함수다. 즉 접근자 프로퍼티 키로 프로터티 값을 저장하면 프로퍼티 어트리뷰트 [[set]]의 값, 즉 setter 함수가 호출되고 그 결과가 프로퍼티 값으로 저장

접근자 함수는 getter/setter 함수라고도 부른다. 접근자 프로퍼티는 getter와 setter 함수를 모두 정의할 수도 있고 하나만 정의할 수도 있다.

```jsx
const person ={
	//데이터 프로퍼티
	firstName:'Ungmo',
	lastName:'Park',
	//fullName은 접근자 함수로 구성된 접근자 프로퍼티다.
	//getter 함수
	get fullName(){
		return `${this.firstName}${this.lastName}`;
	},
	//setter 함수
	set fullName(){
		//배열 디스트럭처링 할당
		[this.firstName, this.lastName] = name.split('');
	}
};

// 데이터 프로퍼티를 통한 프로퍼티 값의 참조
console.log(person.firstName + ''+person.lastName); // Ungmo Park

//접근자 프로퍼티를 통한 프로퍼티 값의 저장
// 접근자 프로퍼티 fullName에 값을 저장하면 setter 함수가 호출된다.
person.fullName = "jinhyeon Park"
console.log(person); // {fistName:"jinhyeon", lastName:"Park"}

//접근자 프로퍼티를 통한 프로퍼티 값의 참조
// 접근자 프로퍼티 fullname에 접근하면 getter 함수가 호출된다.
console.log(person.fullName); // jinhyeon Park

//firstName은 데이터 프로퍼티다.
//데이터 프로퍼티는 [[value]], [[writable]], [[Enumberable]],[[Configurable]]
//프로퍼티 어트리뷰트를 갖는다.
let descriptor = Object.getOwnPropertyDescriptor(person,'firstName');
console.log(descriptor);

//	name:{ value:"jinhyeon", writable:true, enumerable:true, configurable:true},

//fullName은 접근자 프로퍼티다.
//접근자 프로퍼티는 [[get]],[[set]],[[Enumberable]],[[Configurable]]
//프로퍼티 어트리뷰트를 갖는다.
descriptor = Object.getOwnPropertyDescriptor(person,'fullName');
console.log(descriptor);
//{get:f,set:f,enumerable:true, configurable:true}
```

person 객체의 firstName과 lastName 프로퍼티는 일반적인 데이터 프로퍼티다. 메서드 앞에 get, set이 붙은 메서드가 잇는데 이것들이 바로 getter와 setter함수이고, getter/setter 함수의 이름이 fullName이 접근자 프로퍼티다. 접근자 프로퍼티는 자체적으로 값(프로퍼티 어트리뷰트 [[Value]])을 가지지 않으며 다만 데이터 프로퍼티의 값을 읽거나 저장할때 관여할 뿐

이를 내부 슬롯/메서드 관점에서 설명하면 다음과 같다. 접근자 프로퍼티 fullName으로 프로퍼티 값에 접근하면 내부적으로 [[get]] 내부 메서드가 호출되어 다음과 같이 동작한다.

1.  프로퍼티 키가 유효한지 확인. 프로퍼티 키는 문자열 또는 심벌이어야 한다. 프로퍼티 키 “fullName”은 문자열이므로 유효한 프로퍼티 키다.
2.  프로토타입 체인에서 프로퍼티를 검색한다. person 객체에 fullName 프로퍼티가 존재한다.
3.  검색된 fullName 프로퍼티가 데이터 프로퍼팅니지 접근자 프로퍼티인지 확인한다. fullName 프로퍼티는 접근자 프로퍼티다.
4.  접근자 프로퍼티 fullName의 프로퍼티 어트리뷰트 [[get]]의 값은Object.getOwnPropertyDescriptor 메서드가 반환하는 프로퍼티 디스크립터 객체의 get프로퍼티 값과 같다.

<aside>
💡 프로토타입은 어떤 객체의 상위(부모)객체의 역할을 하는 객체다. 프로토타입은 하위(자식) 객체에게 자신의 프로퍼티와 메서드를 상속한다. 프로토타입 객체의 프로퍼티나 메서드를 상속받은 하위 객체는 자신의 프로퍼티 또는 메서드인 것처럼 자유롭게 사용할 수 있다.
프로토타입 체인은 프로토타입이 단방향 링크드 리스트 형태로 연결되어 있는 상속 구조를 말한다. 객체의 프로퍼티나 메서드에 접근하려고 할 때 해당 겍체에 접근하려는 프로퍼티 또는 메서드가 없다면 프로포타입 체인을 따라 프로포타입의 프로퍼티나 메서드를 차례대로 검색한다.

</aside>

접근자 프로퍼티와 데이터 프로퍼티를 구별하는 방법은 다음과 같다.

```jsx
//일반 객체 __proto__는 접근자 프로퍼티다.
Object.getOwnPropertyDescriptor(Object.prototype, "__proto__");
//{get:f,set:f, ennumrable:false, configurable:true}

//함수 객체의 prototype은 데이터 프로퍼티다.
Object.getOwnPropertyDescriptor(function () {}, "prototype");
//{value:{...}, writable:true, enumerable: false,configurable:false}
```

Object.getOwnPropertyDescriptor 메서드가 반환한 프로퍼티 어트리뷰트를 객체로 표현한 프로퍼티 디스크립터 객체를 유심히 살펴보자 접근자 프로퍼티와 데이터 프로퍼티의 프로퍼티 디스크립터 객체의 프로퍼티가 다른 것을 알 수 있다.

---

## 프로퍼티 정의

프로퍼티 정의란 새로운 프로퍼티를 추가하면서 프로퍼티 어트리뷰트를 명시적으로 정의하거나, 기준 프로퍼티의 프로퍼티 어트리뷰트를 재정의하는 것을 말한다. 예를 들어, 프로퍼티 값을 갱신 가능하도록 할 것인지, 프로퍼티를 열거 가능하도록 할 것인지, 프로퍼티를 재정의 가능하도록 할 것인지 정의할 수 있다. 이를 통해 객체의 프로퍼티가 어떻게 동작해야 하는지 명확히 정의할 수 있다.

Object.defineProperty 메서드를 사용하면 프로퍼티의 어트리뷰트를 정의할 수 있다. 인수로는 객체의 참조와 데이터 프로퍼티의 키인 문자열, 프로퍼티 디스크립터 객체를 전달한다.

```jsx
const person ={};

//데이터 프로퍼티 정의
Object.defineProperty(person, 'firstName',{
	value:'123',
	wrtiable:true,
	enumberable:true,
	configurable:true
});

	Object.defineProperty(person, 'lastName',{
	value:"park"
});

let descriptor = Object.getOwnPropertyDescriptor(person,'firstName');
console.log('firstName',descriptor)
//	name:{ value:"123", writable:true, enumerable:true, configurable:true},

//디스크립터 객체의 프로퍼티를 누락시키면 undefined, false가 기본값이다.
descriptor = Object.getOwnPropertyDescriptor(person,'lastName');
console.log('lastName',descriptor)

//	name:{ value:"park", writable:true, enumerable:true, configurable:true},

//[[enumerable]]의 값이 false인 경우
// 해당 프로퍼티는 for..in 문이나 object.keys등으로 열거할 수 없다.
//lastName 프로퍼티는 [[enumerable]]의 값이 false이므로 열거되지 않는다.
console.log(Object.keys(person)); //["firstName"]

//[[writable]]의 값이 false인 경우 해당 프로퍼티의 [[value]]의 값을 변경할 수 없다.
//lastName 프로퍼티는 [[writable]]의 값이 false이므로 값을 변경할 수 없다.
//이때 값을 변경하면 에러는 발생하지 않고 무시된다.
person.lastName="kim";

//[[configurable]]의 값이 false인 경우 해당 프로퍼티를 재정의할 수 없다.
//Object.defineProperty(person,'lastName', {enumberable:true});
//Uncaught TypeError: cannot redefine property:lastName
descriptor = Object.getOwnPropertyDescriptor(person,'lastName');
console.log('lastName',descriptor)
//	lastName { value:"park", writable:false, enumerable:false, configurable:false}

//접근자 프로퍼티 정의
Object.defineProperty(person,'fullName',{
	//getter 함수
	get(){
		return `${this.firstName} ${this.lastName}`;
	}
	//setter 함수
	set(name){
	[this.firstName, this.lastName] = name.split('');
	},
	enumerable:true,
	configurable:true
});

descriptor = Object.getOwnPropertyDescriptor(person,'fullName');
console.log('fullName',descriptor);

person.fullName = '123 park';
console.log(person);
```

Object.defineProperty 메서드로 프로퍼티를 정의할 때 프로퍼티 디스크립터 객체의 프로퍼티를 일부 생략할 수 있다. 프로퍼티 디스크립터 객체에서 생략된 어트리뷰트는 다음과 같이 기본값이 적용된다.

프로퍼티 디스크립터 객체의 프로퍼티

value

대응하는 프로퍼티 어트리뷰트

[[value]]

생략했을 때의 기본값

undefined

프로퍼티 디스크립터 객체의 프로퍼티

get

대응하는 프로퍼티 어트리뷰트

[[get]]

생략했을 때의 기본값

undefined

프로퍼티 디스크립터 객체의 프로퍼티

set

대응하는 프로퍼티 어트리뷰트

[[set]]

생략했을 때의 기본값

undefined

프로퍼티 디스크립터 객체의 프로퍼티

Writable

대응하는 프로퍼티 어트리뷰트

[[writable]]

생략했을 때의 기본값

false

프로퍼티 디스크립터 객체의 프로퍼티

[[Enumberable]]

대응하는 프로퍼티 어트리뷰트

[[Enumberable]]

생략했을 때의 기본값

false

프로퍼티 디스크립터 객체의 프로퍼티

Configurable

대응하는 프로퍼티 어트리뷰트

Configurable

생략했을 때의 기본값

false

Object.definedProperty 메서드는 한번에 하나의 프로퍼티만 정의할 수 있다. Object.definedProperties 메서드를 사용하면 여러 개의 프로퍼티를 한번에 정의할 수 있다.

---
