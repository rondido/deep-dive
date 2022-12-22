# 제어문

제어문은 조건에 따라 코드 블록을 실행(조건문)하거나 반복 실행(반복문)할 때 사용한다. 일반적으로 코드는 위에서 아래 방향으로 순차적으로 실행. 제어문을 사용하면 코드의 실행 흐름을 인위적으로 제어할 수 있다.

하지만 코드의 실행 순서가 변경된다는 것은 단순히 위에서 아래로 순차적으로 진행하는 직관적인 코드의 흐름을 혼란스럽게 만든다. 따라서 제어문은 코드의 흐름을 이해하기 어렵게 만들어 가독성을 해치는 단점이 있다.

---

## 블록문

블록문은 0개 이상의 문을 중괄호로 묶은 것으로, 코드 블록 또는 블록이라고 부른다.

자바스크립트는 블록문을 하나의 실행 단위로 취급한다. 블록문은 단독으로 사용할 수 있으나 일반적으로 제어문이나 함수를 정의할 대 사용하는 것이 일반적이다.

```jsx
{
  var foo = 10;
}

var x = 1;
if (x < 10) {
  x++;
}

function sum(a, b) {
  return a + b;
}
```

---

## 조건문

조건문은 주어진 조건식의 평가 결과에 다라 코드 블록(블록문)의 실행을 결정한다.

조건식은 불리언 값으로 평가될 수 있는 표현식이다.

자바스크립트는 if..else 문과 switch 문으로 두 가지 조건문을 제공

### if…else 문

is…else 문은 주어진 조건식(불러언 값으로 평가될 수 있는 평가식)의 평가 결과, 즉 논리적 참 또는 거짓에 따라 실행할 코드 블록을 결정. 조건식의 평가 결과가 true일 경우 if 문의 코드 블록이 실행되고 false일 경우 else 문의 코드 블록이 실행

```jsx
if (조건식) {
  // 조건식이 참이면 이 코드 블록이 실행
} else {
  // 조건식이 거짓이면 이 코드 블록이 실행
}
```

조건식을 추가하여 조건에 따라 실행될 코드 블록을 늘리고 싶으면 else if 문을 사용

```jsx
if (조건식1) {
} else if (조건식2) {
} else {
}
```

else if 문과 else문은 옵션 즉, 사용할 수도 있고 사용하지 않을 수도 있다.

if 문과 else 문은 2번 이상 사용할 수 없지만 else if 문은 여러 번 사용할 수 있다.

만약 코드 블록 내의 문이 하나뿐이라면 중괄호를 생략할 수 있다.

```jsx
var num = 2;
var kind;

if (num > 0) kind = "양수";
else if (num < 0) kind = "음수";
else kind = "영";
console.log(kind); //양수
```

대부분의 if…else 문은 삼항 조건 연산자로 바꿔 쓸 수 있다.

```jsx
var x = 2;
var result;

if (x % 2) {
  result = "홀수";
} else {
  result = "짝수";
}

console.log(result); //양수
```

다음과 같이 삼항 조건 연산자로 바꿔 쓸 수 있다.

```jsx
var x = 2;
var result = x % 2 ? "홀수" : "짝수";
console.log(result); //짝수
```

---

### switch 문

swich 문은 주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 case 문으로 실행 흐름을 옮긴다. case 문은 상황을 의미하는 표현식을 지정하고 클록으로 마친다. 그리고 그 뒤에 실행할 문들을 위치시킨다.

switch 문의 표현식과 일치하는 case 문이 없다면 실행 순서는 default 문으로 이동.default 문은 선택사항으로, 사용할 수도 있고 사용하지 않을 수 도 있다.

```jsx
switch(표현식){
	case 표현식1:
		switch 문의 표현식과 표현식1이 일치하면 실행될 문;
		break;
	case 표현식2:
		switch 문의 표현식과 표현식2이 일치하면 실행될 문;
		break;
	default:
		switch 문의 표현식과 일치하는 case 문이 없을 때 실행될 문;
}
```

