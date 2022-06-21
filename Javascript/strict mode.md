
# use strict 사용으로 발생하는 제약 조건
 

전역 변수를 허용하지 않으며, 전역 변수 선언시 오류 발생
변수 이름 선언 및 사용시 "var"가 누락되면 오류 발생
값 할당 실패는 오류 발생 (NaN = 1;).
삭제할 수없는 속성을 삭제하려고 하면 (Object.prototype 삭제) 오류 발생
읽기 전용 속성에 쓰기를 하려고 하면 오류 발생
객체 리터럴의 모든 속성 이름은 고유해야한다. (var x = {x1 : "1", x1 : "2"}).
함수의 파라메터는 고유해야 한다. (function calc (x, x) {}와 같이 같은 파라미터 이름 중복 사용 금지)
8 진수 구문과 8진수 이스케이프 표현 금지(var a = 010; 과 같은 8진수 표현 사용 금지)
with 키워드 금지
'eval', 'agruments'는 예약어로 변수명으로 사용불가능 (var eval = 1;)
변수를 생성하는 eval()은 보안상 사용불가능 (eval ("var x = 2");)
변수 이름과 함수 이름 삭제 금지 (var a = 1; delete a;)
arguments.callee 미지원. arguments.callee 속성은 이름이 없는 익명 함수(anonymous function)를 선언해서 사용할 때 실행 중인 함수 안에서 함수 자신을 참조하기 위해 사용. 재귀 호출 방식으로 자신을 호출하는 방식은 잠재적으로 참조 오류를 발생시킬 수 있음


출처: https://haenny.tistory.com/286 [Haenny]