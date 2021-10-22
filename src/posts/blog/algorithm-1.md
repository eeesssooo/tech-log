---
title: 'Algorithm | H-Index'
category: 'Algorithm'
date: '2021-10-22 22:53:00 +09:00'
desc: 'programmers 정렬'
thumbnail: './images/code-block/thumbnail.jpg'
alt: 'sort'
---

**문제**<br/>
어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

**제한사항**<br/>
과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
논문별 인용 횟수는 0회 이상 10,000회 이하입니다.

**입출력 예**

| citations       | return |
| --------------- | ------ |
| [3, 0, 6, 1, 5] | 3      |

**입출력 예 설명**<br/>
이 과학자가 발표한 논문의 수는 5편이고, 그중 3편의 논문은 3회 이상 인용되었습니다. 그리고 나머지 2편의 논문은 3회 이하 인용되었기 때문에 이 과학자의 H-Index는 3입니다.

**풀이**<br/>
문제를 이해 자체가 어려웠다. 아래 링크를 통해서 h-index에 대한 이해를 완료한 뒤 문제를 해결하니 이해할 수 있었다.<br/>
https://www.ibric.org/myboard/read.php?Board=news&id=270333

**💻 &nbsp; point**

- 내림차순 정렬(인용된 횟수가 큰 순서로 정렬)
- 피인용수(citations(i))가 논문수(i)와 같아지거나 피인용수가 논문수보다 작아지기 시작하는 숫자가 바로 h(=answer)이다!

```js
function solution(citations) {
  let answers = 0;
  for (let i = 0; i < citations.length; i++) {
    if (i < citations[i]) {
      answers++;
    }
  }

  return answers;
}
```
