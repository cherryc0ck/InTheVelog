### 😲 시작하기에 앞서

노마드강의의 초보자를 위한 리덕스 101을 복습하며 정리하려고 포스팅한다.
react에 redux를 사용하기 전 바닐라로 조금 더 쉽게 개념을 잡아보려고한다. 생략된 개념이 있을 수 있으므로 이해가 가지않는다면
[Vanilla Redux-(1) Counter를 참고하길바란다.](https://velog.io/@cherrycock/Vanilla-Redux-1-COUNTER)

## 1. Vanilla ToDo

### 😁 index.html

> ![](<https://images.velog.io/images/cherrycock/post/d8f06e8f-1ccd-44bd-bd21-9970b7f8a88c/(index.html).JPG>)심플하다. <code>h1</code>, <code>input</code>, <code>button</code> 그리고 <code>ul</code>로 구성되어있다.

### 😁 index.js

> ![](<https://images.velog.io/images/cherrycock/post/d6501e1f-95e2-4c71-800a-d2d6bc0c8eff/(index.js1).JPG>)<code>form</code>이 <code>submit</code>되면 <code>onSubmit</code>함수가 실행이되고 <code>input</code>에서
> 값을 가져온다음 <code>createToDo</code>함수를 호출하고
> <code>input</code>에서 얻은 텍스트를 인자로 보낸다.
> 그러면 <code>list item</code>을 만들어주고 <code>list</code>의 <code>innerText</code>를
> 인자로받은 <code>toDo</code>로 바꿔준다음 <code>list</code>에 <code>append</code>시키는 구조이다.

**하지만 지금 코드는**
**어플리케이션이 데이터를 가지고 있지 않고 HTML을 수정해주는 것 뿐이다.**
**이전 섹션에 배운 것을 연습삼아 Redux를 이용해보자.**

### 😁 index.js

```
import {createStore} from "redux";

const form = document.querySelector("form");
const input = document.querySelector("input");
const ul = document.querySelector("ul");

const ADD_TODO = "ADD_TODO";
const DELETE_TODO = "DELETE_TODO";

const reducer = (state = [],  action) => {
  console.log(action);
  switch(action.type){
    case ADD_TODO:
      return [];
    case DELETE_TODO:
      return [];
    default:
      return state;
  }
};
const store = createStore(reducer);

const onSubmit = e => {
  e.preventDefault();
  const toDo = input.value;
  input.value = "";
  store.dispatch({ type: ADD_TODO, text: toDo });
};

form.addEventListener("submit", onSubmit);
```

먼저 **redux**를 <code>import</code>해주고
<code>import {createStore} from "redux";</code>

이전에 배운 **reducer**와 **store**함수를 만들어줬다.
<code>const reducer = (state = [], action = []) => {}</code>
<code>const store = createStore(reducer);</code>

그리고 각각의 **action**들을 만들고
<code>const ADD_TODO = "ADD_TODO";
const DELETE_TODO = "DELETE_TODO";</code>

**reducer**함수에 <code>swtich문</code>을 이용하여 (뭐가됐든 우선)<code>return</code>하게 만들었다.

```
const reducer = (state = [],  action) => {
console.log(action);
    switch(action.type){
    case ADD_TODO:
      return [];
    case DELETE_TODO:
      return [];
    default:
      return state;
  }
};
```

마지막으로 사용자가 <code>submit</code>할때 리스트를 만들고 리스트 아이템들을
리스트에 넣어주는 createToDo를 호출하는대신 <code>dispatch</code> 시켜줬다.
현 케이스에서는 **action**말고도 <code>text</code>가 필요하다.
<code> store.dispatch({ type: ADD_TODO, text: toDo });</code>

**이것을 콘솔로 확인해보자.**

### 📕console

> ![](<https://images.velog.io/images/cherrycock/post/25c892f8-f32a-4535-8ae5-21eb3fe02f92/(console.log1).JPG>)input에 text를 입력하고 add버튼을 눌렸을때 콘솔로그가 실행되며
> **dispatch**로 인해<code>store.dispatch({ type: ADD_TODO, text: toDo });</code>
> **action**의 <code>type</code>과 <code>text</code>가 맞게 나오는걸 확인할 수 있다.

**여기서 꼭 이해하고 넘어가야하는게 있다 **

## 1.1 State Mutation

### [📕Redux 공식문서 中 ](https://redux.js.org/understanding/thinking-in-redux/three-principles)

Redux 공식문서 Three Principles(세가지 원칙) 카테고리를보면
**Changes are made with pure functions**라는 소제목이 있다.
내용을 살펴보면
**Remember to return new state objects,
instead of mutating the previous state.**<code>
이전 상태를 변경하는 대신 새 상태 개체를 반환해야 합니다.</code>

즉, **state를 mutate하는게 아니라 새로운 objects를 리턴해야한다.**
상태를 수정하는 것이 아니라 **새로운 것을 리턴해야된다는 의미이다.**

### 😄index.js

> ![](<https://images.velog.io/images/cherrycock/post/123fe792-716b-41d2-b138-0bd6a8cd98b3/(index.js2).JPG>)앞서 말한 것처럼 state.push()같이 state를 변형하는것은 하지않을것이다.
> ~~<code>return state.push(action.text)</code>~~
> <br>
> Es6 spread 문법을 이용해 기존의 state를 똑같이 가져와
> 새로운 array로 return할 수 있다.
> <code>return [...state, { text: action.text }];</code>

**콘솔로 확인해보자**

### 📕console

> ![](https://images.velog.io/images/cherrycock/post/f100f590-14d8-4f33-a814-609e178adec3/console.log2.JPG)subscribe을 이용해 변화가 생길때 콘솔로그를 실행하게된다.
> 사진에서와같이 text를 입력할때마다 기존의 state값을 가져와 입력한text를 포함한 **새로운 array**를 출력하는것을 확인할 수 있다.
> <code>store.subscribe(() => console.log(store.getState())); </code>

### 😁index.js

> 이제 delete하는 기능을 추가할건데 현재는 text값밖에 없어 새로운 array를 생성할때 Date.now()를 이용해 고유값을 추가해줄것이다.
> <code>case ADD_TODO:

      return [...state, { text: action.text, id: Date.now() }];</code>