if … else 문의 조건식은 불리언 값으로 평가되어야 하지만 switch 문의 표현식은 불리언 값보다는 문자열이나 숫자 값인 경우가 많다. 다시 말해, if … else 문은 논리적 참, 거짓으로 실행할 코드 블록을 결정

switch 문의 표현식, 즉 month 변수의 평가 결과인 숫자 값 11과 일치하는 case 문으로 실행 흐름이 이동

```jsx
var month = 11;
var monthName;

switch(month){
	case 1: monthName = 'January';
	case 1: monthName = 'February';
	case 1: monthName = 'March';
	case 1: monthName = 'april';
	case 1: monthName = 'May';
	case 1: monthName = 'June';
	case 1: monthName = 'July';
	case 1: monthName = 'August';
	case 1: monthName = 'September';
	case 1: monthName = 'October';
	case 1: monthName = 'November';
	case 1: monthName = 'December';
	default: monthName = "Invalid month';
}
console.log(monthName); //Invalid month
```

그런데 위 예제를 실행해 보면 ‘November’가 출력되지 않고 ‘Invalid month’가 출력된다. 이는 switch 문의 표현식의 평가 결과와 일치하는 case 문을 실행 흐름이 이동하여 문을 실행하는 것은 맞지만 문을 실행한 후 switch 문을 탈출하지 않고 switch 문이 끝날 때까지 이후의 모든 case 문과 default 문을 실행했기 때문. 이를 폴스루라 한다. monthName 변수에 ‘November’가 할당된 후 마지막 default 까지 재할된 상태

이러한 결과가 나온 이유는 case 문에 해당하는 문의 마지막에 break 문을 사용하지 않았기 때문

---

## 반복문

반복문은 조건식의 평가 결과가 참인 경우 코드 블록을 실행 그 후 조건식을 다시 평가하여 여전히 참인 경우 코드 블록을 다시 실행한다 . 이는 조건식이 거짓일 때까지 반복

자바스크립트는 세 가지 반복문인 for 문, whiel 문, do …while 문을 제공

### for 문

for 문은 조건식이 거짓으로 평가될 때까지 코드 블록을 반복 실행. 가장 일반적으로 사용되는 for 문의 형태는 다음과 같다.

```jsx
for(변수 선언문 또는 할당; 조건식; 증감식){
	조건식이 참인 경우 반복 실행될 문;
}
```

for 문은 매우 중요하다. 아직 for 문에 익숙하지 않다면 많은 연습을 통해 확실히 이해하기를 권장

```jsx
for (var i = 0; i < 2; i++) {
  console.log(i);
}
```

```jsx
0;
1;
```

1. for 문을 실행하면 맨 먼저 변수 선언문 var i = 0이 실행 변수 선언문은 단 한번만 실행
2. 변수 선언문의 실행이 종료되면 조건식이 실행 현재 i 변수의 값은 0이므로 조건식의 평가 결과는 true
3. 조건식의 평가 결과가 true 이므로 코드 블록이 실행 증감문으로 실행 흐름이 이동하는 것이 아니라 코드 블록으로 실행 흐름이 이동하는 것에 주의
4. 코드 블록의 실행이 종료 되면 증감식 i++가 실행되어 i 변수의 값은 1이 됨.
5. 증감식 실행이 종료되면 다시 조건식이 실행. 변수 선언문이 실행되는 것이 아니라 조건식이 실행된다는 점에 주의하자 (앞에서 설명했지만 변수 선언문 단 한번만 실행) 현재 i 변수의 값은 1이므로 조건식의 평가 결과는 true이다.
6. 조건식의 평가 결과가 true이므로 코드 블록이 다시 실행
7. 코드 블록의 실행이 종료되면 증감식 i++가 실행되어 i 변수의 값은 2가 된다.
8. 증감식 실행이 종료되면 다시 조건식이 실행. 현재 i 의 변수값은 2이므로 조건식의 평가 결과는 false

for문의 변수 선언문, 조건, 증감식은 모두 옵션이므로 반드시 사용할 필요없는 없다. 단, 어떤 식도 선언하지 않으면 무한 루프가 된다. 무한루프란 코드 블록을 무한히 반복 실행하는 문

