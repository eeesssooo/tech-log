---
title: 'CSS | perspective를 활용한 tarot card'
category: 'CSS'
date: '2021-11-10'
desc: 'perspective'
thumbnail: './images/getting-started/thumbnail.jpg'
alt: 'perspective'
---

3차원의 공간을 위해서는 원근감이 필요하다. 이때 사용할 수 있는 arribute는 perspective이다. 이전에는 사용 빈도수가 얼마나 될까? 라는 생각을 가졌다면, 최근에는 메타버스의 등장으로 더욱 주목받고 있는 arribute인 perspective에 대하여 학습하였다.

> 참고 문헌

- https://developer.mozilla.org/en-US/docs/Web/CSS/perspective
- https://imjignesh.com/how-css-perspective-works/
- https://3dtransforms.desandro.com/card-flip
- https://nykim.work/26

## 1. perspective란?

- perspective는 우리가 대상을 보는 거리
- 값이 적을수록 더 가까이 보게 되므로 효과가 더 극적으로 나타나게 된다. 예를 들어 같은 각도로 기울어진 물체를 멀리서 볼 때와 가까이서 볼 때, 가까이서 보게 되었을 때 그 기울어진 정도가 더 크게 느껴진다.

아래의 코드와 이미지를 통해서 이해를 해보자면,

```
css
 .origin {
    width: 200px;
    height: 200px;
    border: 1px solid black;
    margin: 100px auto;
    /*첫 번째 그림*/
    perspective: 100px;
    /*두 번째 그림*/
    perspective: 400px;
}

.rotate-pannel {
    width: 200px;
    height: 200px;
    background: red;
    transform: rotateX(45deg);
}
```

```
html

<div class="origin">
     <div class="rotate-pannel"></div>
</div>
```

![](https://images.velog.io/images/e_soojeong/post/2ae2f1ee-123f-4abd-9df3-2f31657118c7/image.png)
![](https://images.velog.io/images/e_soojeong/post/c003675e-9b27-43d6-901c-7fc2934d1108/image.png)

같은 각도로 rotateX(45deg) 되었지만, perspective의 값에 따라서 `perspective: 100px;`일 때와 `perspective: 400px;` 일 때의 원근감은 크게 나타남을 알 수 있게 되었다.

## 2. Y축의 소실점

![](https://images.velog.io/images/e_soojeong/post/f2bad8ed-8551-4565-b540-e0ade6972501/image.png)

이 화면은 아래의 코드를 입력하였을 때, 보이는 화면이다. 하나를 기준으로 rotate 할 때에는 몰랐는데, 여려 개의 박스에 적용하니 서로 다른 모습을 보이고 있다.

```
html
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>perspective</title>
<style>
  .origin {
    display: flex;
    justify-content: space-between;
    width: 1000px;
    height: 200px;
    border: 1px solid black;
    margin: 100px auto;
    perspective: 400px;
  }

  .pannel {
    width: 200px;
    height: 200px;
    background: aqua;
    transform: rotateY(45deg);
  }
</style>
</head>
<body>
  <div class="origin">
    <div class="pannel"></div>
    <div class="pannel"></div>
    <div class="pannel"></div>
    <div class="pannel"></div>
    <div class="pannel"></div>
    <div class="pannel"></div>
  </div>
</body>
</html>
```

그 이유는, perspective 속성을 부모 요소에 적용하였기 때문에 pannel들이 서로 다른 투영점(perspective) 즉, 다른 소실점(vanishing point)을 갖고 있기 때문이다.

## 3. 동일한 perspective 설정하기

### 3-1. 자식 요소에 transform 속성의 값으로 perspetive를 주고, 괄호 안에 수치를 입력

```
css
	.origin {
    display: flex;
    justify-content: space-between;
    width: 1000px;
    height: 200px;
    border: 1px solid black;
    margin: 100px auto;
    }

  .pannel {
    width: 200px;
    height: 200px;
    background: aqua;
    transform: perspective(400px);
    rotateY(45deg);
    }
```

### 3-2. 부모 요소에 perspective-origin 사용

- 소실점이 어디있는가를 나타내는 속성
- 기본 값은 `perspective-origin: 50% 50%;`

```
css
.origin {
    display: flex;
    justify-content: space-between;
    width: 1000px;
    height: 200px;
    border: 1px solid black;
    margin: 100px auto;
    perspective-origin: 50% 50%;
}

.pannel {
    width: 200px;
    height: 200px;
    background: aqua;
    transform: rotateY(45deg);
}
```

## 4. perspective와 grid를 활용한 타로카드 뽑기

![](https://images.velog.io/images/e_soojeong/post/04aebbf7-9994-40bb-aa1e-6404eb2eb4af/IMB_Vc3zPs.GIF)

✏️ **설계**

1. 처음엔 perspective를 활용하여 어떻게 앞, 뒤를 나타낼 수 있을까 고민했다. 블로그에서 힌트를 얻어서 앞, 뒤를 나타내는 요소를 만들고 이를 하나의 카드처럼 보일 수 있게 위치 조정을 해주었다.

2. `transform-style: preserve-3d`는 이 perspective를 부모로부터 받아 자신을 통과해 자식까지 전달한다.

3. `backface-visibility: hidden`는 3D Transform에서 요소의 뒷면을 숨기는 역할을 한다. hidden 처리하지 않으면 앞면/뒷면이 함께 보이는 문제가 발생한다.

4. https://imjignesh.com/how-css-perspective-works/ 과 https://nykim.work/26 를 참고하여 구현하였다.

5. 위치는 grid를 활용하여 한 줄에 5개의 카드가 나타날 수 있도록 하였다.

📒 **나의 생각** <br>
역시 만들고 싶은 것을 만들면 더 열심히 그리고 재미나게 배울 수 있었다. 그리고 모든 것을 알지 못해도, 원하는 것에 대하여 구글링하며 참조하면 구현이 가능하다는 것도 또 다시 깨달았다. 여기서도 추가로 구현하고 싶은 것들이 생각이 났는데, JS를 적용하여 해당하는 카드를 클릭했을 때, 모달 창이 떠서 해당 카드에 대한 설명을 사용자에게 전달해주면 이게 바로..! 온라인 타로가 아닐까? 하는 생각과 함께 이걸 더 디벨롭하면 심리테스트나, mbti 같은 재미난 결과값을 보여주는 프로젝트를 만들 수 있을 것이라고 생각했다. 결론은 레이아웃 구성한 마크업에 JS를 달아보는 일을 꼭 하자는 것..!
