### 😲 시작하기에 앞서

노마드강의의 초보자를 위한 리덕스 101을 복습하며 정리하려고 포스팅한다.
바닐라JS로 React를 적용해봤고 이제 드디어 React에 적용해보겠다.

이전 바닐라JS 포스팅이 궁금하다면
[Vanilla Redux-(1) Counter](https://velog.io/@cherrycock/Vanilla-Redux-1-COUNTER)
[Vanilla Redux-(2) ToDoList]
(https://velog.io/@cherrycock/Vanilla-Redux-2-To-Do-List)

## 1. Setup

### 😀 Add redux, rounter-dom

> ![](<https://images.velog.io/images/cherrycock/post/363e01b1-9880-40d7-9d30-718b166dcc95/(pakage.json).JPG>)**yarn add react-redux react-router-dom**

### 😀 src

> ![](https://images.velog.io/images/cherrycock/post/2692b11e-9a36-4320-aa58-d7d2c03ccefa/root.JPG)

### 😁 index.html

> ![](<https://images.velog.io/images/cherrycock/post/9328c333-dc44-4c77-9b26-626507fb6a0c/(index.hml1).JPG>)

### 😀 Index.js

> ![](<https://images.velog.io/images/cherrycock/post/d8f88e9d-6a5c-4e9a-aa6d-668fbe7673ca/(index.js1).JPG>)

### 😎 App.js

> ![](<https://images.velog.io/images/cherrycock/post/ce69875c-8b44-479c-81da-1dc4f64b3e08/(app.js1).JPG>)

### 😎 Home.js

> ![](<https://images.velog.io/images/cherrycock/post/ed977b4e-9448-4414-a1c4-2f17900dc9bc/(home.js).JPG>)

### 😎 Detail.js

> ![](<https://images.velog.io/images/cherrycock/post/d87b50c5-6c91-4213-a199-3327230a48f4/(detail.js).JPG>)

기본적인 셋업이다.
<code>Redux</code>, <code>Router</code>를 추가해줬고 <code>App</code>에서
default component는 **Home**
/detail은 **Detail**로 path값을 설정해주었다.

**Home**이 리턴하는 것은
<code>form</code>태그에 **text**를 입력하는 <code>input</code>과 추가버튼인 <code>button</code> 그리고 <code>ul</code>이다.
<code>useState</code>를 이용하여 **text**를 선언해주었고
<code>input</code> 요소 값이 변경될때마다 호출되는 <code>onChange</code>함수와
<code>submit</code> 될 때 호출되는 <code>onSubmit</code>함수를 생성하였다.
<code>input</code> 요소 값이 변경될때 <code>onChange</code>함수가 호출되고 <code>setText</code>를 이용해
해당 <code>event</code>객체의 <code>target.value</code>로 **state**값을 업데이트시켜준다.
그럼 <code>input value</code>는 새로업데이트된 **state**값이 되어 렌더링된다.

**자 그럼 Store를 만들고 연동해보자!**

## 1.1 Connecting the Store

### 😎 Store.js

```
import {createStore} from "redux";

const ADD = "ADD";
const DELETE = "DELETE";

export const addToDo = text => {
  return {
    type:ADD,
    text
  };
};

export const deleteToDo = id => {
  return {
    type:DELETE,
    id
  };
};

const reducer = (state = [], action) => {
  switch(action.type) {
    case ADD:
      return  [{ text: action.text, id:Date.now() }, ...state];
    case DELETE:
      return state.filter(toDo => toDo !== action.id);
    default:
      return state;
  }
}

const store = createStore(reducer);

export default store;

```

**store** 구조는 앞서 포스팅한 것과 동일하다.
이것을 연동할건데,

### 😎 Index.js

> ![](<https://images.velog.io/images/cherrycock/post/724b4282-a1d9-4f70-b463-ade88385ec7d/(index.js2).JPG>)
> <code>Provider</code> 컴포넌트를 사용하여 **App**에 **store**를 연동하였다.
> <code>Provider</code>는 <code>react-redux</code> 라이브러리에 내장되어있는,
> 리액트 앱에 **store**를 손쉽게 연동 할 수 있도록 도와주는 컴포넌트이다.
> 이 컴포넌트를 불러오고 연동 할 컴포넌트를 감싸준다음에
> <code>Provider</code> 컴포넌트의 <code>props</code>로 **store** 값을 설정해주면된다.

## 1.2 mapStateToProps

<code>redux-state</code>로부터 정보를 가지고 올 수 있어야한다.
알다시피 현재 **state**는 비어있다.

현재 브라우저에 <code>toDo</code>들을 렌더링해주는 **Home**이다.
**store**로부터 **state**를 가져올 수 있도록해야한다.
즉, **connect** 연동해줘야한다.

> ![](<https://images.velog.io/images/cherrycock/post/b2db5569-96b9-4f26-9129-c85a4c84b952/(redux-org1).JPG>)<code>redux</code>문서에서 보면 이것을 **mapStateToProps**라고 부르고있다.기본적으로
> **mapStateToProps**는 함수인데 두종류의 <code>argument</code>와 함께 호출된다.
> <code>state</code>는 **redux store로부터온 state**
> <code>ownProps</code>는 **component의 props**

자 그럼 <code>getCurrentState</code>함수를 이용해서 **store**로부터 **state**를 가지고오자.

### 😀Home.js

```
function getCurrentState(state, ownProps) {
  console.log(state, ownProps);

};
export default connect(getCurrentState)(Home);
```

이렇게 <code>getCurrentState</code>함수를 실행시키고 콘솔을 확인해보면 다음과 같다.

### ❗ Console

> ![](<https://images.velog.io/images/cherrycock/post/05f86449-f5a0-4b2c-bd08-42b532a8d689/(console.log1).JPG>)에러를 보면 **connect**의 <code>mapStateToProps</code>에 에러가 생겼다고하고
> 이것은 <code>object</code>를 리턴해야된다는 말이다.
> 맞는 말이다 현재 우린 아무것도 <code>return</code>해주지않고있다.
> 하지만 중요한 부분은 콘솔로그에 찍힌
> <code>Redux store</code>로 부터 **state**를 받아오고있음을 알 수 있다.
> 확인하기 위해 **default state**를 설정해보자.

```
const reducer = (state = ["Hello?"], action) => {
  switch(action.type) {
    case ADD:
      return  [{ text: action.text, id:Date.now() }, ...state];
    case DELETE:
      return state.filter(toDo => toDo !== action.id);
    default:
      return state;
  }
}
```

![](<https://images.velog.io/images/cherrycock/post/59840282-4e11-4f03-a2f6-90fbac1b7a27/(console.log2).JPG>)콘솔을 확인해보면
**첫번째 argument는 현재 redux store에서 온 state이다.**
<code>Hello?</code>
**두번째 argument는 component의 props이다.**
<code>리액트라우터에 의해 주어진 history, location, match...</code>

<code>mapStateToProps</code>를 사용한다는 건 **store**로 부터 무엇인가를 가져오고싶다는것이다. 그리고나서 컴포넌트의 <code>props</code>에 넣는다.

즉 현재 케이스에서의 **connect**함수인 <code>getCurrentState</code>함수는
**Home**으로 보내는 <code>props</code>에 추가될 수 있도록 허용해주는것이다.

```
function getCurrentState(state, ownProps) {
  return { toDos: state };
};

export default connect(getCurrentState)(Home);
```

이제 함수이름을 기본적으로 <code>mapStateToProps</code>로 바꿔준 다음  
리턴문을 작성하고 콘솔을 확인해보면

> ![](<https://images.velog.io/images/cherrycock/post/057a7221-c971-45c7-a281-b4c22c155929/(console.log3).JPG>)**props에 state가 추가되어있다.**

정리하자면, 함수와 컴포넌트를 이용해서 **connect**를 사용하기만 하면된다.

## 1.3 mapDispatchToProps

이번엔 **connect**의 두번째 인자인 **mapDispatchToProps**를 적용해보겠다.

먼저 **mapDispatchToProps**함수를 생성하고
<code>인자로는 dispatch와 ownProps가 있지만 지금은 dispatch만 사용하겠다.</code>

```
function mapDispatchToProps(dispatch){
}
```

**connect**에 두번째 인자로 입력해준다.

```
export default connect(mapStateToProps, mapDispatchToProps)(Home);
```

이제 <code>prop</code>을 만들어주자.
먼저 <code>store.js</code>에서 <code>addToDo</code>, <code>DeleteToDo</code>를 <code>unexport</code>해주고
<code>actionCreators</code>함수를 만든 다음 이것을 <code>export</code>해주겠다.

```
const addToDo = text => {
  return {
    type:ADD,
    text
  };
};

deleteToDo = id => {
  return {
    type:DELETE,
    id
  };
};

export const actionCreators = {
  addToDo,
  deleteToDo
}
```

다시 **Home**으로 와서 **mapDispatchToProps**함수를 작성해보겠다.
**store**의 **addToDo**를 <code>retrun</code>하게끔말이다.

```
function mapDispatchToProps(dispatch){
  return {
    addToDo: text => dispatch(actionCreators.addToDo(text))
  };
}
```

이렇게 **addToDo**라는 함수를 만들었다.
**addToDo**는 <code>text argument</code>를 필요로하고
**addToDo** 가 하는일은 **dispatch**를 호출한다 그리고
**dispatch**는 <code>actionCreators</code>를 호출할것이고
**addToDo**는 <code>text</code>를 받아야한다.
조금 정리하자면..
이 함수는 <code>text</code>를 인자로 받고 이 함수가 실행되면
**dispatch**를 호출한다 <code>actionCreators.addToDo(text)</code>와 함께

그럼 이제 성공적으로 리액트 컴포넌트로부터
**reducer**에게 **dispatch**를 하는것이다.
<br/>

**그럼 이제 ToDo컴포넌트를 생성해 렌더링을 해보고 삭제기능을 만들어보자.**

## 1.4 Deleting To Do

### 😎 ToDo.js

> ![](<https://images.velog.io/images/cherrycock/post/d0a37834-719a-4cd8-bfcc-f548094298c0/(todo.js1).JPG>)<code>props</code>로 <code>text</code>를 받아오는 **ToDo컴포넌트**이다.

### 😀 Home.js

```
return (
    <>
      <h1>To Do</h1>
      <form onSubmit={onSubmit}>
        <input type="text" value={text} onChange={onChange} />
        <button>Add</button>
      </form>
      <ul>
        {toDos.map(toDo =>
          <ToDo key={toDo.id} {...toDo} />
        )}
      </ul>
    </>
  )
```

**mapStateToProps**함수로부터 받아온 <code>prop</code>인 **toDos**와 <code>Array.prototype.map()</code>메서드를 이용하여
**ToDo component**를 렌더링한다.
**ToDo component**는 <code>text</code>를 받아오고 {text}는 li태그에 있다.
이제 <code>submit</code>될때마다 리스트들이 추가가 될것이다.

이제 본격적으로 삭제기능을 만들어보자.
누군가가 del버튼을 눌렀을때 그 해당 **ToDo**를 지워야한다.
**ToDo**를 지우기위해 뭐가 필요할까?
id가 필요하다.
**store.dispatch()**를 호출해야되는데
<code>store.dispatch({ type:del, id })</code> (이런식으로)
현재 어떤 방법으로 dispatch동작에 접근을 해야할까?
이전챕터에서 적용시켰던 **mapDispatchToProps**를 이용해보자.
**ToDo**는 오로지 **dispatch**만 신경쓰면된다.
**ToDo**는 **reducer**에게 메세지를 보내야한다.
즉, **ToDo**는 <code>state</code>에는 신경을쓰지않아도 된다.

그렇다면 **ToDo**에도 **connect**해보자.

### 😁 ToDo.js

> ![](<https://images.velog.io/images/cherrycock/post/a800bcea-be2b-4010-8e80-41d486b5e0eb/(todo.js2).JPG>)
> **ToDo**를 지우기위해서는 id가 필요하지만
> 현재 <code>onBtnClick</code>함수는 인자로 id를 받을 필요가 없다.
> 왜냐하면 **home**에서의 id를 <code>prop</code>으로 받았기때문에
> <code>ToDo key={toDo.id}</code>
> **mapDispatchToProps**함수의 두번째 인자인
> <code>ownProps</code>를 사용하여 id에 접근하면된다.

**이렇게 삭제까지 가능하게하였고 마지막으로 detail컴포넌트를 다뤄보자.**

## 1.5 Detail Screen

### 😎App.js

> ![](<https://images.velog.io/images/cherrycock/post/c5bbad3c-fd5a-4322-8361-b7142c8e7b73/(app.js3).JPG>)**detail의 path값을 "/detail"에서 "/:id"로 수정하였다.**

### 😁ToDo.js

> ![](<https://images.velog.io/images/cherrycock/post/5f1bed0a-54f5-4e1f-aa86-e9bb404ee0ea/(todo.js3).JPG>)**클릭하면 다른 주소로 이동하는 React-router의 <code>Link</code>컴포넌트를 사용해 id값을 넘겨주며 detail컴포넌트로 이동시킨다.**

### 😁Detail.js

> ![](<https://images.velog.io/images/cherrycock/post/a6d3c2c0-07d1-4490-81fa-4a5237843c9f/(detail.js2).JPG>)
> **connect를하고 mapStateToProps을 생성해 toDo를 리턴해준다.**
> **toDo의 text와 id가 있다면 그 값을 렌더링한다.**
