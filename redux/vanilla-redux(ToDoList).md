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

## 1.2 Delete To Do

삭제 기능을 만들기전 <code>onSubmit</code>함수에서 **dispatch**를 하는것이 아닌
각각의 <code>addToDo</code>, <code>deleteToDo</code>함수를 만들겠다.

먼저 <code>addToDo</code>함수는 text<code>(input의 value)</code>를 파라미터로 받고
**store.dispatch**를 호출해준다.

```
const addToDo = text => {
  store.dispatch({ type: ADD_TODO, text });
}
```

그리고 todo들을 paint해줘야하는데 <code>paintToDos</code>함수를 만들고
이 함수를 **subcribe**해준다.
<code>paintToDos</code>함수가 실행되면 <code>getState</code>를 가져와 <code>toDos</code>변수에 담고
리스트를 생성해 text값과 id값을 지정해주고 <code>append</code>시켜준다.

```
const paintToDos = () =>{
  const toDos = store.getState();
  ul.innerText ="";
  toDos.forEach(toDo => {
    const li = document.createElement('li');
    li.id = toDo.id;
    li.innerText = toDo.text;
    ul.appendChild(li);
  })
}
store.subscribe(paintToDos);
```

추가적으로 **reducer**에서 <code>ADD_TODO</code>일때 리턴하는 순서를 수정해주겠다. 이렇게 수정해준다면 <code>todo</code>가 새롭게 추가될때마다 <code>array</code>의 첫부분에 있게된다.
<code>return [{ text: action.text, id: Date.now() }, ...state];</code>

이제 삭제기능을 만들건데 list item이 생성될때마다 삭제버튼 또한 필요하다. 버튼을 생성하고 클릭이벤트를 등록하였다. <code>deleteToDo</code>함수가 실행되게끔

```
const paintToDos = () =>{
  const toDos = store.getState();
  ul.innerText ="";
  toDos.forEach(toDo => {
    const li = document.createElement('li');
    const btn = document.createElement('button');
    btn.innerText = "DEL";
    btn.addEventListener('click', deleteToDo);
    li.id = toDo.id;
    li.innerText = toDo.text;
    li.appendChild(btn);
    ul.appendChild(li);
  })
}
```

이제 <code>deleteToDo</code> 함수를 만들어보자.
자 생각해보자.
우리는 <code>list item</code>에 고유의 <code>id</code>값을 넣어주었다. 현재 버튼에는 <code>eventListener</code>가 등록되어있고
<code>event</code>객체의 <code>target.parentNode</code>를 이용하면
고유의 <code>id</code>를 가진 해당 <code>list item</code>에 접근할 수 있다.

```
const deleteToDo = e => {
  const id = e.target.parentNode.id;
  store.dispatch({ type: DELETE_TODO, id });
}
```

이렇게 <code>addToDo</code>, <code>deleteToDo</code> 함수 생성하였고 추가적으로
**action**을 <code>return</code>하는 함수를 생성할것이다.
<code>대부분의 사람들이 주로 reducer 위에 추가한다고한다.</code>

```
const addToDo = text => {
  return {
     type: ADD_TODO,
     text
  }
}

const deleteToDo = id => {
  return {
    type: DELETE_TODO,
    id
  }
}
```

**그리고 기존의 함수를 수정해주겠다.**

```
const dispatchAddToDo = text => {
  store.dispatch(addToDo(text));
}


const dispatchDeleteToDo = e => {
  const id = e.target.parentNode.id;
  store.dispatch(deleteToDo(id));
}
```

자 조금 정리를 하자면 <code>addToDo</code>, <code>deleteToDo</code>함수는 오로지 **action**을 return
<code>dispatchAddToDo</code>, <code>dispatchDeleteToDo</code>함수는 <code>addToDo</code>, <code>deleteDo</code>함수의
return하는 object를 **dispatch**해준다.

## 1.3 Delete To Do part Two

이제 정말 삭제기능을 만들어볼 차례이다.

조건은
내가 삭제할,선택한 <code>todo</code>를 삭제하되
내가 삭제할 <code>todo</code>의 <code>id</code>에 해당하지 않는 <code>todo</code>들을 유지시키면된다.
<code>Array.filter</code>를 사용해 조건을 작성하고 그 조건이 충족되면 해당 요소는 새로운 <code>array</code>에 남게하면된다.
절~~대 <code>Array.prototype.splice()</code>같이 기존의 배열을 수정하는것이아닌
새로운 <code>array</code>값을 <code>return</code>해야한다.

```
case DELETE_TODO:
  return state.filter(toDo => toDo.id !== action.id );
```

자 이제 완성이다! 아래는 완성한 <code>index.js</code>이다.

### 😁index.js

```
import {createStore} from "redux";

const form = document.querySelector("form");
const input = document.querySelector("input");
const ul = document.querySelector("ul");

const ADD_TODO = "ADD_TODO";
const DELETE_TODO = "DELETE_TODO";

const addToDo = text => {
  return {
     type: ADD_TODO,
     text
  }
}

const deleteToDo = id => {
  return {
    type: DELETE_TODO,
    id
  }
}


const reducer = (state = [],  action) => {
  switch(action.type){
    case ADD_TODO:
      //Never state mutation!!
      //return state.push(action.text);

      // Return something new
      return [{ text: action.text, id: Date.now() }, ...state];

    case DELETE_TODO:
      return [];
    default:
      return state;
  }
};

const store = createStore(reducer);

store.subscribe(() => console.log(store.getState()));


const dispatchAddToDo = text => {
  store.dispatch(addToDo(text));
}


const dispatchDeleteToDo = e => {
  const id = e.target.parentNode.id;
  store.dispatch(deleteToDo(id));
}


const paintToDos = () =>{
  const toDos = store.getState();
  ul.innerText ="";
  toDos.forEach(toDo => {
    const li = document.createElement('li');
    const btn = document.createElement('button');
    btn.innerText = "DEL";
    btn.addEventListener('click', deleteToDo);
    li.id = toDo.id;
    li.innerText = toDo.text;
    li.appendChild(btn);
    ul.appendChild(li);
  })
}

store.subscribe(paintToDos);

const onSubmit = e => {
  e.preventDefault();
  const toDo = input.value;
  input.value = "";
  dispatchAddToDo(toDo);
};

form.addEventListener("submit", onSubmit);
```