```jsx
for(;;){...}
```

for 문 내에 for 문을 중첩해 사용할 수 있다. 이를 중첩 for문이라 한다. 다음은 두개의 주사윌르 던졌을 때 두 눈의 합이 6이 되는 모든 경우의 수를 출력하기 위해 이중 중첩 for 문을 사용한 예

```jsx
for (var i = 1; i <= 6; i++) {
  for (var j = 1; j <= 6; j++) {
    if (i + j === 6) console.log(`[${i},${j}]`);
  }
}
```

```jsx
[1, 5][(2, 4)][(3, 3)][(4, 2)][(5, 1)];
```

---

### while 문

while 문은 주어진 조건식의 평가 결과가 참이면 코드 블록을 계속해서 반복 실행 for 문은 반복 횟수가 명확할 때 주로 사용하고 while 문은 반복 횟수가 불명확할 때 주로 사용

while 문은 조건문의 평가 결과가 거짓이 되면 코드 블록을 실행하지 않고 종료 만약 조건식의 평가 결과가 불리언 값이 아니면 불리언 값으로 강제 변환하여 논리적 참, 거짓을 구별

```jsx
var count = 0;

while (count < 3) {
  console.log(count); //0 1 2
  count++;
}
```

조건식의 평가 결과가 언제나 참이면 무한루프가된다.

```jsx
while(true) {...}
```

무한루프에서 탈출하기 위해서는 코드 블록 내에 if문으로 탈출 조건을 만들고 break 문으로 코드 블록을 탈출

```jsx
var count = 0;

while (true) {
  console.log(count);
  count++;

  if (count === 3) break;
} // 0 1 2
```

---

### do … while 문

do …while 문은 코드 블록을먼저 실행하고 조건식을 평가. 따라서 코드 블록은 무조건 한 번 이상 실행

```jsx
var count = 0;
do {
  console.log(count); // 0 1 2
  count++;
} while (count < 3);
```

---

## break문

switch 문과 while 문에서 살펴보았듯이 break 문은 코드 블록을 탈출한다. 좀 더 정확히 표현하자면 코드 블록을 탈출하는 것이 아니라 레이블 문, 반복문(for, for…in, for…of, while, do…while) 또는 switch 문의 코드 블록을 탈출 레이블 문, 반복문, swtich 문으 코드 블록 외에 break 문을 사용하면 SyntaxError(문법 에러)가 발생

```jsx
if (true){
	break; // Uncaugth SyntaxError : Illeagl break statement
}
```

참고로 레이블 문이란 식별자가 붙은 문을 말한다.

```jsx
foo: console.log("foo");
```

레이블 문은 프로그램의 실행 순서를 제어하는 데 사용한다. 사실 switch 문의 case 문과 default 문도 레이블 문. 레이블 문을 탈출하려면 break 문에 레이블 식별자를 지정한다.

```jsx
foo: {
  console.log(1);
  break foo; // foo 레이블 블록문을 탈출한다.
  console.log(2);
}

console.log("Done!");
```

중첩된 for 문의 내부 for 문에서 break 문을 실행하면 내부 for 문을 탈출하여 외부 for 문으로 진입

이때 내부 for 문이 아닌 외부 for 문을 탈출하려면 레이블 문을 사용

```jsx
outer: for (var i = 0; i < 3; i++) {
  for (var j = 0; j < 3; j++) {
    if (i + j === 3) break outer;
    console.log(`inner [${i}, ${j}]`);
  }
}
console.log("Done!");
```

---

## continue 문

continue 문은 반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다. break 문처럼 반복문을 탈출하지는 않는다.

다음은 문자열에서 특정 문자의 개수를 세는 예

```jsx
var string = 'Hello world';
var search = 'l';
var count = 0;

for( var i =0; i< string.length; i++){
	if(string[i] !== search) continue;
	count++;
}

console.log(count); // 3
const regexp = new RegExp(search, 'g);
console.log(string.match(regexp).length); //3
```

```jsx
for (var i = 0; i < string.length; i++) {
  if (string[i] === search) count++;
}
```
