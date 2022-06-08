# React의 개념과 장점, 그리고 컴포넌트란 무엇인가?
개념: UI를 구축하기 위한 자바스크립트 프론트엔드 라이브러리 <br/>
장점:
  * virtual DOM을 사용해서 어플리케이션의 성능을 향상시킴
  * 서버, 클라이언트 사이드 렌더링 지원이 가능함
  * 컴포넌트의 가독성이 높고 간단하여 유지보수가 쉬움
  * 다른 프레임워크와도 혼용이 가능  <br/>
컴포넌트란?  <br/>
레고 블록과 같이 작은 단위로 만들어져서 그것을 조립하듯이 개발하는 방법
캡슐화, 확장성, 결합성, 재사용성과 같은 이점이 있음

# props Drilling 이란?
리액트 컴포넌트 트리에서 데이터를 전달하기 위해 필요한 과정

# React Hooks의 장점
* 로직의 재사용이 가능
* 관리가 쉬움
* 함수 안의 다른 함수를 호출하는 것으로 새로운 Hooks를 만들어 볼 수 있음

# virtual DOM을 갱신하는 방법
* setState() 메소드를 호출하는 방법
* Redux store가 변하면 다시 최상위 컴포넌트의 render() 함수를 호출해서 갱신

# 리액트 lifeCycle
* 1) componentDidMount()
-> 최초로 컴포넌트 객체가 생성되어질 때 한 번 수행
* 2) render()
-> 초기에 화면을 그려줄 때와 업데이트가 될 때 호출되어짐
* 3) componentDidUpdate()
-> 컴포넌트의 속성 값 또는 상태 값이 변경되어지면 호출되어짐
* 4) componentWillunmount()
-> 컴포넌트가 소멸될 때 호출되어짐

# state를 직접 변경하지 않고 setState를 사용하는 이유?
* state는 불변성을 유지 해야하기 때문
* 컴포넌트는 setState를 비교해서 업데이트가 필요한 경우에만 render함수를 호출하는데 state를 직접 수정하게 되면 
* react가 render함수를 호출하지 않아 상태 변경이 일어나도 렌더링이 일어나지 않을 수 있음

# class component와 functional component의 차이점
* class component는 여러 단계 상속으로 인해 복잡성과 오류 가능성을 증가 시킴
* 이로 인해 functional component가 탄생하게 됨
* functional component는 hooks를 이용하여 생명주기에 원하는 동작을 할 수 있으며,
* class component는 life cycle을 가져 생명주기 메소드를 알고 있어야 함

#  virtual DOM이 무엇인가요? virtual DOM이 좋은 이유는?
* virtual DOM은 실제 DOM 변화를 최소화 시켜주는 역할을 함
* virtual DOM을 사용하면 효율성을 높일 수 있고, 시간 복잡도를 낮출 수 있음
* ex) 만약 HTML 파일에 20개의 변화가 생기면 과정 역시 20회가 이루어짐
* 하지만 virtual DOM은 변화된 부분만 가려내어 실제 DOM에 전달하기 때문에 실제 DOM은 1회로 인식함

# JSX란 무엇인가?
* JSX는 자바스크립트 코드를 HTML처럼 표현할 수 있는 React 엘리먼트를 생성하는 언어이다.

# 웹 성능 향상을 위해 최적화를 해 본 경험이 있나요? 혹은 useMemo와 useCallback 메소드를 활용해 최적화하는 원리에 대해서 설명하세요.
* 웹 성능 향상을 위해 useMemo와 useCallback 메소드를 이용
* useMemo는 특정 결과 값을 재사용하고 싶을 때 사용
* useCallback은 특정 함수를 재사용하고 싶을 때 사용
* 이 둘은 dependency 리스트를 이용하여 값이 변경되었을 경우 결과에 대해 반영함

# useCallback의 동작원리
* useCallback은 함수를 재사용하고 싶을 때 사용되는 hook으로 이 메소드를 사용한다면 성능최적화에 이점이 있음
* deps의 변경을 통해 값이 변경되면 새로운 함수를 return하고.
* 값이 변경되지 않으면 기존 함수를 return

# React 에서 상태 변화가 생겼을 때, 변화를 어떻게 알아채는지에 대해서 설명하세요.
* react에서 상태는 불변성을 띄고 있음
* 그렇기 때문에 상태의 주소값이 변경이 되면 변화가 되었다는 것을 알 수 있음
