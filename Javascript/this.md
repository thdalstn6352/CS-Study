# ⚡️ this의 정의
## ❗️this는?
### this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수(self-reference variable)이다.

this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다.
this는 자바스크립트 엔진에 의해 암묵적으로 생성된다.
this는 코드 어디서든 참조할 수 있다.

하지만 this는 객체의 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수이므로
일반적으로 객체의 메서드 내부 또는 생성자 함수 내부에서만 의미가 있다.
함수를 호출하면 인자와 this가 암묵적으로 함수 내부에 전달된다.
함수 내부에서 인자를 지역 변수처럼 사용할 수 있는 것처럼, this도 지역 변수처럼 사용할 수 있다.
단, this가 가리키는 값, 즉 this 바인딩은 함수 호출 방식에 의해 동적으로 결정된다.
크게 전역에서 사용할 때와 함수안에서 사용할 때로 나눌 수 있다.
👉 바인딩이란?
식별자와 값을 연결하는 과정을 말한다.
변수선언은 변수 이름과 확보된 메모리 공간의 주소를 바인딩하는 것이다.
this 바인딩은 this(키워드로 분류되지만 식별자의 역할을 한다.)와 this가 가리킬 객체를 바인딩하는 것이다.
❗️this를 전역에서 사용한 경우
브라우저라는 자바스크립트 런타임의 경우에 this는 항상 window라는 전역 객체를 참조한다.
전역 객체란 전역 범위에 항상 존재하는 객체를 의미한다. (Node.js에서 전역 객체는 global 이다.)
브라우저라는 자바스크립트 런타임에서 모든 변수, 함수는 window라는 객체의 프로퍼티와 메소드이다.
전역변수의 프로퍼티

브라우저의 전역 객체 window
node.js-전역객체-global

Node.js 의 전역 객체 global
Node.js의 REPL에 this 와 global 키워드를 각각 입력한 결과가 동일한 것을 확인 할 수 있다.
❗️this를 함수 내부에서 사용한 경우
함수는 전역에 선언된 일반 함수와 객체 안에 메소드로 크게 구분할 수 있다.
객체안에 선언된 함수를 전역에 선언된 함수와 구분하기 위해 메소드라고 한다.
그런데 전역에 선언된 일반 함수도 결국 window 전역 객체의 메소드다.
즉, 모든 함수는 객체 내부에 있다.
이때 this는 현재 함수를 실행하고 있는 그 객체를 참조한다.
정리하면 함수 내부에서 this의 값은 함수를 호출하는 방법에 의해 바뀐다.
그리고 또한 엄격모드 여부에 따라 참조 값이 달라진다.
엄격 모드에서 일반 함수 내부의 this는 undefinded 가 바인딩 된다.
 

 

⚡️ this의 사용
❗️전역에 선언된 함수에서 this
👉 Case 1.
function → global (window, global) 인 경우이다.
function myFn () {
  return this;
}
myFn(); // window 객체 출력
👉 Case 2.
new 연산자를 사용해서 생성자 함수방식으로 인스턴스를 생성한 경우이다.
생성자 함수 MyFn가 빈 객체를 만들고 이 생성자 함수에서 this가 이 빈 객체를 가리키도록 설정하였다.
function MyFn() {
  this.title = 'Hello World!';
  return this;
}
// new 연산자를 이용해서 새로운 객체를 얻는다.
const myfn = new MyFn();
myfn // MyFn {title: 'Hello World!'}
 

❗️객체의 메소드 함수에서 this
👉 Case 1.
method → obj 인 경우이다.
showTitle() 메소드는 fn 객체의 메소드이기 때문에 this는 fn 객체를 참조한다.
const fn = {
  title: 'Hello World!',
  showTitle() {
    console.log(this.title);
  }
};
fn.showTitle(); // 'Hello World!'
👉 Case 2.
고차 함수의 콜백함수 안에서 this는 콜백함수가 일반 함수이기 때문에 전역 객체를 참조한다.
const fn = {
  title: 'Hello World!',
  tags: [1, 2, 3, 4],
  showTags() {
    this.tags.forEach(function(tag) {
      console.log(tag);
      console.log(this); // window
    });
  }
}
fn.showTags();
// 1
// window 객체 출력
// 2
// window 객체 출력
// 3
// window 객체 출력
// 4
// window 객체 출력
👉 Case 3.
Case 2. 해결 방법으로 콜백함수 다음 인자로 참조할 객체를 전달해준다.
const fn = {
  title: 'Hello World!',
  tags: [1, 2, 3, 4],
  showTags() {
    this.tags.forEach(function(tag) {
      console.log(tag);
      console.log(this); // fn
    }, this); // 여기는 일반 함수 바깥, fn 객체를 참조할 수 있다.
  }
}
fn.showTags();
// 1
// fn 객체 출력
// 2
// fn 객체 출력
// 3
// fn 객체 출력
// 4
// fn 객체 출력
👉 Case 4.
function 키워드로 생성한 일반함수와 화살표 함수의 가장 큰 차이점이 바로 this이다.
이를 Lexical this (렉시컬 this)라고 한다.
화살표 함수 안에서 this는 언제나 상위 스코프의 this를 가리킨다.
일반 함수는 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정되지 않고, 함수를 호출 할 때 함수가 어떻게 호출 되는지에 따라 this에 바인딩할 객체가 동적으로 결정된다.
화살표 함수는 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정된다.
화살표 함수의 this 바인딩 객체 결정 방식은 함수의 상위 스코프를 결정하는 방식인 렉시컬 스코프와 유사하다.
화살표 함수는 call, apply, bind 메소드를 사용하여 this를 변경할 수 없다.
const fn = {
  title: 'Hello World!',
  tags: [1, 2, 3, 4],
  showTags() {
    this.tags.forEach((tag) => {
      console.log(tag);
      console.log(this); // fn
    });
  }
}
fn.showTags();
// 1
// fn 객체 출력
// 2
// fn 객체 출력
// 3
// fn 객체 출력
// 4
// fn 객체 출력
 

 

⚡️ 결론
this는 이처럼 어떤 위치에 있느냐, 어디에서 호출하느냐, 어떤 함수에 있느냐에 따라 참조 값이 달라지는 특성이 있다.
그래서 사용할 때 주의해야한다.
