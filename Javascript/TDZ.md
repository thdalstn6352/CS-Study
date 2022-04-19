# Temporal Dead Zone(TDZ)
## TDZ: 스코프의 시작 지점부터 초기화 시작 지점까지의 구간
![tdz](https://user-images.githubusercontent.com/12326139/163824806-875c9fa7-3936-411d-af30-32b226fb72ba.png)
>TDZ 시맨틱은 선언 전에 변수에 접근하는 것을 금지한다. TDZ는 에러를 발생한다: 변수 선언 전에 어떤 것도 사용하지 않는다.

var와 let/const선언에 대한 범위의 차이 중 하나는 let/const가 TDZ에 의해 제약을 받는다는 것이다.
즉, 변수가 초기화되기 전에 액세스하려고 하면, var처럼 undefined를 반환하지 않고, ReferenceError가 발생한다. 이는 코드를 예측가능하고 잠재적 버그를 쉽게 찾아낼 수 있도록 한다.


▣ 변수 생성 단계
TDZ 를 이해하기 위해서는 Javascript 의 변수 생성 단계를 먼저 알아야 합니다.


1. 선언 단계 (Declaration phase)
변수를 실행 컨텍스트의 변수 객체에 등록하는 단계

2. 초기화 단계 (Initialization phase)
실행 컨텍스트에 등록한 변수를 위한 메모리를 만드는 단계, 메모리가 만들어지면 처음에는 undefined 가 할당

3. 할당 단계 (Assignment phase)
사용자가 undefined 로 할당된 변수에 다른 값을 할당하는 단계

* var 는 선언과 초기화 단계가 동시에 이루어집니다.
* let, const 는 선언, 초기화, 할당 단계가 각각 따로 이루어집니다.
* function (함수 선언문) 은 선언, 초기화, 할당 단계가 동시에 이루어집니다.


그렇기 때문에 선언과 초기화 단계가 따로 이루어 지는 let, const 같은 경우는 TDZ에 영향을 받는다.

참고: https://dmitripavlutin.com/javascript-variables-and-temporal-dead-zone/
https://noogoonaa.tistory.com/78