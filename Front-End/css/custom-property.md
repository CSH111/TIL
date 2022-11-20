# css의 커스텀 프로퍼티(변수)

## 기본

- `--`로 시작하는 커스텀 프로퍼티를 만들어 변수로 사용할 수 있다.
- 변수를 호출하고자 할 때에는 `var(변수)` 이용
- `var()` 의 두번째 인자에 기본값을 설정할 수 있다.

```css
p {
  --color-blue: skyBlue;

  backgroud-color: var(--color-blue, coral);
}
```

<br>

- 정의된 태그의 자손 태그에서 호출가능

```html
<style>
  p {
    --color-blue: skyBlue;
  }
  b {
    background-color: var(--color-blue, coral);
  }
</style>

<body>
  <p>하이<b>skyBlue 적용</b>하이</p>
  <b>coral 적용, p의 하위가 아니기때문에 --color-blue가 빈값</b>
</body>
```

<br>

## 응용1 - css 파일만을 이용한 전역(?) variable 이용

- document의 최상위 태그인 html태그에 변수들을 선언해 놓으면 어디서든 자유롭게 호출해서 사용할 수 있다.
- html 대신 알아서 최상위 태그를 찾아주는 `:root` 가상셀렉터 이용가능

```html
<style>
  html {
    --color-blue: skyBlue;
  }
  /* 가상셀럭터를 쓸경우 */
  :root {
    --color-blue: skyBlue;
  }

  h1 {
    background-color: var(--color-blue, coral);
  }

  h2 {
    background-color: var(--color-blue, coral);
  }
</style>

<body>
  <h1>skyBlue 적용</h1>
  <h2>skyBlue 적용</h2>
</body>
```

## 응용2 다이나믹 변수 선언- 반응형 웹 적용

```css
/* 사스 문법 가정 */
/* 포인팅 기기가 없는 모바일 등 기기일 때 높이를 크게 만드는 반응형 */
:root {
  --min-box-height: 20px;

  @media (pointer: coarse) {
    --min-box-height: 30px;
  }
}

.responsiveBox {
  min-height: var(--min-height);
}
```
