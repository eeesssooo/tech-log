---
title: 'Core Javascript | 콜백함수'
category: 'Javascript'
date: '2021-10-13 17:00:00 +09:00'
desc: '코어 자바스크립트 책을 보며 공부한 내용입니다.'
thumbnail: './images/markdown-test/thumbnail.jpg'
alt: '코어 자바스크립트를 보며 공부한 내용입니다.'
---

## 1. 콜백함수란?

### 콜백함수

- 다른 코드(함수 or 메서드)의 인자로 넘겨주는 함수
- 제어권도 함께 위임한 함수

## 2. 제어권

**콜백함수의 제어권을 넘겨받은 코드가 갖는 제어권**

- 콜백함수를 호출하는 시점을 스스로 판단해서 실행
- 콜백함수를 호출할 때 인자로 넘길 값과 순서에 대한 제어권
- 콜백함수의 this에 대한 결정
  ** 콜백함수의 this** 1) 무엇을 바라볼지 정해져 있는 경우 ⇒ 해당 객체 2) 정해지지 않은 경우 ⇒ 전역 객체 3) 사용자 임의로 변경하고 싶은 경우 ⇒ bind 메서드 활용

## 3. 콜백함수는 함수다

**콜백함수로 어떤 객체의 메서드를 전달하더라도, 그 메서드는 메서드가 아닌 함수로서 호출된다.**

예제를 통해 살펴보면,

```js
let obj = {
  vals: [1, 2, 3],
  logValues: function (v, i) {
    console.log(this, v, i);
  },
};
obj.logValues(1, 2); //result01
[4, 5, 6].forEach(obj.logValues); // result02
```

**결과**

![](https://images.velog.io/images/e_soojeong/post/d32471d7-4097-4b9c-8d8a-3609f81f3fa1/Untitled.png)

**logValue**는 <br/>
**result01** ⇒ 메서드 (dot이 있으니 메서드로서 전달 : 함수로 호출됨)

- this : obj
- v : 1
- i : 2

**realt02** ⇒ forEach함수의 콜백함수

- this : 전역객체(Window)
  `arr.forEach(callback(currentvalue[, index[, array]])[, thisArg])`
  ✔️ \_전역객체로 출력되는 이유 : obj를 this로 하는 메서드가 아닌 obj.logValues가 가리키는 함수만 전달 ⇒ 별도로 obj 인자를 지정하지 않는다면, obj와 직접적인 연관이 없다.
- v : 4, 5, 6 (CurrentValue)
- i : 0, 1, 2 (index)

[Array.prototype.forEach()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) : forEach MDN

## 4. 콜백 함수 내부의 this에 다른 값 바인딩하기

**콜백 함수 내부의 this가 객체를 바라보게 하는 방법**

- 클로저 : 전통적 방법
- bind 메서드 이용하는 방법

## 5. 콜백 지옥과 비동기 제어

### 동기와 비동기

#### 1. 동기와 비동기는 서로 반대의 개념이다.

- 동기 : 즉시 처리가 가능한 대부분의 코드
- 비동기 : 별도의 요청, 실행 대기, 보류가 필요한 코드 (언제 코드가 실행될지 예측할 수 없는 코드)

#### 2. 자바스크립트는 동기적이다.

- 호이스팅이 된 이후부터 코드가 작성한 순서(정해진)에 맞춰서 하나씩 동기적으로 실행된다.
- 호이스팅이란 ? var, function 등의 선언이 자동적으로 코드의 상단으로 옮겨지는 것

#### 3. Callback은 항상 비동기일까? Nope!

```js
// 1. 동기 콜백 : 즉각적

//printImmediately  함수가 호이스팅 되면서 맨위에서 실행되고 1,3,hello,2 순으로 콘솔 확인
function printImmediately(print) {
  print();
}
printImmediately(() => console.log('synchronous callback'));

// 2. 비동기 콜백 : 언제 실행될지 예측할 수 없는 콜백
function printWithDelay(print, timeout) {
  setTimeout(print, timeout);
}
printWithDelay(() => console.log('async callback'), 2000); // 비동기
```

[드림코딩 by 엘리](https://www.youtube.com/watch?v=s1vpVCrT8f4&feature=youtu.be)의 강의를 참고하였습니다.

## 콜백 지옥

콜백 함수 안의 콜백함수는 콜백 지옥을 초래할 수 있다. 가독성이 떨어지며, 에러 처리의 어려움이 있다.

**해결 방법**<br/><br/>
**1. 기명함수로 변환** : 일회성 함수를 전부 변수에 할당해야하는 단점

**2. Promise(ES6)** : new 연산자(Promise는 클래스이기 때문에 new 키워드 사용)와 함께 Promise 호출

- Promise : 비동기를 간편하게 처리할 수 있는 자바스크립트 내장 오브젝트
- resolve, reject 라는 executor 콜백 함수를 인자로 받음
- 정해진 시간에 기능을 수행하고나서 정상적으로 기능 수행(resolve)이되면 → 코드 진행 / 그렇지 않을 경우 → Error 오브젝트 반환(reject)
- state(오퍼레이션 수행 상태)

1.  pending(지정한 오퍼레이션 수행하고 있는 중)
2.  fulfilled(오퍼레이션 성공) or rejected(오퍼레이션 실패)

**3. Generator(ES6)** : \* 이 붙은 함수가 Generator 함수

- Generator 함수 : Generator는 빠져나갔다가 나중에 다시 돌아올 수 있는 함수
- Generator 함수 실행 ⇒ Iterator 반환 ⇒ Iterator 내의 next 메서드 호출 ⇒ Generator 함수 내 첫 번째 yield에서 함수 실행을 멈춤
  ⇒ 다시 next 메서드 호출하여 그 다음 yield에서 함수 실행을 멈춤 : 반복

즉, 비동기 작업이 완료되는 시점마다 next 메서드 호출하여 Generator 함수 내부 소스가 위 → 아래로 진행된다.

자세한 셜명은 [function\*](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/function*) MDN 참고

**4. Promise + async + await**

- async : 비동기 작업을 수행하고자 하는 함수 앞에 표기
- await : 함수 내부에서 실질적인 비동기 작업이 필요한 위치마다 표기

⇒ Promise 에서 then 체이닝을 계속하다보면 코드가 난잡해지는 것을 방지

[드림코딩 by 엘리](https://youtu.be/aoQSOZfz3vQ) 의 강의를 참고하였습니다.
