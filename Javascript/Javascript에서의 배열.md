# 배열

자료구조에서 말하는 배열(array)은 동일한 크기의 메모리 공간이 빈틈없이 연속적으로 나열된 자료구조이다. 우리가 통상적으로 알고있는 이 배열을 밀집 배열(dense array)이라고 한다.

일반적인 배열은 각 요소가 동일한 데이터 크기를 가지며, 빈틈없이 연속적으로 이어져 있다.

## Javascript에서의 배열은 배열이 아니다
결론부터 말하자면, Javascript에서의 배열은 배열이 아닌 객체이다. 더 정확하게는 일반적인 배열의 동작을 흉내 낸 특수한 객체이다.

Javascript에서의 배열은 요소를 위한 각각의 메모리 공간은 동일한 크기를 갖지 않아도 되며, 연속적으로 이어져 있지 않을 수도 있다. 이러한 배열을 희소 배열(sparse array)라고 한다.

```javascript
const arr = [1, 2, 3];

console.log(typeof arr); // object
console.log(arr.constructor === Array);  // true
console.log(Object.getPrototypeOf(arr) === Array.prototype);  // true
```


위의 코드의 결과를 보면 알 수 있듯이 Javascript에서의 배열은 객체이다. 그렇다면 일반 객체와는 어떠한 차이가 있을까?

|구분|객체|배열|
|---|---|---|
|구조|Key와 Value|Index와 Element|
|값의 참조|Key값|Index값|
|값의 순서|X|O|
|length 프로퍼티|X|	O|


일반 객체와 배열을 구분하는 가장 명확한 차이는 값의 순서와 length 프로퍼티이다.

```javascript
console.log(Object.getOwnPropertyDescriptors([1, 2, 3]));
/*
{
  '0': { value: 1, writable: true, enumerable: true, configurable: true },
  '1': { value: 2, writable: true, enumerable: true, configurable: true },
  '2': { value: 3, writable: true, enumerable: true, configurable: true },
  length: { value: 3, writable: true, enumerable: false, configurable: false }
}
*/
```
위의 코드의 결과처럼 Javascript에서의 인덱스를 나타내는 문자열을 프로퍼티 key로 가지며, length 프로퍼티를 갖는 특수한 객체로 Javascript에서의 요소는 사실 value 값인 것이다.

자바스크립트에서는 모든 값이 객체의 프로퍼티 값이 될 수 있으므로 어떠한 타입의 값이라도 배열의 요소가 될 수 있다.

## 일반적인 배열과 Javascript에서의 배열의 차이
### 일반적인 배열
- 인덱스로 요소에 빠르게 접근 가능
- 특정 요소를 검색하거나 삽입 또는 삭제의 경우 효율적이지 않음

### 자바스크립트의 배열
- 해시 테이블로 구현된 객체이므로 인덱스로 요소에 접근하는 경우 일반적인 배열보다 성능적으로 느림
- 특정 요소를 검색하거나 삽입 또는 삭제하는 경우에는 일반적인 배열보다 성능적으로 빠름

## length 프로퍼티와 희소배열
length 프로퍼티는 배열의 길이를 나타내는 0 이상의 정수를 값으로 갖는다.

```javascript
const arr = [1, 2, 3];
console.log(arr.length);  // 3

arr.push(4);
console.log(arr.length);  // 4

arr.pop();
console.log(arr.length); // 3
```
length 프로퍼티에 임의의 값을 할당할 수도 있다.

```javascript
const arr = [1, 2, 3, 4, 5];

arr.length = 3;
console.log(arr); // [1, 2, 3]
const arr = [1, 2];

arr.length = 4;

console.log(arr.length); // 4
console.log(arr);  // [ 1, 2, <2 empty items> ]
```
위의 코드에서의 empty items는 실제로 추가가 되지는 않는다.
현재 length 프로퍼티 값보다 큰 숫자를 할당하게 되면 length는 변경되지만 실제 배열에는 아무 변화가 없다.

```javascript
console.log(Object.getOwnPropertyDescriptors(arr));
/*
{
  '0': { value: 1, writable: true, enumerable: true, configurable: true },
  '1': { value: 2, writable: true, enumerable: true, configurable: true },
  length: { value: 4, writable: true, enumerable: false, configurable: false }
}
*/
```
위의 코드의 결과를 보면 값이 없는 요소를 위해 메모리 공간을 확보하지 않은 것을 확인할 수 있다.

이처럼 배열의 요소가 연속적으로 위치하지 않고 일부가 비어 있는 배열을 희소 배열이라고 한다.

## 배열인지 체크
자바스크립트 코드를 작성하다가 해당 변수가 배열인지 아닌지 체크해야할 때가 있다.
위에서 언급을 했지만 자바스크립트에서는 배열은 객체로 만들어져 있기 때문에 보통 사용하는 typeof 로는 배열인지 알 수가 없다.
따라서, 자바스크립트에서는 Array.isArray() 라는 배열인지 체크하는 메서드를 제공한다.

```javascript
const arr = [1, 2, 3];

console.log(typeof arr);  // object
console.log(Array.isArray(arr));  // true
```




references
TCPschool - 배열
MDN - Array
MDN - Array.isArray()
모던자바스크립트 - array

