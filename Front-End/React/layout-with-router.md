# Route에 따라 다른 레이아웃 적용시키기

## react-router-dom 에서 제공하는 방식

Route nesting  
감싸는 루트에 element prop으로 레이아웃을 준다.

```jsx
//App.js
import { MainLayout, SubLayout } from "./components/layout";

<BrowserRouter>
  <Reset />
  <Routes>
    <Route element={<MainLayout />}>
      <Route path="/" element={<Home />} />
      <Route path="/bookmark" element={<Bookmark />} />
    </Route>
    <Route element={<SubLayout />}>
      <Route path="/login" element={<Login />} />
      <Route path="/register" element={<Register />} />
    </Route>
  </Routes>
</BrowserRouter>;
```

```jsx
//MainLayout.js
import { Outlet } from "react-router-dom";
//Outlet위치에 페이지 컨텐츠(nested route의 element)가들어간다

const MainLayout = () => {
  return (
    <Wrapper>
      <Header />
      <Outlet /> /
    </Wrapper>
  );
};
```

## 이렇게도 가능

```jsx
//App.js
import { MainLayout, SubLayout } from "./components/layout";

<BrowserRouter>
  <Reset />
  <Routes>
    <Route path="/" element={<MainLayout element={<Home />} />} />
    <Route path="/bookmark" element={<MainLayout element={<Bookmark />} />} />
    <Route path="/login" element={<SubLayout element={<Login />} />} />
    <Route path="/register" element={<SubLayout element={<Register />} />} />
  </Routes>
</BrowserRouter>;
```

```jsx
//MainLayout.js

const MainLayout = ({ element }) => {
  return (
    <Wrapper>
      <Header />
      {element}
    </Wrapper>
  );
};
```

```

```
