---
title: 'Algorithm | 로또의 최고 순위와 최저 순위'
category: 'Algorithm'
date: '2021-11-01 22:53:00 +09:00'
desc: 'programmers 2021 Dev-Matching: 웹 백엔드 개발자(상반기)'
thumbnail: './images/code-block/thumbnail.jpg'
alt: 'sort'
---

#### 문제

로또의 최고 순위와 최저 순위 문제 확인 👉 https://programmers.co.kr/learn/courses/30/lessons/77484

**나의 풀이**

```javascript
function solution(lottos, win_nums) {
  //교집합 찾기
  let intersection = lottos.filter((x) => win_nums.includes(x));
  //교집합의 갯수 찾기
  let intersectionCount = lottos.length - intersection.length + 1;

  // 교집합이 있는 경우, 없는 경우를 나누어서 출력
  if (intersection.length == 0) {
    intersectionCount = lottos.length - intersection.length;
  } else {
    intersectionCount = lottos.length - intersection.length + 1;
  }

  //0의 갯수 구하기
  let countZero = lottos.filter((element) => 0 === element).length;

  //로또의 최고 순위 구하기
  let lottosMax = intersectionCount - countZero;

  //최고 순위의 조건  분기처리
  if (countZero == 6) {
    lottosMax = lottosMax + 1;
  } else {
    lottosMax;
  }

  const answer = [lottosMax, intersectionCount];

  return answer;
}
```

최소, 최대 당첨 순위를 계산 했지만 구할 때마다 경우의 수를 나누어 처리하는게 불필요하다고 생각했다.
그리고 개인적으로 나의 코드와 유사한 필터를 가졌지만, rank라는 배열을 기준으로 한 다른 사람의 풀이를 보았다.

✏️ **내 코드와의 차이점**

- zeroCount를 t/f로 분기처리하였다.
  (단, '0을 제외한 다른 숫자들은 lottos에 2개 이상 담겨있지 않습니다.'라는 제한 사항이 있어서 가능한 부분이다.)
- rank라는 순위가 담긴 기준 배열을 만들었다.

- 나는 count를 할 때, 기존 lottos 배열의 length에서 새롭게 구한 배열의 length를 출력하면서, 값에 따라서 +1을 해주어야하는 경우의 수를 굳이 나누어 처리하였지만 rank라는 배열을 기준으로 잡아 처리할 경우엔 index의 특성(0부터 카운트) 그러한 처리 자체가 불필요하다.

**다른사람 풀이**

```javascript
function solution(lottos, win_nums) {
  const rank = [6, 6, 5, 4, 3, 2, 1];

  let minCount = lottos.filter((v) => win_nums.includes(v)).length;
  let zeroCount = lottos.filter((v) => !v).length;

  const maxCount = minCount + zeroCount;

  return [rank[maxCount], rank[minCount]];
}
```
