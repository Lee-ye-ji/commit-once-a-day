# 인터페이스
인터페이스는 상호간의 정의한 약속 혹은 규칙을 의미한다. 
타입스크립트에서의 인터페이스는 보통 다음과 같은 범주에 대해 약속을 정의할 수 있다.
* 객체의 스펙(속성과 속성의 타입)
* 함수의 파라미터
* 함수의 스펙(파라미터, 반환타입 등)
* 배열과 객체를 접근하는 방식
* 클래스
타입스크립트는 객체의 타입을 정의할 수 있게 하는 interface 제공

## 인터페이스 선언문
```ts
interface 인터페이스 이름{
  속성이름[?]: 속성 타입[,...]
}
```

## 선택 속성(옵션 속성)
인터페이스를 설계할 때 어떤 속성은 반드시 있어야 하지만, 어떤 속성은 있어도 되고 없어도 되는 형태로 만들고 싶을 때 사용되어진다.
```ts
interface 인터페이스_이름{
  속성?: 타입;
}
```
속성의 끝에 `?`를 붙인다.
```ts
interface Iperson{
  name: string; // 필수 속성
  age: number; // 필수 속성
  etc?: boolean; // 선택 속성
}
let good1: Iperson2 = { name: 'Jack', age: 32 }
let good2: Iperson2 = { name: 'Jack', age: 32, etc: true }
```

## 익명 인터페이스
타입스크립트는 interface 키워드도 사용하지 않고 인터페이스의 이름도 없는 인터페이스를 만들 수 있다.
```ts
let ai: {
  name: string
  age: number
  etc?: boolean
} = { name: 'Jack', age: 32 }
```
이러한 익명 인터페이스는 주로 다음처럼 함수를 구현할 때 사용된다.
```ts
function printMe(me: {name: string, age: number, etc?: boolean }){
  console.log(
    me.etc ? 
    `${me.name} ${me.age} ${me.etc}` :
    `${me.name} ${me.age}`
  )
}
printMe(ai) // Jack 32
```

## 읽기 전용 속성
읽기 전용 속성은 인터페이스로 객체를 처음 생성할 때만 값을 할당하고 
그 이후에는 변경할 수 없는 속성을 의미한다.
```ts
interface CraftBeer{
  readonly brand: string;
}
```
인터페이스로 객체를 선언하고 나서 수정하려고 하면 아래와 같이 오류가 난다.
```ts
let myBeer: CraftBeer = {
  brand: 'Belgian Monk'
};
myBeer.brand = 'Korean Person'; // error!
```

## 읽기 전용 배열
배열을 선언할 때 `ReadonlyArray<T>`타입을 사용하면 읽기 전용 배열을 생성할 수 있다.
```ts
let arr: ReadonlyArray<number> = [1,2,3];
arr.splice(0,1); // error;
arr.push(4); // error;
arr[0] = 100; // error;
```
위처럼 배열을 `ReadonlyArray`로 선언하면 배열의 내용을 변경할 수 없다. 
선언하는 시점에만 값을 정의할 수 있으니 주의해서 사용해야한다!

## 객체 선언과 관련된 타입 체킹
타입 스크립트는 인터페이스를 이용하여 객체를 선언할 때 좀 더 엄밀한 속성 검사를 진행한다.
```ts
interface CraftBeer {
  brand?: string;
}

function brewBeer(beer: CraftBeer){
  // ...
}

brewBeer({ brandon: 'what' }); // error: Object literal may only specify known properties, but 'brandon' does not exist in type 'CraftBeer'. Did you mean to write 'brand'?
```
위 코드를 보면 `CraftBeer`인터페이스에는 `brand`라고 선언되어 있지만 
`brewBeer()`함수에 인자로 넘기는 `myBeer`객체에는 `brandon`이 선언되어 있어 오탈자 점검을 요하는 오류가 난다.
만약 이런 타입 추론을 무시하고 싶다면 다음과 같이 선언하면 된다.
```ts
let myBeer = { brandon: 'what' }';
brewBeer(myBeer as CraftBeer);
```
인터페이스 정의하지 않은 속성을 추가로 사용하고 싶을 때 아래와 같은 방법을 사용하면 되지만,
any타입을 쓰는 것은 좋지 못한다고 한다...
```ts
interface CraftBeer {
  brand?: string;
  [propName: string]: any;
}
```

### Java에서 interface란?
> 자바에서 인터페이스는 객체를 의미하고, 자바는 기존의 다중 상속이 불가능하다. 
그 이유는 C언어에서 다중상속을 했을 경우 설계(?) 자체에서 불안정했기에 자바 자체에서 다중상속이 불가능하도록 구현했다고 한다.
하지만 강아지라는 객체가 동물이기도 하고 포유류이기도 할 경우 다중상속을 해야하기에 이럴 때에는 
interface를 이용하여 다중 상속해야한다. 
`ex) public class 강아지 extends 동물 implements 포유류{...}`

### 그러면 TS에서도 다중 상속이 불가능한가?
interface를 상속하는 것은 가능하지만 class를 다중 상속하는 것은 불가능하다. 
 `이는 자바도 같다.`
즉, 아래와 같이 `dog`의 인터페이스는 포유류와 동물의 속성을 받을 수 있다.
```ts
interface 동물{
  leg: number;
  eye: number;
  army: number;
}

interface 포유류{
  baby: string[]
}

interface dog extends 동물, 포유류 {
  name: string
}
```
하지만 한 클래스에서 두 개 이상의 상위 클래스로 부터 상속은 불가능하다.
```ts
class A{
  show(){}
}

class B{
  eat(){}
}

class AB extends A, B {}
// error TS1174: Classes can only extend a single class.
```
즉, 타입스크립트에서 클래스와 추상클래스는 extends라는 명령어를 통해서 단 한번만 상속이 가능하다.


--- 
출처) 
https://lakelouise.tistory.com/187
https://joshua1988.github.io/ts/guide/interfaces.html#%EC%9D%BD%EA%B8%B0-%EC%A0%84%EC%9A%A9-%EB%B0%B0%EC%97%B4
https://www.typescriptlang.org/docs/handbook/interfaces.html <br/>
타입스크립트 프로그래밍 책
