### 😲 시작하기에 앞서

나에게 있어 **Redux**란 <code>React</code> 라이브러리 중 **Redux**라는 것이 있고
전역으로 상태를 관리하는, 상태관리 **React** 라이브러리 라고 알고있었다.
최근 이상형월드컵 프로젝트를 <code>state</code>를 더 깔끔하고 관리하기 쉽게
**Redux**를 공부하자고 마음먹었고 개념이나 혹은 잘못 알고있었던 부분에
대해서 포스팅하고 추후 최근 프로젝트에 적용시키려고 한다.

## 1. Redux, Redux란?

**Redux**는
기본적으로 <code>JavaScript Application</code>들의 <code>State</code>를 관리하는 방법이다.

**Redux**는 <code>React</code>와 별개다.

**Redux**는
<code>Angular.js</code>에서도 쓸 수 있고,
<code>Vue.js</code>에서도 쓸 수 있고,
<code>Vanilla JavaScript</code>에서도 쓸 수 있고
내가 원하는곳에서 다 쓸 수 있다.
현재..!
**Redux**는 사람들이 <code>React</code>와 많이 사용해서 유명해졌다고한다.
하지만..!
**Redux**와 <code>React</code> 별개다.
**Redux**는 <code>React</code>에 의존하는 라이브러리가 아니다.

## 2. Redux의 필요성

**Redux**는 **전역**으로 **상태를 관리**하기에 **효과적**이다.

### 2-1 Redux가 필요한 상황

⚽. 시간에 따라 바뀌는 충분한 양의 데이터가 있다.

⚾. 상태를 위한 단 하나의 원천이 필요하다.

🥎. 모든 상태를 가지고 있기에 최상위 상태는 더 이상 적당하지 않다.

### 2-2 Redux의 장점

- 😀**1. 읽기 전용 상태**

  - **Redux**는 상태를 읽기 전용으로 취급한다.

  - 기존의 상태는 건들이지 않고 새로운 상태를 생성하여 이전 상태로 돌아가기 위해서는 현재 상태에 덮어쓰기만 하면 된다.
    **Rudux**는 <code>Rudex Undo</code>라는 라이브러리를 통해
    실행 취소 기능을 제공한다고 한다.

- 😁**2. 중앙화**
  - **Redux**는 <code>Store</code>라는 (전역)자바스크립트 변수를 통해
    상태를 한 곳에서 관리하는데 이것을 **'중앙화'**라고 하며
    다음과 같은 이점이 있다.


      더 이상 웹 사이트의 상태를 어디에 둘지 고민하지 않아도 된다.

      웹사이트에 다시 방문했을 때를 대비해 쉽게 상태를 저장 혹은
      불러올 수 있다.

### 2-3 Redux의 주의점

**[출처]** https://www.bangseongbeom.com/redux-benefits-caveats.html

**Redux**는 일반적인 라이브러리나 프레임워크가 아니다.
**Redux**만의 설계 철학과 함께 철학을 쉽게 따를 수 있도록
여러 도구를 지원해주는 개발도구다.
**Redux**를 사용함으로 인해 여러가지 강력한 장점을 얻을 수 있다.
하지만
**Redux**의 철학이 강제하는 방식으로 인해 오히려 코드가
복잡해지거나 코드를 작성하기 어려워질 수도 있다.
**Redux** 탄생 배경을 이해하고 **Redux**가 제공하는 여러 장점이 필요한 상황이 아니라면 다른 라이브러리나 프레임워크를 사용하는 것이 더 나을수도 있다.

**[관련 참고자료]** https://repo.yona.io/doortts/blog/post/297

## 3. Redux의 핵심 키워드

> #### 😊 액션(Action) : 무엇이 일어났는지 설명하는 객체

**Action** 객체는 <code>type field</code>를 필수적으로 가지고 있어야하고
그 외의 값들은 마음대로 넣어줄 수 있다.
**example** :

```
{
  type: "ADD_TODO",
  data: {
    id: 0,
    text: "리덕스 배우기"
  }
}
```

> #### 😊 리듀서(Reducer) : 이전에 값이 <code>action</code>의 설명을 통해 nextState로 바뀌었음을 return으로 알려준다.

**즉,** **Reducer**는 현재의 상태와, 전달 받은 액션을 참고하여
새로운 상태를 만들어서 반환한다.

> #### 😊 스토어 (Store) : 애플리케이션의 모든 state을 감싸주는 역할을 한다.

**Reducer**에서는 한 <code>Application</code>당 하나의 <code>Store</code>를 만들게 된다.
<code>Store</code>안에는, 현재의 앱 상태와, Reducer가 들어가있으며
추가적으로 몇가지 내장 함수들이 있다.

> #### 😊 디스패치 (dispatch) : 스토어의 내장함수 중 하나, 액션을 발생 시키는 것

디스패치가 호출되고 스토어는 <code>Reducer</code>함수를 실행시킨다.
파라미터로 전달해준 해당 <code>Action</code>을 처리하는 로직이 있다면
<code>Action</code>을 참고하여 새로운 상태를 만들어줌.

> #### 😊 구독 (subscribe) : 스토어의 내장함수 중 하나, 함수 형태의 값을 파라미터로 받아온다.

<code>Store</code>의 내장함수 중 하나로써 함수 형태의 값을 파라미터로 받아온다.
<code>subscribe</code>함수에 특정 함수를 전달하면,
<code>Action</code>이 <code>Dispatch</code>될 때마다 전달해준 함수가 호출된다.
