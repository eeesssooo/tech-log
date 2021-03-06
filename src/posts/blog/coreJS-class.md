---
title: 'Core Javascript | 클래스'
category: 'Javascript'
date: '2021-10-16 11:00:00 +09:00'
desc: '코어 자바스크립트 책을 보며 공부한 내용입니다.'
thumbnail: './images/markdown-test/thumbnail.jpg'
alt: '코어 자바스크립트를 보며 공부한 내용입니다.'
---

## 0. 들어가며

**자바스크립트는 프로토타입 기반 언어이다** <br/>
=> '상속'의 개념이 없어 상속에 대한 니즈가 발생하였다. <br/>
=> ES6에서 클래스 문법이 추가되었다.

## 1. 클래스와 인스턴스의 개념 이해

### 1-1. 클래스란?

> 어떤 사물의 공통 속성을 모아 정의한 추상적인 개념

- **상위 클래스(superclass)**
  같은 클래스에서 상위(superior)의 개념을 갖는 것
- **하위 클래스(subclass)**
  상위 클래스의 조건을 충족하면서 더욱 구체적인 조건이 추가된 것

### 1-2. 인스턴스란?

> 클래스의 속성이지니는 구체적인 사례

### 1-3. 프로그래밍 언어에서의 클래스

- **공통 요소를 지니는 집단을 분류하기 위한 개념**
- 클래스가 먼저 정의 되어야 공통적인 요소를 지니는 개체들을 생성할 수 있다.
- 사용에 따라 추상적 or 구체적 개체가 될 수 있다.

## 2. 자바스크립트의 클래스

- **프로토타입 메서드**
  인스턴스에서 직접 호출 할 수 있는 메서드
- **스태틱 메서드**
  인스턴스에서 직접 접근할 수 없는 메서드
  (생성자 함수를 this로 해야만 호출 가능)

  **1-3**에서 언급한 "사용에 따라 추상적 or 구체적 개체가 될 수 있다."는 것의 의미는 아래와 같다.

1.  Class가 프로토타입 메서드의 역할을 할 때에는 추상적 개체가 되고
2.  Class가 스태틱 메서드의 역할을 할 경우, 클래스 자체가 하나의 개체로 취급된다.

## 3. 클래스 상속(ES6 이전)

### 클래스 상속을 흉내내기 위한 방법 3

**전제조건** : constructor 프로퍼티가 원래의 생성자 함수를 바라보도록 조정해야한다.

- SubClass.prototype에 SuperClass의 인스턴스 할당 => 다음 프로퍼티를 모두 삭제
- 빈 함수(Bridge)를 활용하는 방법
- Object.create를 이용하는 방법

## 4. 클래스 상속(ES6)

```javascript
var Rectangle = class {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }
  getArea() {
    return this.width * this.height;
  }
};

//ES6 클래스 문법 도입
var Square = class extends Rectangle {
  constructor(width) {
    super(width, width);
  }
  getArea() {
    console.log('size is :', super.getArea());
  }
};
```

- **class** 명령어 뒤에 '**extends**'라는 키워드를 추가하면 상속관계 설정이 끝난다.
- constructor 내부에서 **super** 라는 키워드를 함수처럼 사용할 수 있다. 이 함수는 SuperClass의 constructor를 실행한다
- constructor 메서드를 제외한 다른 메서드에서는 super 키워드를 객체처럼 활용할 수 있다. 이때, 객체는 SuperClass.prototype을 바라보는데, 호출한 메서드의 this는 'super'가 아닌 원래의 this를 그대로 따른다.
