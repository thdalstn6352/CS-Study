# 🎈 자바스크립트의 특징
### 웹 페이지에 생동감을 붙어넣기 위해 만들어진 프로그래밍 언어 
### HTML, CSS와 함께 웹을 구성하는 요소 중 하나로 웹 브라우저에서 동작하는 유일한 프로그래밍 언어

## 특징
1. 자바스크립트는 개발자가 별도의 컴파일 작업을 수행하지 않는 동적이며, 타입을 명시할 필요가 없는 인터프리터 언어
2. 대부분의 모던 자바스크립트 엔진(크롬의 V8, 파이어폭스의 SpiderMoney, 사파리의 JavaScriptCore, 마이크로소프트 엣지의 Chakra 등)은 인터프리터와 컴파일러의 장점을 결합해 비교적 처리 속도가 느린 인터프리터의 단점을 해결.
3. 인터프리터는 소스코드를 즉시 실행하고 컴파일러는 빠르게 동작하는 머신 코드를 생성하고 최적화한다. 이를 통해 컴파일 단계에서 추가적인 시간이 필요함에도 더욱 빠르게 코드를 실행할 수 있다.
4. 싱글 쓰레드 기반 언어

## 컴파일러 언어와 인터프리터 언어

|컴파일러 언어|인터프리터 언어|
|------|---|
|코드가 실행되기 전 단계인 컴파일 타임에 소스코드 전체를 한번에 머신 코드로 변환한 후 실행|코드가 실행되는 단계인 런타임에 문 단위로 한 줄씩 중간코드(interdediate code)인 바이트코드로 변환한 후 실행|
|실행 파일을 생성한다.|실행 파일을 생성하지 않는다.|
|컴파일 단계와 실행 단계가 분리되어 있다. 그리고 명시적인 컴파일 단계를 거치고, 명시적으로 실행 파일을 실행한다.|인터프리트 단계와 실행 단계가 분리되어 있지 않다.|
|인터프리터는 한 줄씩 바이트코드로 변환하고 즉시 실행한다.||
|실행에 앞서 컴파일은 단 한번 수행된다.|코드가 실행될 때마다 인터프리트 과정이 반복 수행된다.|
|컴파일과 실행 단계가 분리되어 있으므로 코드 실행 속도가 빠르다.|인터프리트 단계와 실행 단계가 분리되어 있지 않고 반복 수행되므로 코드 실행 속도가 비교적 느리다.|


하지만 대부분의 모던 브라우저에서 사용되는 인터프리터는 전통적인 컴파일러 언어처럼 명시적인 컴파일 단계를 거치지는 않지만 복잡한 과정을 거치며 일부 소스코드 컴파일하고 실행한다.

이를 통해 인터프리터 언어의 장점인 동적 기능 지원을 살리면서 실행 속도가 느리다는 단점을 극복한다. 따라서 현재는 컴파일러와 인터프리터의 기술적 구분이 점파 모호해져 가는 추세다. 하지만 자바스크립트는 런타임 컴파일되며 실행 파일이 생성되지 않고 인터프리터의 도움 없이 실행할 수 없기 때문에 컴파일러 언어라고 할 수 없다.

자바스크립트는 명령형, 함수형, 프로토타입 기반 객체지향 프로그래밍을 지원하는 멀티 패러다임 프로그래밍 언어다.

비록 다른 객체지향 언어와의 차이점에 대한 논쟁이 있긴 하지만 자바스크립트는 강력한 객체지향 프로그래밍 능력을 지니고 있다. 간혹 클래스(ES6에서 도입됨), 상속, 정보 은닉을 위한 키워드가 없어서 객체지향 언어가 아니라고 오해하는 경우고 있지만 자바스크립트는 클래스 기반 객체지향 언어보다 더 효율적이면서 강력한 **프로토타입 기반의 객체지향 언어**다.



## 자바스크립트의 표준화
### 크로스 브라우징 이슈
= 브라우저에 따라 웹페이지가 정상적으로 동작하지 않는 문제

### 크로스 브라우징 이슈의 배경
1. 마이크로 소프트사가 자바스크립트의 파생인 "JScript"를 자사 익스플로러 브라우저의 탑재
2. 시장성을 높이기 위해 익스플로러에서만 동작하는 기능을 추가
3. 이로 인해 브라우저에 따라 웹페이지가 정상적으로 동작하지 않는 크로스 브라우징 이슈 발생
### 표준화 시작
1. 1996년 11월, 넷스케이프 케뮤니케이션즈가 비영리 표준화 기구인 ECMA 인터내셔널에 자바스크립트의 표준화 요청
2. 1997년 7월, ECAM-262라불리는 표준화된 자바스크립트(ECMAScript 1) 사양이 완성
3. 2015년에 공개된 ECMAScript 6(ECMAScript 2015, ES6)는 let/const 키워드, 화살표 함수, 클래스, 모듈 등과 같이 범용 프로그래밍 언어로서 갖춰야 할 기능들을 대거 도입하는 큰 변화

### ECMAScript 버전별 특징
- ES1(1997) 	초판
- ES2(1998)	ISO/IEC 16262 국제 표준과 동일한 규격을 적용
- ES3(1999)	정규 표현식, try ... catch
- ES5(2009)	HTML5 함께 출현한 표준안.
JSON, strict mode, 접근자 프로퍼티, 프로퍼티 어트리뷰트 제어, 향상된 배열 조작 기능(forEach, map, filter, reduce, some, every)
- ES6(ECMAScript 2015)	let/const 클래스, 화살표 함수, 템플릿 리터럴, 디스트럭처링 할당, 스프레드 문법, rest 파라미터, 심벌, 프로미스, Map/Set, 이터러블, for ...of, 제너레이터, Proxy, 모듈 import/export
- ES7(ECMAScript 2016)	지수(**) 연산자, Array.prototype.includes, String.prototype.includes
- ES8(ECMAScript 2017)	async/await, Object 정적 메서드(Object.values, Object.entries, Object.getOwnPropertyDescriptors)
- ES9(ECMAScript 2018)	Object rest/spread 프로퍼티, Promise.prototype.finally, async generator, for wait ... of
- ES10(ECMAScript 2019)	Object.formEntries, Array.prototype.flat, Array.prototype.flatMap, optional catch biding
- ES11(ECMAScript 2020)	String.prototype.matchAll, BigInt, globalThis, Promise.allSettled, null 병합 연산자, 옵셔널 체이닝 연산자, for ... in enumeration order



