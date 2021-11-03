---
title: 'Algorithm | 신규 아이디 추천'
category: 'Algorithm'
date: '2021-11-03 22:53:00 +09:00'
desc: '2021 KAKAO BLIND RECRUITMENT'
thumbnail: './images/code-block/thumbnail.jpg'
alt: 'sort'
---

#### 문제

로또의 최고 순위와 최저 순위 문제 확인 👉 https://programmers.co.kr/learn/courses/30/lessons/72410

**나의 풀이**

```javascript
function solution(new_id) {
  // 1단계
  new_id = new_id.toLowerCase();
  // 2단계
  new_id = new_id.replace(/[^\w\.\-]/g, '');
  // 3단계
  new_id = new_id.replace(/[\.]{2,}/g, '.');
  // 4단계
  new_id = new_id.replace(/^\./, '');
  // 4단계
  new_id = new_id.replace(/\.$/, '');
  // 5단계
  if (!new_id) {
    new_id = 'a';
  }
  // 6단계
  if (new_id.length >= 16) {
    new_id = new_id.slice(0, 15);
    new_id = new_id.replace(/\.$/, '');
  }
  // 단계
  if (new_id.length <= 2) {
    new_id = new_id.padEnd(3, new_id.split('').reverse().join(''));
  }
  return new_id;
}
```

문제를 보고, 1-7 단계를 하나씩 해결하자고 생각하였다.

<strong>1단계</strong> 소문자로 치환 : toLowerCase()<br>
<strong>2단계</strong> 특정 문자 제거 : replace()<br>
<strong>3단계</strong> 특정 문자 치환 : replace()<br>
<strong>4단계</strong> 특정 문자 제거 : replace()<br>
<strong>5단계</strong> 'a' 대입 : 직접 대입<br>
<strong>6단계</strong> 조건문, 특정 문자 제거 : slice(), replace()<br>
<strong>7단계</strong> 조건문, 특정 문자 추가(기존 문자열의 맨 끝) : padEnd(), split().reverse().join()<br>

메서드들을 적용하기 전, array에 익숙해져 있어 String을 array안에 각각 담아서 적용하려고 했다. 하지만 array에 적용되는 메서드 말고 String에 적용할 수 있는 메서드를 찾아서 적용하였다.

그렇게 새롭게 알게된 javascript 메서드 `padEnd()`이었다. `padEnd()`, `padStart()`는 메서드는 현재 문자열의 시작을 다른 문자열로 채워, 주어진 길이를 만족하는 새로운 문자열을 반환한다. 메서드 이름에서도 추론할 수 있 듯이, `padEnd()`의 채워넣기는 대상 문자열의 끝(우측)부터 적용됩니다. `padStart()`의 채워넣기는 대상 문자열의 시작(좌측)부터 적용된다.

<i>참고링크</i><br>
<b>padStart()</b><br>
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/padStart <br>
<b>padEnd()</b><br>
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/padEnd

**다른사람 풀이**

```javascript
function solution(new_id) {
  const answer = new_id
    .toLowerCase() // 1
    .replace(/[^\w-_.]/g, '') // 2
    .replace(/\.+/g, '.') // 3
    .replace(/^\.|\.$/g, '') // 4
    .replace(/^$/, 'a') // 5
    .slice(0, 15)
    .replace(/\.$/, ''); // 6
  const len = answer.length;
  return len > 2 ? answer : answer + answer.charAt(len - 1).repeat(3 - len);
}
```

✏️ **내 코드와의 차이점**

- 모든 코드가 체이닝 기법으로 적용되었다.
- 정규 표현식을 사용하여 특정 문자를 제거하고, 치환하고, 대입하였다
- 나는 맨 마지막 문자열을 찾기 위해서 기존 문자열을 거꾸로 변환하여 반복하였다. 하지만 다른 사람의 코드에서는 맨 마지막, 7단계의 경우는 조건식을 return 하였다. 이때 적용된 메서드는 charAt(), repeat()로 적용하여 마지막 글자를 찾아서 반복되게 적용하였다.

<i>참고링크</i><br>
<b>charAt()</b><br>
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/charAt
<b>repeat()</b><br>
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/repeat
