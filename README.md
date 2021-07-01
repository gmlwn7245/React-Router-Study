## React
* Single-page application(SPA)로 하나의 HTML 페이지와 애플리케이션 실행에 필요한 JavaScript와 CSS 같은 모든 자산을 로드하는 애플리케이션
* 페이지 또는 후속 페이지가 상호작용할때 서버로부터 새로운 페이지를 불러오지 않기 때문에 다시 로드되지 않는다
* 하나의 페이지 내에서 컴포넌트만 변경시켜 부분만 추가하고 업데이트할 수 있다

## React Router DOM
* React의 화면 전환을 도와주는 기술
* 페이지 이동시 전체 페이지의 다시 로딩하지 않고 필요한 컴포넌트를 불러와 업데이트 해준다

## Router
* 모든 Router 구성요소에 대한 공통 저수준 인터페이스
```
import React from "react";
import ReactDOM from "react-dom";
import { Router } from "react-router";
import { createBrowserHistory } from "history";

const history = createBrowserHistory();

ReactDOM.render(
  <Router history={history}>
    <App />
  </Router>,
  node
);
```
* history : history 객체 탐색을 위해 사용
* < APP / > : 렌더링할 자식 요소


## React Router DOM Installation
```
npm install react-router-dom
```

## Hooks
#### 1. useHistory
* 화면 이동에 사용할 수 있는 history 인스턴스에 접근하게 해준다
* React에서 페이지를 이동할 수 있는 이유는 react-router-dom을 이용하여 페이지 기록을 알 수 있기 때문이다
* history는 브라우저 세션 기록에 접근할 수 있는 방법을 제공하는 인터페이스이다
* history의 push() 메소드를 이용하면 이동할 페이지 path와 넘겨줄 state 값을 props로 넘겨줄 수 있다

* import 문
```
import { useHistory } from 'react-router-dom';
```
* 사용 방법
```
let history = useHistory();
history.push(path, [state]);
```
* console로 history 객체를 출력하면 사용 가능한 여러 메소드 확인할 수 있다

#### 2. useLocation
* useLocation Hook은 현재 URL을 대표하는 location 객체를 반환한다
* URL이 바뀔때마다 새로운 location이 반환되는 useState와 비슷한 기능을 가진다
* useHistory에서 넘겨받은 state 값을 사용할 수 있다

* import 문
```
import { useLocation } from 'react-router-dom';
```
* 사용방법
```
let location = useLocation();
let content = location.state.필드명;
```

#### 3. useParams
* useParams Hook은 URL 매개변수의 key-value 객체를 반환한다

* import 문
```
import { useParams } from 'react-router-dom';
```
* 사용 방법 (1) Route 선언
```
<Route path="/topics/:id/:title">
    <Topic></Topic>
</Route>
```
* 사용 방법 (2) Topic 컴포넌트 내부
```
let params = useParams();
let id = params.id;
let title = params.title;
```

#### 4. useRouteMatch
* useRouteMatch Hook은 match 객체 값에 접근할 수 있게 해준다
* 인자로 Route 컴포넌트의 프로퍼티들을 가진 객체를 받을 수 있다
* 만약 path 프로퍼티와 현재 페이지의 URL이 일치한 경우 해당 path의 match 객체를 반환하고 일치하지 않을 경우 null을 반환한다
* match 객체는 어떤 Route에 매칭이 되었는지에 대한 정보가 있고 params(/about/:name) 형식의 정보를 가지고 있다

* import 문
```
import { useRouteMatch } from "react-router-dom";
```
* 기존 사용방법
```
function BlogPost() {
  return (
    <Route
      path="/blog/:slug"
      render={({ match }) => {
        // Do whatever you want with the match...
        return <div />;
      }}
    />
  );
}
```
* useRouteMatch 사용
```
function BlogPost() {
  let match = useRouteMatch("/blog/:slug");

  // Do whatever you want with the match...
  return <div />;
}
```

## API
#### 1. < BrowserRouter >
* HTML5의 history API를 이용하여 UI 업데이트
* 동적인 페이지에 적합
* Link 컴포넌트 to 속성에 이동할 경로 기술
* Route 컴포넌트 path 속성을 Link의 to속성과 매핑 Component에 컴포넌트 경로 기술
* 새로고침 하면 경로 못찾아서 에러남
```
<BrowserRouter
  basename={optionalString}
  forceRefresh={optionalBool}
  getUserConfirmation={optionalFunc}
  keyLength={optionalNumber}
>
  <App />
</BrowserRouter>
```
* basename(String) : 모든 위치의 기본 URL
* forceRefresh(bool) : true 라우터가 페이지 탐색에서 전체 페이지 새로고침을 사용하는 경우 이를 사용하여 기존 서버 렌더링 앱이 페이지 탐색 사이에 전체 페이지 새로 고침으로 작동하는 방식을 모방할 수 있음 
* getUserConfirmation(func) : 네비게이션 확인에 사용하는 기본 기능
* keyLength(Number) : location.key의 길이

#### 2. < HashRouter >
* URL의 hash를 활용한 라우터
* 주소에 #이 붙음 (검색 엔진으로 읽지 못함)
* 정적인 페이지에 적합
```
<HashRouter
  basename={optionalString}
  getUserConfirmation={optionalFunc}
  hashType={optionalString}
>
  <App />
</HashRouter>
```
* hashType(String) : window.laction.hash에 사용할 인코딩 유형

#### 3. < Link >
* 애플리케이션에 대해 선언적이고 엑세스가 가능한 탐색 제공
```
<Link to="/about">About</Link>
```
* to(String) : 위치의 경로 이름

#### 4. < NavLink >
* 현재 URL과 일치할 때 렌더링 된 요소에 스타일 지정 속성을 추가하는 Link의 특수 버전
```
<NavLink to="/about">About</NavLink>
```





`Reference`

[ReactRouter-API](https://reactrouter.com/web/api/Hooks "ReactRouter-API")
[Blog1](https://explain-programming.tistory.com/3 "블로그")
[Blog2](https://codingbroker.tistory.com/72 "블로그")