# 타입 시스템
* 타입 시스템의 구분
  * 명시적으로 알려주는 타입
  * 자동으로 타입을 추론하는 타입
```ts
let a : number = 1;
// 어노테이션: 타입 명시
```
```js
let a = 1;
// 타입 추론
```
타입스크립트는 충분히 추론을 잘하기 때문에 꼭 필요할 때만 어노테이션을 사용한다!


# 타입스크립트 기본 타입
### boolean
👉 `true 또는 false를 나타내는 자료형`
```ts
let isDone: boolean = false;
// Primitive Type하기 -> boolean 소문자
isDone = true;
console.log(typeof isDone) // boolean
```
---
### Number
👉 `JavaScript와 같이 TypeScript의 모든 숫자는 부동 소수점 값`
```ts
let decimal:number = 6;
// 10진수 사용 가능
let hex:number = 0xf00d;
// 16진수도 사용 가능
let binary:number = 0b1010;
// 2진수도 사용 가능
let octal:number = 0o744;
// 8진수도 사용 가능
let notNumber:number = NaN;
// NaN을 할당해도 전혀 문제 없음!
// NaN은 숫자의 한 형태!!!
let underscoreNum:number = 1_000_000;
// _를 이용해서도 사용가능 
// 1_000_000 = 1,000,000 = 백만
```
---
### String
👉 `텍스트 형식을 참조하기 위해 "String"형식을 사용`
* 자바스크립트와 마찬가지로, 문자열 데이터를 감싸기 위해 `"`큰 따옴표나, `'`작은 따옴표를 사용!
```ts
let myName:string = "Yeji";
myName = "Anna";
```
#### Template String
```ts
let fullName: string = "Yeji";
let age:number = 20;
let sentence:string = `Hello My Name is ${fullName}. 
	I'll be ${age + 1} years old next month`;

console.log(sentence)
// Hello My Name is Yeji. 
// I'll be 21 years old next month
```
---
### Symbol
👉 `Symbol은 고유한 데이터로, 여러개의 Symbol에 동일한 description을 넣어도 각 다른 존재로 인식된다.`
* Symbol을 함수로 사용해서 symbol 타입을 만들어 낼 수 있음
* 📌 주로 접근을 제어하는 데 쓰는 경우가 많음
```ts
const sym = Symbol();

const obj = {
	[name]: "val"
};

console.log(obj[name]) // "val"
// 접근을 막거나, 접근이 필요한 경우에만 사용
```

### Null & Undefined
👉 `값이 없다는 의미!`
#### Null과 Undefined의 차이점은?
📌 **null은 Object자료형을 가지고 있고, undefined는 자료형이 없다!**
```ts
// 이 변수들에 할당할 수 있는 것들은 거의 없다

let u: undefined = undefined;
let n: null = null;
```
---
### Object
👉 `객체: 이름(name)과 값(value)으로 구성된 프로퍼티(property)의 정렬되지 않은 집합`

* `Primitive Type`과 다르게 직접 값을 가지고 있지 않고, 그 값을 가리키는 정보를 가지고 있는 성질을 가지고 있음
```ts
// Created by object literal
const person1 = {name: 'Yeji', age: 20};

// person1 is not "object" type
// 타입스크립트에선 person1은 Object 타입이 아니다.
// person1 is "{name: 'Yeji', age: 20}" type
// person1은 "{name: 'Yeji', age: 20}" 이러한 타입으로 나온다.

// Created by Object.create
// Object: 소문자가 아닌 대문자 오브젝트!
// Object: 전역객체, 내장전역객체 - runtime에 제공되는 미리 준비된 것
// 여기서 Object는 Primitive Type이 아닌 것!
// 그래서 인자로 들어오는 타입은 오브젝트 or null인 합집합으로 이루어져 있음!
const person2 = Object.create({name: 'Yeji', age: 20});
```
--- 
### Array
👉  `같은 타입의 요소들을 모아놓은 자료형`
* 📌 배열 안에 있는 요소, 요소들은 같은 타입이다!
* 원래 자바스크립트에서 array는 객체이다
* 사용방법
    * Array<타입>
    * 타입[]
```ts
let list: number[] = [1, 2, 3]; // 이 방식이 더 많이 사용됨!
let list: Array<number> = [1, 2, 3];
// Array<number>는 js나 ts에서 충돌 날 위험이 있기 때문!

let list: (number | string)[] = [1, 2, 3, "4"];
// union으로 위처럼 가능
// 하지만 ["Mark", 39]의 자료처럼 첫번째는 String, 두번째는 Number의 경우에는
// Array가 아닌 Tuple을 사용!
```
---
### Tuple
👉 `배열과 비슷하지만, 자료형에 대한 순서가 있을 때 사용되는 자료형`

> `["Mark", 39]`의 자료처럼 첫번째는 `String`, 두번째는 `Number`의 경우에는 `Array`가 아닌 `Tuple`을 사용!

```ts
let x: [string, number];

x = ["Yeji", 20]; // 순서와 타입, 길이 모두 일치해야 함

// x = [20, "Yeji"]; // Error - 순서가 다르기 때문에

// x[2]; // Error - 2번째 인덱스에는 아무것(undefined)도 없기 때문에

const person: [string, number] = ["Yeji", 20];

const [] = person; // destructuring (분해할당)
// person에 있는 요소를 가지고 나와서 [] 변수 안에 넣음!
// 순서가 중요함! -> [first, second]
const [first, second] = person;
```
---
### Any
👉 `어떤 것이나 된다는 의미를 가진 타입`
* 정말 어떤 것이든 들어올 수 있는 경우가 있고, 아닌 경우가 있을 수도 있다. 개발자가 타이핑하다가 귀찮아진 경우나 어떤 타입인지 모를 때 무심코 쓰게 된다면, 전체적인 문제가 발생할 수 있다.

**📌 즉, Any는 정확히 알고 써야한다.!**
```ts
function returnAny(message): any {
	console.log(message);
};

const any1 = returnAny('리턴은 아무거나');

any1.toString(); // 타입에러 뜨지 않음 > any이기 때문
```
* any를 최대한 쓰지 않는 게 핵심이다.
* 왜냐하면 컴파일 타입에 타임체크가 정상적으로 이루어지지 않기 때문이다.
* 그래서 컴파일 옵션 중에는 any를 써야하는 데 쓰지 않으면 오류를 뱉도록 하는 옵션이 있음! ➡ `noImpicitAny`
* 편의를 위해서 any를 지정한 순간! 안전성을 잃을 수 있음!ㅜ

**Any의 전파력을 알 수 있는 코드**
```ts
let looselyTyped: any = {};

let d = looselyTyped.a.b.c.d;
// looselyTyped는 any이기에 .a.b.c로 타고 갈 경우에도 any로 지정이 된다.
// 그로 인해 오류가 발생하지 않는다... 

function leakingAny(obj: any) {
	// const a = obj.num; // a의 타입: any
  	const a: number = obj.num; // a의 타입: number
  	const b = a + 1; // b의 타입 : any -> b의 타입 : number
  
  	return b;
}

const c = leakingAny({ num : 0 });
// c.indexOf('0');
```
---
### Unknown
👉 `Any가 가지고 있던 타입에 불안정한 요소를 주는 그러한 부분을 해소시키고자 나온 대체 자료형`
* 응용프로그램을 작성할 때는 모르는 변수의 타입을 묘사해야할 수도 있다.
➡ 모르는 변수를 `any`라고 지정했었던 것이다!
이러한 경우는 api를 얻어서 오는 동적콘텐츠 일 수 있다.
* 컴파일러와 코드를 작성하는 다른 사람에게 이 변수가 무엇이든 될 수 있음을 알려주는 타입을 제공하기 위해 쓰인다.

```ts
declare const maybe: unknown;

// const aNumber: number = maybe; (X)
if(typeof maybe === 'number') { // typeof typeguard
	const aNumber: number = maybe; // (O)
}

if(maybe === true) { // typeguard
	const aBoolean: boolean = maybe; // (O)
  	// const aString: string = maybe; // (X)
}

if(typeof maybe === 'string') { // typeof typeguard
	const aString: string = maybe; // (O)
  	// const aBoolean: boolean = maybe; // (X)
}
```
---
### never
👉 `보통 return에서 사용된다.`
```ts
function error(msg: string): never {
	throw new Error(msg);
  	// throw를 하면 이 밑으로는 내려오지 않게 된다.
}
// never는 아무것도 리턴되지 않는다라는 의미
// return이나 함수의 body부분이 끝나지 않아야 한다.

function fail() {
	return error('failed');
}

function infiniteLoop(): never {
	while(true) {}
  	// while 밑으로 내려오지 않는다.
}
```
---
### Void
👉 `어떤 타입도 가지고 있지 않는 빈 상태를 의미하는 자료형`
* 값은 없고, type만 있어서 void라는 값을 쓸 수는 없음!
* 소문자로 사용
* 일반적으로 어떤 변수 안에다가 void라는 것을 annotation하는 게 아니고, 값을 반환하지 않는 일종의 undefined를 리턴하는 상태일 때 return타입으로 사용된다.
* 함수의 반환타입으로 사용
```ts
function returnVoid(message:string) {
	console.log(message);
  
  	return;
}
const r = returnVoid("리턴이 없다"); // const r: void

function returnVoid(message: string): void {
	console.log(message);
  
  	return undefined;
}
```

---
