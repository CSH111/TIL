# 리액트+노드 프로젝트 진행

## cors 이슈의 발생이유

리액트 개발단계

http://localhost:3000

노드 서버

http://localhost:5000

둘은 프로토콜과 호스트는 일치 하지만 포트가 다름 ⇒ SOP 원칙 위배 ⇒cors이슈 발생

build 후 같은 경로의 파일을 5000번 포트에서 sendfile 하기 때문에 SOP원칙 ok

최종 배포 후에는 어떤일이?

한 서버에서 클라이언트와 서버 사이드를 같이 배포할시 SOP충족. (같은포트 일때)

## 해결책(리액트)

```jsx
npm i http-proxy-middleware

// src/setupProxy.js

const { createProxyMiddleware } = require("http-proxy-middleware");

module.exports = function (app) {
  app.use(
    "/api",
    createProxyMiddleware({
      target: "http://localhost:5000",  //서버 포트
      changeOrigin: true,
    })
  );
};

```

위와 같이 프록시 설정한 뒤 react 재시작 해야함.
