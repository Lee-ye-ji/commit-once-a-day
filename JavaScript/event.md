# 이벤트 버블링(Event Bubbling), 이벤트 캡처링(Event Capturing)에 대해서 설명하세요.
* 이벤트 버블링
-> 특정 화면 요소에서 이벤트가 발생했을 때 더 상위 요소들로 전달되어 가는 특성을 의미함
* 이벤트 캡처링
-> 이벤트 버블링과 반대로 상위 요소에서 하위 요소로 탐색하여 이벤트를 전파하는 방식

# 이벤트 버블링을 막을 수 있는 방법은?
이벤트 버블링을 막기 위해서는 이벤트 객체인 메소드인 `event.stopPropagation()`을 사용하면 된다.

# event delegation에 대해서 설명
* 이벤트 위임은 상위노드에서 하위노드의 이벤트를 제어하고 싶을 때 쓰는 방식
* 동적인 요소들에 대한 처리가 수월함
* 이벤트 핸들러를 더 적게 등록해주기 때문에 메모리도 절약할 수 있음
* to do list에서 오늘의 할일을 추가하고, 그 추가된 항목의 일을 완료했다면
* 완료했다는 의미로 밑줄을 그어야 한다.
* 이 때 이벤트 위임을 활용하여 li 태그의 추가된 리스트를 통제할 수 있는 ul 태그에 이벤트 리스너를 연결
* 그 후 하위에서 발생하는 이벤트를 감지 시켜주도록 사용할 수 있음
