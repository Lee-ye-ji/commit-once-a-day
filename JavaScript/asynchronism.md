# callback, Promise, async/await의 차이점
* 이 세개의 함수는 비동기를 위한 함수로 맨 먼저 callback이 만들어지게 됨.
* callback은 함수의 처리 순서를 보장하는 과정에서 중첩해서 사용하게 되고,
* 이를 계속해서 사용하다 보니 콜백 지옥 현상이 발생하게 됨
* 콜백 지옥 현상으로 인해 가독성과 유지보수가 떨어지게 되고, 

* 그 이후로 Promise가 탄생하게 되었음
* Promise는 비동기 연산이 종료된 이후에 에러를 처리할 수 있도록 처리기를 연결하는 역할의 객체임
* 그 Promise 객체로 인해 성공, 실패, 에러처리 로직을 처리하기에 수월해지게 됨

* Async/await는 비동기 코드를 동기식으로 표현하는 더 나은 방법으로, 이 둘은 같이 있어야 제대로 동작이 가능함
* Async함수는 Promise 객체를 통해 비동기적으로 처리된 내용을 동기적인 코드 진행 순서로 보여주는 역할을 함
* await는 Promise 객체를 받아서 처리하고, 만약 비동기함수가 아닌 동기적 함수라면 리턴값을 그대로 받음