## 함수 선언식(Function Declarations)이란?
일반적인 프로그래밍 언어에서의 함수 선언과 비슷한 형식이다.

변수 선언이 let이나 const로 시작해야하는 것처럼 함수 선언을 function으로 시작한다.

선언된 함수는 나중 사용을 위해 저장되며, 함수를 실행하려면 함수 이름을 호출(call)하면 된다.

```javascript
function 함수명() {
  구현 로직
}
// 함수 선언
function sayHi() {  // 함수명 sayHi가 곧 변수명이다.
  alert("Hello");
}

// 함수 실행
sayHi();
```

## 함수 표현식(Function Expressions)이란?
함수 표현식은 정의한 function을 별도의 변수에 할당하는 것이다.

함수 선언문의 경우 반드시 함수명이 정의돼 있어야 하는 반면, 함수 표현식은 없어도 되기에 일반적으로 함수 표현식은 함수명을 정의하지 않는다.

함수 표현식은 유연한 자바스크립트 언어의 특징을 활용한 선언 방식으로 다른 언어에서는 함수를 '특별한 동작을 하는 구조'로 취급하지만, 자바스크립트에서는 함수를 특별한 종류의 값(value)으로 취급한다. 즉, 함수를 다른 변수에 값으로써 '할당'한 것이 곧 함수 표현식이다.

```javascript
let 함수명 = function() {
  구현 로직
};
// 함수 표현식을 사용한 변수 할당
let sayHi = function() {  // 변수명 sayHi가 곧 함수명이다.
  alert("Hello");
};

// 함수 실행
sayHi();
```

## 함수 선언식과 표현식의 차이점
함수 선언식은 호이스팅에 영향을 받지만, 함수 표현식은 호이스팅에 영향을 받지 않는다.

함수 선언식은 코드를 구현한 위치와 관계없이 호이스팅되어 브라우저가 자바스크립트를 해석할 때 맨 위로 끌어 올려진다.

이러한 이유로 함수 선언식은 코드가 실행되기 전에 로드되지만, 함수 표현식은 인터프리터가 해당 코드 줄에 도달할 때만 로드된다.


아래 예시는 코드 실행 전의 상태
```javascript
console.log(sum(1, 2));
console.log(minus(5, 2));

function sum(a, b) {          // 함수 선언문
  return a + b;
}

var minus = function(a, b) {  // 함수 표현식
  reutrn a - b;
};
```
아래는 호이스팅에 의해 실제 자바스크립트 엔진이 동작하는 과정이다.

```javascript
var sum = function sum(a, b) {  // 함수 선언문은 전체를 호이스팅한다.
  return a + b;
};

var minus;                      // 변수는 선언부만 호이스팅한다.

console.log(sum(1, 2));
console.log(minus(5, 2));       // 'minus is not a function' 에러 메시지

minus = function(a, b) {        // 변수의 할당부는 원래 자리에 남겨둔다.
  reutrn a - b;
};
```