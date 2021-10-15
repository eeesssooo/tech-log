---
title: 'CSS | Attribute Selector(CSS 속성 선택자)'
category: 'CSS'
date: '2021-10-15 10:00:00 +09:00'
desc: 'CSS Attribute Selector'
thumbnail: './images/getting-started/thumbnail.jpg'
alt: 'CSS Attribute Selector'
---

SCSS로 UI를 스타일링하면서, 공통의 attribute가 있다면 이를 통하여 스타일 속성을 지정하는 것이 편리할 것이라고 생각을 하였다. class, lang, href 등 다양한 attribute를 적용할 수 있다.

## 속성 선택자 정리

-`[attr]` : attr이라는 이름의 특성을 가진 요소를 선택합니다. <br/> -`[attr=value]` : attr이라는 이름의 특성값이 정확히 value인 요소를 선택합니다.<br/> -`[attr~=value]` : attr이라는 이름의 특성값이 정확히 value인 요소를 선택합니다. attr 특성은 공백으로 구분한 여러 개의 값을 가지고 있을 수 있습니다. 즉, 여러 개의 class가 함께 지정되어 있어도 attr를 특성값으로 가졌다면 선택합니다. <br/> -`[attr|=value]` : attr이라는 특성값을 가지고 있으며, 그 특성값이 정확히 value이거나 value로 시작하면서 -(U+002D) 문자가 곧바로 뒤에 따라 붙으면 이 요소를 선택합니다. 즉, 시작하는 요소로 선택하되, 하이픈이 붙어있는 요소들도 선택합니다. 보통 언어 서브코드(en-US, ko-KR 등)가 일치하는지 확인할 때 사용합니다. <br/> -`[attr^=value]` : attr이라는 특성값을 가지고 있으며, 접두사로 value가 값에 포함되어 있으면 이 요소를 선택합니다.<br/> -`[attr$=value]` :
attr이라는 특성값을 가지고 있으며, 접미사로 value가 값에 포함되어 있으면 이 요소를 선택합니다. <br/> -`[attr*=value]` : attr이라는 특성값을 가지고 있으며, 값 안에 value라는 문자열이 적어도 하나 이상 존재한다면 이 요소를 선택합니다. <br/> -`[attr operator value i]` : 괄호를 닫기 전에 i 혹은 I를 붙여주면 값의 대소문자를 구분하지 않습니다. (ASCII 범위 내에 존재하는 문자에 한해서 적용됩니다) <br/> -`[attr operator value s]` : 괄호를 닫기 전에 s 혹은 S를 붙여주면 값의 대소문자를 구분합니다. (ASCII 범위 내에 존재하는 문자에 한해서 적용됩니다)

## 속성 선택자 예제

`a` 태그를 예제로 보면,

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
