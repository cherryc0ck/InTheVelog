### ๐ฒ ์์ํ๊ธฐ์ ์์

๋ธ๋ง๋๊ฐ์์ ์ด๋ณด์๋ฅผ ์ํ ๋ฆฌ๋์ค 101์ ๋ณต์ตํ๋ฉฐ ์ ๋ฆฌํ๋ ค๊ณ  ํฌ์คํํ๋ค.
react์ redux๋ฅผ ์ฌ์ฉํ๊ธฐ ์  ๋ฐ๋๋ผ๋ก ์กฐ๊ธ ๋ ์ฝ๊ฒ ๊ฐ๋์ ์ก์๋ณด๋ ค๊ณ ํ๋ค. ์๋ต๋ ๊ฐ๋์ด ์์ ์ ์์ผ๋ฏ๋ก ์ดํด๊ฐ ๊ฐ์ง์๋๋ค๋ฉด
[Vanilla Redux-(1) Counter๋ฅผ ์ฐธ๊ณ ํ๊ธธ๋ฐ๋๋ค.](https://velog.io/@cherrycock/Vanilla-Redux-1-COUNTER)

## 1. Vanilla ToDo

### ๐ index.html

> ![](<https://images.velog.io/images/cherrycock/post/d8f06e8f-1ccd-44bd-bd21-9970b7f8a88c/(index.html).JPG>)์ฌํํ๋ค. <code>h1</code>, <code>input</code>, <code>button</code> ๊ทธ๋ฆฌ๊ณ  <code>ul</code>๋ก ๊ตฌ์ฑ๋์ด์๋ค.

### ๐ index.js

> ![](<https://images.velog.io/images/cherrycock/post/d6501e1f-95e2-4c71-800a-d2d6bc0c8eff/(index.js1).JPG>)<code>form</code>์ด <code>submit</code>๋๋ฉด <code>onSubmit</code>ํจ์๊ฐ ์คํ์ด๋๊ณ  <code>input</code>์์
> ๊ฐ์ ๊ฐ์ ธ์จ๋ค์ <code>createToDo</code>ํจ์๋ฅผ ํธ์ถํ๊ณ 
> <code>input</code>์์ ์ป์ ํ์คํธ๋ฅผ ์ธ์๋ก ๋ณด๋ธ๋ค.
> ๊ทธ๋ฌ๋ฉด <code>list item</code>์ ๋ง๋ค์ด์ฃผ๊ณ  <code>list</code>์ <code>innerText</code>๋ฅผ
> ์ธ์๋ก๋ฐ์ <code>toDo</code>๋ก ๋ฐ๊ฟ์ค๋ค์ <code>list</code>์ <code>append</code>์ํค๋ ๊ตฌ์กฐ์ด๋ค.

**ํ์ง๋ง ์ง๊ธ ์ฝ๋๋**
**์ดํ๋ฆฌ์ผ์ด์์ด ๋ฐ์ดํฐ๋ฅผ ๊ฐ์ง๊ณ  ์์ง ์๊ณ  HTML์ ์์ ํด์ฃผ๋ ๊ฒ ๋ฟ์ด๋ค.**
**์ด์  ์น์์ ๋ฐฐ์ด ๊ฒ์ ์ฐ์ต์ผ์ Redux๋ฅผ ์ด์ฉํด๋ณด์.**

### ๐ index.js

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

๋จผ์  **redux**๋ฅผ <code>import</code>ํด์ฃผ๊ณ 
<code>import {createStore} from "redux";</code>

์ด์ ์ ๋ฐฐ์ด **reducer**์ **store**ํจ์๋ฅผ ๋ง๋ค์ด์คฌ๋ค.
<code>const reducer = (state = [], action = []) => {}</code>
<code>const store = createStore(reducer);</code>

๊ทธ๋ฆฌ๊ณ  ๊ฐ๊ฐ์ **action**๋ค์ ๋ง๋ค๊ณ 
<code>const ADD_TODO = "ADD_TODO";
const DELETE_TODO = "DELETE_TODO";</code>

**reducer**ํจ์์ <code>swtich๋ฌธ</code>์ ์ด์ฉํ์ฌ (๋ญ๊ฐ๋๋  ์ฐ์ )<code>return</code>ํ๊ฒ ๋ง๋ค์๋ค.

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

๋ง์ง๋ง์ผ๋ก ์ฌ์ฉ์๊ฐ <code>submit</code>ํ ๋ ๋ฆฌ์คํธ๋ฅผ ๋ง๋ค๊ณ  ๋ฆฌ์คํธ ์์ดํ๋ค์
๋ฆฌ์คํธ์ ๋ฃ์ด์ฃผ๋ createToDo๋ฅผ ํธ์ถํ๋๋์  <code>dispatch</code> ์์ผ์คฌ๋ค.
ํ ์ผ์ด์ค์์๋ **action**๋ง๊ณ ๋ <code>text</code>๊ฐ ํ์ํ๋ค.
<code> store.dispatch({ type: ADD_TODO, text: toDo });</code>

**์ด๊ฒ์ ์ฝ์๋ก ํ์ธํด๋ณด์.**

### ๐console

> ![](<https://images.velog.io/images/cherrycock/post/25c892f8-f32a-4535-8ae5-21eb3fe02f92/(console.log1).JPG>)input์ text๋ฅผ ์๋ ฅํ๊ณ  add๋ฒํผ์ ๋๋ ธ์๋ ์ฝ์๋ก๊ทธ๊ฐ ์คํ๋๋ฉฐ
> **dispatch**๋ก ์ธํด<code>store.dispatch({ type: ADD_TODO, text: toDo });</code>
> **action**์ <code>type</code>๊ณผ <code>text</code>๊ฐ ๋ง๊ฒ ๋์ค๋๊ฑธ ํ์ธํ  ์ ์๋ค.

**์ฌ๊ธฐ์ ๊ผญ ์ดํดํ๊ณ  ๋์ด๊ฐ์ผํ๋๊ฒ ์๋ค **

## 1.1 State Mutation

### [๐Redux ๊ณต์๋ฌธ์ ไธญ ](https://redux.js.org/understanding/thinking-in-redux/three-principles)

Redux ๊ณต์๋ฌธ์ Three Principles(์ธ๊ฐ์ง ์์น) ์นดํ๊ณ ๋ฆฌ๋ฅผ๋ณด๋ฉด
**Changes are made with pure functions**๋ผ๋ ์์ ๋ชฉ์ด ์๋ค.
๋ด์ฉ์ ์ดํด๋ณด๋ฉด
**Remember to return new state objects,
instead of mutating the previous state.**<code>
์ด์  ์ํ๋ฅผ ๋ณ๊ฒฝํ๋ ๋์  ์ ์ํ ๊ฐ์ฒด๋ฅผ ๋ฐํํด์ผ ํฉ๋๋ค.</code>

์ฆ, **state๋ฅผ mutateํ๋๊ฒ ์๋๋ผ ์๋ก์ด objects๋ฅผ ๋ฆฌํดํด์ผํ๋ค.**
์ํ๋ฅผ ์์ ํ๋ ๊ฒ์ด ์๋๋ผ **์๋ก์ด ๊ฒ์ ๋ฆฌํดํด์ผ๋๋ค๋ ์๋ฏธ์ด๋ค.**

### ๐index.js

> ![](<https://images.velog.io/images/cherrycock/post/123fe792-716b-41d2-b138-0bd6a8cd98b3/(index.js2).JPG>)์์ ๋งํ ๊ฒ์ฒ๋ผ state.push()๊ฐ์ด state๋ฅผ ๋ณํํ๋๊ฒ์ ํ์ง์์๊ฒ์ด๋ค.
> ~~<code>return state.push(action.text)</code>~~
> <br>
> Es6 spread ๋ฌธ๋ฒ์ ์ด์ฉํด ๊ธฐ์กด์ state๋ฅผ ๋๊ฐ์ด ๊ฐ์ ธ์
> ์๋ก์ด array๋ก returnํ  ์ ์๋ค.
> <code>return [...state, { text: action.text }];</code>

**์ฝ์๋ก ํ์ธํด๋ณด์**

### ๐console

> ![](https://images.velog.io/images/cherrycock/post/f100f590-14d8-4f33-a814-609e178adec3/console.log2.JPG)subscribe์ ์ด์ฉํด ๋ณํ๊ฐ ์๊ธธ๋ ์ฝ์๋ก๊ทธ๋ฅผ ์คํํ๊ฒ๋๋ค.
> ์ฌ์ง์์์๊ฐ์ด text๋ฅผ ์๋ ฅํ ๋๋ง๋ค ๊ธฐ์กด์ state๊ฐ์ ๊ฐ์ ธ์ ์๋ ฅํtext๋ฅผ ํฌํจํ **์๋ก์ด array**๋ฅผ ์ถ๋ ฅํ๋๊ฒ์ ํ์ธํ  ์ ์๋ค.
> <code>store.subscribe(() => console.log(store.getState())); </code>

### ๐index.js

> ์ด์  deleteํ๋ ๊ธฐ๋ฅ์ ์ถ๊ฐํ ๊ฑด๋ฐ ํ์ฌ๋ text๊ฐ๋ฐ์ ์์ด ์๋ก์ด array๋ฅผ ์์ฑํ ๋ Date.now()๋ฅผ ์ด์ฉํด ๊ณ ์ ๊ฐ์ ์ถ๊ฐํด์ค๊ฒ์ด๋ค.
> <code>case ADD_TODO:

      return [...state, { text: action.text, id: Date.now() }];</code>

## 1.2 Delete To Do

์ญ์  ๊ธฐ๋ฅ์ ๋ง๋ค๊ธฐ์  <code>onSubmit</code>ํจ์์์ **dispatch**๋ฅผ ํ๋๊ฒ์ด ์๋
๊ฐ๊ฐ์ <code>addToDo</code>, <code>deleteToDo</code>ํจ์๋ฅผ ๋ง๋ค๊ฒ ๋ค.

๋จผ์  <code>addToDo</code>ํจ์๋ text<code>(input์ value)</code>๋ฅผ ํ๋ผ๋ฏธํฐ๋ก ๋ฐ๊ณ 
**store.dispatch**๋ฅผ ํธ์ถํด์ค๋ค.

```
const addToDo = text => {
  store.dispatch({ type: ADD_TODO, text });
}
```

๊ทธ๋ฆฌ๊ณ  todo๋ค์ paintํด์ค์ผํ๋๋ฐ <code>paintToDos</code>ํจ์๋ฅผ ๋ง๋ค๊ณ 
์ด ํจ์๋ฅผ **subcribe**ํด์ค๋ค.
<code>paintToDos</code>ํจ์๊ฐ ์คํ๋๋ฉด <code>getState</code>๋ฅผ ๊ฐ์ ธ์ <code>toDos</code>๋ณ์์ ๋ด๊ณ 
๋ฆฌ์คํธ๋ฅผ ์์ฑํด text๊ฐ๊ณผ id๊ฐ์ ์ง์ ํด์ฃผ๊ณ  <code>append</code>์์ผ์ค๋ค.

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

์ถ๊ฐ์ ์ผ๋ก **reducer**์์ <code>ADD_TODO</code>์ผ๋ ๋ฆฌํดํ๋ ์์๋ฅผ ์์ ํด์ฃผ๊ฒ ๋ค. ์ด๋ ๊ฒ ์์ ํด์ค๋ค๋ฉด <code>todo</code>๊ฐ ์๋กญ๊ฒ ์ถ๊ฐ๋ ๋๋ง๋ค <code>array</code>์ ์ฒซ๋ถ๋ถ์ ์๊ฒ๋๋ค.
<code>return [{ text: action.text, id: Date.now() }, ...state];</code>

์ด์  ์ญ์ ๊ธฐ๋ฅ์ ๋ง๋ค๊ฑด๋ฐ list item์ด ์์ฑ๋ ๋๋ง๋ค ์ญ์ ๋ฒํผ ๋ํ ํ์ํ๋ค. ๋ฒํผ์ ์์ฑํ๊ณ  ํด๋ฆญ์ด๋ฒคํธ๋ฅผ ๋ฑ๋กํ์๋ค. <code>deleteToDo</code>ํจ์๊ฐ ์คํ๋๊ฒ๋

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

์ด์  <code>deleteToDo</code> ํจ์๋ฅผ ๋ง๋ค์ด๋ณด์.
์ ์๊ฐํด๋ณด์.
์ฐ๋ฆฌ๋ <code>list item</code>์ ๊ณ ์ ์ <code>id</code>๊ฐ์ ๋ฃ์ด์ฃผ์๋ค. ํ์ฌ ๋ฒํผ์๋ <code>eventListener</code>๊ฐ ๋ฑ๋ก๋์ด์๊ณ 
<code>event</code>๊ฐ์ฒด์ <code>target.parentNode</code>๋ฅผ ์ด์ฉํ๋ฉด
๊ณ ์ ์ <code>id</code>๋ฅผ ๊ฐ์ง ํด๋น <code>list item</code>์ ์ ๊ทผํ  ์ ์๋ค.

```
const deleteToDo = e => {
  const id = e.target.parentNode.id;
  store.dispatch({ type: DELETE_TODO, id });
}
```

์ด๋ ๊ฒ <code>addToDo</code>, <code>deleteToDo</code> ํจ์ ์์ฑํ์๊ณ  ์ถ๊ฐ์ ์ผ๋ก
**action**์ <code>return</code>ํ๋ ํจ์๋ฅผ ์์ฑํ ๊ฒ์ด๋ค.
<code>๋๋ถ๋ถ์ ์ฌ๋๋ค์ด ์ฃผ๋ก reducer ์์ ์ถ๊ฐํ๋ค๊ณ ํ๋ค.</code>

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

**๊ทธ๋ฆฌ๊ณ  ๊ธฐ์กด์ ํจ์๋ฅผ ์์ ํด์ฃผ๊ฒ ๋ค.**

```
const dispatchAddToDo = text => {
  store.dispatch(addToDo(text));
}


const dispatchDeleteToDo = e => {
  const id = e.target.parentNode.id;
  store.dispatch(deleteToDo(id));
}
```

์ ์กฐ๊ธ ์ ๋ฆฌ๋ฅผ ํ์๋ฉด <code>addToDo</code>, <code>deleteToDo</code>ํจ์๋ ์ค๋ก์ง **action**์ return
<code>dispatchAddToDo</code>, <code>dispatchDeleteToDo</code>ํจ์๋ <code>addToDo</code>, <code>deleteDo</code>ํจ์์
returnํ๋ object๋ฅผ **dispatch**ํด์ค๋ค.

## 1.3 Delete To Do part Two

์ด์  ์ ๋ง ์ญ์ ๊ธฐ๋ฅ์ ๋ง๋ค์ด๋ณผ ์ฐจ๋ก์ด๋ค.

์กฐ๊ฑด์
๋ด๊ฐ ์ญ์ ํ ,์ ํํ <code>todo</code>๋ฅผ ์ญ์ ํ๋
๋ด๊ฐ ์ญ์ ํ  <code>todo</code>์ <code>id</code>์ ํด๋นํ์ง ์๋ <code>todo</code>๋ค์ ์ ์ง์ํค๋ฉด๋๋ค.
<code>Array.filter</code>๋ฅผ ์ฌ์ฉํด ์กฐ๊ฑด์ ์์ฑํ๊ณ  ๊ทธ ์กฐ๊ฑด์ด ์ถฉ์กฑ๋๋ฉด ํด๋น ์์๋ ์๋ก์ด <code>array</code>์ ๋จ๊ฒํ๋ฉด๋๋ค.
์ ~~๋ <code>Array.prototype.splice()</code>๊ฐ์ด ๊ธฐ์กด์ ๋ฐฐ์ด์ ์์ ํ๋๊ฒ์ด์๋
์๋ก์ด <code>array</code>๊ฐ์ <code>return</code>ํด์ผํ๋ค.

```
case DELETE_TODO:
  return state.filter(toDo => toDo.id !== action.id );
```

์ ์ด์  ์์ฑ์ด๋ค! ์๋๋ ์์ฑํ <code>index.js</code>์ด๋ค.

### ๐index.js

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
