# sass의 부모선택자

- & 선택자가 자꾸 헷갈려서 정리..
- 부모 선택자는 선언되는 위치의 바로위 태그로 바꿔서생각

```html
<div>
  <main>
    <p class="pTag">
      <b></b>
    </p>
    <b></b>
  </main>
</div>
```

```scss
div {
  &:hover {
    color: red;
  }
}
div:hover {
  color: red;
}
div {
  :hover {
    color: red;
  }
}
/*셋 다 같은 코드. &자리에 div라고 생각. &뒤에 예시 처럼 가상셀렉터를 사용할 경우 생략이 가능*/

div {
  &:hover {
    color: red;
  }
}
div {
  & :hover {
    /*&뒤에 공백*/
    color: red;
  }
}
/*둘은 다른 코드. 아래처럼 공백을 넣을 경우 div 아래 main,p,b,태그에 적용 */
```

```scss
div {
  /* 1번 */
  &.pTag {
    color: red;
  }
}

div {
  /* 2번 */
  & .pTag {
    /* & 뒤에 공백 */
    color: red;
  }
}

div {
  /* 3번 */
  .pTag {
    color: red;
  }
}

/* 1번은 아무것도 선택되지 않는다. div 중에 pTag라는 클래스가 없기 때문
2번과 3번은 p태그가 선택됨.
가상 셀렉터과는 다르게 &를 생략할 경우 의미가 완전 바뀐다.
*/
```

```scss
b {
  p & {
    color: red;
  }
}
b {
  p > & {
    color: red;
  }
}
/* p 태그 아래에 있는 b태그만 선택됨 */
```

- 리액트 스타일드 컴포넌트 캡슐화에 응용가능
