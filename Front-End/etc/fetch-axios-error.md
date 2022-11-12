# fetch API와 axios의 에러처리

- axios가 익숙했던 나....

## axios

```js
axios
  .post("/api/session", body)
  .then((res) => {
    console.log(res.data);
  })
  .catch((err) => {
    if (err.response) {
      //서버로부터 직접 에러를 응답받음
      alert(err.response.data.msg);
      //서버에서 보내준 메세지가 있다고 가정

      //없다면?
      switch (err.response.status) {
        case 400:
          alert("잘못된 요청입니다.");
        case 403:
          alert("권한이 없습니다.");
        // ...
      }
      return;
    }
    if (error.request) {
      // 서버로부터 응답을 못받음
      alert("서버장애 발생");
      return;
    }
    alert("알수 없는 에러"); // 요청을 날리는 중 에러발생
  });
```

- axios는 서버로부터 받은 응답을 분석해서 에러를 캐치해준다.
- fetch는 아님..

<br>

## fetch API

```js
fetch("/api/todo")
  .then((res) => {
    if (!res.ok) {
      throw Error(); // 에러처리 1
    }
    return res.json();
  })
  .then((data) => {
    console.log(data);
  })
  .catch((err) => {
    console.log(err); //에러처리 2
  });
```

- 직접 `Error`를 `throw`하는 에러처리1이 없다면 `.catch`는 서버에서 던져주는 에러를 인지하지 못한다.
- fetch API에서 `.catch`로 잡을 수 있는 상황은 request 자체를 날리못했을 때 뿐이다.
- 서버가 꺼져있든, 없는 api주소로 요청을 날리든 응답으로 항상 response객체를 받아오며 거기의 `response.ok`의 불리언 값만 바뀐다. 그를 이용해 `.catch`가 반응할 수 있도록 에러를 'throw'해야한다. (물론 then에서 if 이용해서 처리 해도 상관없긴 하다.)
- 이후 캐치에서 다양한 에러에 반응하게끔 처리하면된다.

```js
// 에러처리 예시

fetch("/api/todo")
  .then((res) => {
    if (!res.ok) {
      throw Error(${res.status}); // status: 400,401...
    }
    return res.json();
  })
  .then((data) => {
    console.log(data);
  })
  .catch((err) => {
    switch (err.message) {    // 에러처리
      case '400' : alert('잘못된 요청입니다.')
      case '403' : alert('권한이 없습니다.')
      case '500' : alert('서버에러')
      // ...
    }
  });
```

```js
// 만약 서버에서 직접 메세지를 준다면?
// response 를 파싱해야만 그 메세지를 이용할 수 있다.
//
fetch("/api/todo")
  .then((res) => {
    return res.json();
  })
  .then((data) => {
    if(서버에서 보내주는 것으로 조건처리){ //에러조건
      throw new Error(`${data.msg}`) //서버에서 보낸객체이름.msg로 가정
    }
    console.log(data);  //성공처리
  })
  .catch((err) => {
    alert(err.messsage) // messsage 는 내장 객체
  });
```
