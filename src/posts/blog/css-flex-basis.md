---
title: 'CSS |flex-basis, flex-grow, flex-shrink'
category: 'CSS'
date: '2021-11-19 12:40:00 +09:00'
desc: 'flex-basis, flex-grow, flex-shrink'
thumbnail: './images/getting-started/thumbnail.jpg'
alt: 'flex-basis, flex-grow, flex-shrink'
---

flex를 심도 있게 공부하고 싶어서 레이아웃 잡는 것 외에 flex item에 적용하는 속성들에 대하여 학습하기로 하였다.

## 1. flex-basis

- 유연한 박스의 기본 영역. flex item들의 **기본 점유 크기**를 설정한다.
- width, height 와 다른점은 axis 방향에 따라 달라진다는 것이다. (flex-direction이 row일 때는 너비, column일 때는 높이)
- 기본 값은 `auto` 이며, 이때에는 width, height 값은 가 적용된다. 반대로, **flex-basis**가 적용되어 있다면 width, height 값은 무시되어 컨텐츠의 크기를 갖게된다.

## 2. flex-grow

- 유연하게 늘리기
- flex-grow는 아이템이 **flex-basis의 값보다 커질 수 있는지** 결정하는 속성이다.
- flex-grow에는 숫자값이 들어가며, 기본값인 `0` 보다 큰 값이 들어가면 해당 아이템이 빈 공간을 메우게 된다.
- flex-grow에 들어가는 숫자값은 아이템들의 flex-basis를 제외한 여백 부분을 flex-grow에 지정된 숫자의 비율로 나누어 가진다.

```
css
/* 1:2:1의 비율로 세팅할 경우 */
.item:nth-child(1) { flex-grow: 1; }
.item:nth-child(2) { flex-grow: 2; }
.item:nth-child(3) { flex-grow: 1; }
```

여백의 비는 정확히 1:2:1이다. 정수 뿐 아니라 소수 비율도 가능하다.

## 3. flex-shrink

- 유연하게 줄이기
- flex-shrink는 flex-grow와 쌍을 이루는 속성이다.
- flex-shrink는 **flex-basis의 값보다 작아질 수 있는지** 결정하는 속성이다.
- flex-shrink에는 숫자값이 들어가며, `0` 보다 큰 값이 들어가면 해당 아이템이 flex-basis보다 작아진다.
- 기본값은 `1` 이기 때문에 적용하지 않았어도 아이템이 flex-basis보다 작다.
- flex-shrink를 0 으로 적용하면 아이템의 크기가 flex-basis보다 작아지지 않기 때문에 고정폭의 컬럼을 만들 수 있다. 이때, 고정 크기는 width로 설정한다.

```
css
.container {
	display: flex;
}
.item:nth-child(1) {
	flex-shrink: 0;
	width: 100px;
}
.item:nth-child(2) {
	flex-grow: 1;
}
```

## 4. flex-grow, flex-shrink, flex-basis의 축약형 속성

서로 관련된 속성이기 때문에, 축약형을 쓰는 것이 편리하다. 단, 주의할 점은 flex: 1; 과 같이 flex-basis를 생략해서 쓰면 flex-basis의 값은 0 이다.

```
css

.item {
	flex: 1;
	/* flex-grow: 1; flex-shrink: 1; flex-basis: 0%; */
	flex: 1 1 auto;
	/* flex-grow: 1; flex-shrink: 1; flex-basis: auto; */
	flex: 1 500px;
	/* flex-grow: 1; flex-shrink: 1; flex-basis: 500px; */
}
```

**참고 자료** <br>
https://studiomeal.com/archives/197
