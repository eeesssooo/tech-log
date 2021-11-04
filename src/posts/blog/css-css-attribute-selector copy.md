---
title: 'CSS | Attribute Selector(CSS 속성 선택자)'
category: 'CSS'
date: '2021-11-03 23:00:00 +09:00'
desc: 'CSS Attribute Selector'
thumbnail: './images/getting-started/thumbnail.jpg'
alt: 'CSS Attribute Selector'
---

우리에게 익숙한 태그의 이름, 클래스 이름, ID외의 선택자 외에도 여러 선택자들이 있다. 복합 선택자, 속성 선택자, 가상 선택자가 그것이다. 그 중 나에게 낯설어서 기록하게 된 선택자인 **Attribute Selector**에 대하여 기록하고자 한다.

SCSS로 UI를 스타일링하면서, 공통의 attribute가 있다면 이를 통하여 스타일 속성을 지정하는 것이 편리할 것이라고 생각을 하였다. class, lang, href 등 다양한 attribute를 적용할 수 있다.

## Attribute Selector

**정의**<br>
`속성 선택자` : 태그가 가진 속성으로 접근할 수 있는 선택자

**형태**

```css
/* css */
a[title] {
}
a[href="https://example.com"]
{
}
input[type='text'] {
}
```

```html
<!-- html -->
<a href="https://example.com">클릭</a>
```

단, 예시를 위한 형태일 뿐, `a` 태그가 아닌 모든 태그의 속성에 적용 가능하다.

## 속성 선택자 정리

-`[attr]` : attr이라는 이름의 특성을 가진 요소를 선택한다. <br/> -`[attr=value]` : attr이라는 이름의 특성값이 정확히 value인 요소를 선택한다.<br/> -`[attr~=value]` : attr이라는 이름의 특성값이 정확히 value인 요소를 선택한다. attr 특성은 공백으로 구분한 여러 개의 값을 가지고 있을 수 있다. 즉, 여러 개의 class가 함께 지정되어 있어도 attr를 특성값으로 가졌다면 선택한다. <br/> -`[attr|=value]` : attr이라는 특성값을 가지고 있으며, 그 특성값이 정확히 value이거나 value로 시작하면서 -(U+002D) 문자가 곧바로 뒤에 따라 붙으면 이 요소를 선택한다. 즉, 시작하는 요소로 선택하되, 하이픈이 붙어있는 요소들도 선택한다. 보통 언어 서브코드(en-US, ko-KR 등)가 일치하는지 확인할 때 사용한다. <br/> -`[attr^=value]` : attr이라는 특성값을 가지고 있으며, 접두사로 value가 값에 포함되어 있으면 이 요소를 선택한다.<br/> -`[attr$=value]` :
attr이라는 특성값을 가지고 있으며, 접미사로 value가 값에 포함되어 있으면 이 요소를 선택한다. <br/> -`[attr*=value]` : attr이라는 특성값을 가지고 있으며, 값 안에 value라는 문자열이 적어도 하나 이상 존재한다면 이 요소를 선택한다. <br/> -`[attr operator value i]` : 괄호를 닫기 전에 i 혹은 I를 붙여주면 값의 대소문자를 구분하지 않는다. (ASCII 범위 내에 존재하는 문자에 한해서 적용된다.###) <br/> -`[attr operator value s]` : 괄호를 닫기 전에 s 혹은 S를 붙여주면 값의 대소문자를 구분한다. (ASCII 범위 내에 존재하는 문자에 한해서 적용된다.)

## 속성 선택자 예제

### **태그[속성이름]**

`속성이름` 에 해당되는 속성을 가진 태그를 모두 선택한다.

```css
a[href] {
  color: red;
}
```

### **태그[속성이름="변수"]**

`속성이름` 의 속성값이 `변수`와 일치하는 태그를 선택한다.

```css
a[href="https://example.com"]
{
  color: red;
}
```

### **태그[속성이름~="변수"]**

`속성이름` 의 속성값이 `변수` 를 포함하는 태그를 선택한다.**(단어)**

```css
a[href~='example'] {
  color: red;
}
```

### **태그[속성*="변수"]**

`속성` 의 속성값이 `변수` 를 포함하는 태그를 선택한다.**(문자열)**

```css
a[href*='exam'] {
  color: red;
}
```

🐣 `태그[속성~="변수"]` 와 `태그[속성*="변수"]` 의 차이가 궁금해졌다.

- `~=` 는 **단어**를 기준으로, `*=` 는 **문자열**을 기준으로 판단하여 선택 한다.
- `*=` 은 문자열을 기준으로 `example` 안에 `exam`이 포함되면 선택한다.
- `~=` 은 단어를 기준으로 `exam` 와 `example` 를 다르다고 인식하여 선택하지 않는다.

### **태그[속성^="변수"]**

`속성` 의 속성값이 `변수` 로 시작하는 태그를 선택한다.

```css
a[href^='https'] {
  color: red;
}
```

### **태그[속성$="변수"]**

`속성` 의 속성값이 `변수` 로 끝나는 요소를 선택한다.

```css
a[href$='com'] {
  color: red;
}

a[href$='.hwp'] {
  color: red;
}
```

### **태그[속성|="변수"]**

`속성` 의 속성값이 `변수` 이거나 `변수` 로 시작하는 태그를 선택한다.

```css
a[href|='https'] {
  color: red;
}
```

### MDN에 적용된 예제도 함께 살펴 보았다.

**CSS**

```css
a {
  color: blue;
}

/* Internal links, beginning with "#" */
a[href^='#'] {
  background-color: gold;
}

/* Links with "example" anywhere in the URL */
a[href*='example'] {
  background-color: silver;
}

/* Links with "insensitive" anywhere in the URL,
   regardless of capitalization */
a[href*='insensitive' i] {
  color: cyan;
}

/* Links with "cAsE" anywhere in the URL,
with matching capitalization */
a[href*='cAsE' s] {
  color: pink;
}

/* Links that end in ".org" */
a[href$='.org'] {
  color: red;
}

/* Links that start with "https" and end in ".org" */
a[href^='https'][href$='.org'] {
  color: green;
}
```

**HTML**

```html
<ul>
  <li><a href="#internal">Internal link</a></li>
  <li><a href="http://example.com">Example link</a></li>
  <li><a href="#InSensitive">Insensitive internal link</a></li>
  <li><a href="http://example.org">Example org link</a></li>
  <li><a href="https://example.org">Example https org link</a></li>
</ul>
```

**결과**
![](https://images.velog.io/images/e_soojeong/post/6bbddfe2-b770-4a90-9db8-0432e03e5dbc/image.png)

**참고문헌** <br/>
https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors
