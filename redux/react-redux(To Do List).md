### ๐ฒ ์์ํ๊ธฐ์ ์์

๋ธ๋ง๋๊ฐ์์ ์ด๋ณด์๋ฅผ ์ํ ๋ฆฌ๋์ค 101์ ๋ณต์ตํ๋ฉฐ ์ ๋ฆฌํ๋ ค๊ณ  ํฌ์คํํ๋ค.
๋ฐ๋๋ผJS๋ก React๋ฅผ ์ ์ฉํด๋ดค๊ณ  ์ด์  ๋๋์ด React์ ์ ์ฉํด๋ณด๊ฒ ๋ค.

์ด์  ๋ฐ๋๋ผJS ํฌ์คํ์ด ๊ถ๊ธํ๋ค๋ฉด
[Vanilla Redux-(1) Counter](https://velog.io/@cherrycock/Vanilla-Redux-1-COUNTER)
[Vanilla Redux-(2) ToDoList]
(https://velog.io/@cherrycock/Vanilla-Redux-2-To-Do-List)

## 1. Setup

### ๐ Add redux, rounter-dom

> ![](<https://images.velog.io/images/cherrycock/post/363e01b1-9880-40d7-9d30-718b166dcc95/(pakage.json).JPG>)**yarn add react-redux react-router-dom**

### ๐ src

> ![](https://images.velog.io/images/cherrycock/post/2692b11e-9a36-4320-aa58-d7d2c03ccefa/root.JPG)

### ๐ index.html

> ![](<https://images.velog.io/images/cherrycock/post/9328c333-dc44-4c77-9b26-626507fb6a0c/(index.hml1).JPG>)

### ๐ Index.js

> ![](<https://images.velog.io/images/cherrycock/post/d8f88e9d-6a5c-4e9a-aa6d-668fbe7673ca/(index.js1).JPG>)

### ๐ App.js

> ![](<https://images.velog.io/images/cherrycock/post/ce69875c-8b44-479c-81da-1dc4f64b3e08/(app.js1).JPG>)

### ๐ Home.js

> ![](<https://images.velog.io/images/cherrycock/post/ed977b4e-9448-4414-a1c4-2f17900dc9bc/(home.js).JPG>)

### ๐ Detail.js

> ![](<https://images.velog.io/images/cherrycock/post/d87b50c5-6c91-4213-a199-3327230a48f4/(detail.js).JPG>)

๊ธฐ๋ณธ์ ์ธ ์์์ด๋ค.
<code>Redux</code>, <code>Router</code>๋ฅผ ์ถ๊ฐํด์คฌ๊ณ  <code>App</code>์์
default component๋ **Home**
/detail์ **Detail**๋ก path๊ฐ์ ์ค์ ํด์ฃผ์๋ค.

**Home**์ด ๋ฆฌํดํ๋ ๊ฒ์
<code>form</code>ํ๊ทธ์ **text**๋ฅผ ์๋ ฅํ๋ <code>input</code>๊ณผ ์ถ๊ฐ๋ฒํผ์ธ <code>button</code> ๊ทธ๋ฆฌ๊ณ  <code>ul</code>์ด๋ค.
<code>useState</code>๋ฅผ ์ด์ฉํ์ฌ **text**๋ฅผ ์ ์ธํด์ฃผ์๊ณ 
<code>input</code> ์์ ๊ฐ์ด ๋ณ๊ฒฝ๋ ๋๋ง๋ค ํธ์ถ๋๋ <code>onChange</code>ํจ์์
<code>submit</code> ๋  ๋ ํธ์ถ๋๋ <code>onSubmit</code>ํจ์๋ฅผ ์์ฑํ์๋ค.
<code>input</code> ์์ ๊ฐ์ด ๋ณ๊ฒฝ๋ ๋ <code>onChange</code>ํจ์๊ฐ ํธ์ถ๋๊ณ  <code>setText</code>๋ฅผ ์ด์ฉํด
ํด๋น <code>event</code>๊ฐ์ฒด์ <code>target.value</code>๋ก **state**๊ฐ์ ์๋ฐ์ดํธ์์ผ์ค๋ค.
๊ทธ๋ผ <code>input value</code>๋ ์๋ก์๋ฐ์ดํธ๋ **state**๊ฐ์ด ๋์ด ๋ ๋๋ง๋๋ค.

**์ ๊ทธ๋ผ Store๋ฅผ ๋ง๋ค๊ณ  ์ฐ๋ํด๋ณด์!**

## 1.1 Connecting the Store

### ๐ Store.js

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

**store** ๊ตฌ์กฐ๋ ์์ ํฌ์คํํ ๊ฒ๊ณผ ๋์ผํ๋ค.
์ด๊ฒ์ ์ฐ๋ํ ๊ฑด๋ฐ,

### ๐ Index.js

> ![](<https://images.velog.io/images/cherrycock/post/724b4282-a1d9-4f70-b463-ade88385ec7d/(index.js2).JPG>)
> <code>Provider</code> ์ปดํฌ๋ํธ๋ฅผ ์ฌ์ฉํ์ฌ **App**์ **store**๋ฅผ ์ฐ๋ํ์๋ค.
> <code>Provider</code>๋ <code>react-redux</code> ๋ผ์ด๋ธ๋ฌ๋ฆฌ์ ๋ด์ฅ๋์ด์๋,
> ๋ฆฌ์กํธ ์ฑ์ **store**๋ฅผ ์์ฝ๊ฒ ์ฐ๋ ํ  ์ ์๋๋ก ๋์์ฃผ๋ ์ปดํฌ๋ํธ์ด๋ค.
> ์ด ์ปดํฌ๋ํธ๋ฅผ ๋ถ๋ฌ์ค๊ณ  ์ฐ๋ ํ  ์ปดํฌ๋ํธ๋ฅผ ๊ฐ์ธ์ค๋ค์์
> <code>Provider</code> ์ปดํฌ๋ํธ์ <code>props</code>๋ก **store** ๊ฐ์ ์ค์ ํด์ฃผ๋ฉด๋๋ค.

## 1.2 mapStateToProps

<code>redux-state</code>๋ก๋ถํฐ ์ ๋ณด๋ฅผ ๊ฐ์ง๊ณ  ์ฌ ์ ์์ด์ผํ๋ค.
์๋ค์ํผ ํ์ฌ **state**๋ ๋น์ด์๋ค.

ํ์ฌ ๋ธ๋ผ์ฐ์ ์ <code>toDo</code>๋ค์ ๋ ๋๋งํด์ฃผ๋ **Home**์ด๋ค.
**store**๋ก๋ถํฐ **state**๋ฅผ ๊ฐ์ ธ์ฌ ์ ์๋๋กํด์ผํ๋ค.
์ฆ, **connect** ์ฐ๋ํด์ค์ผํ๋ค.

> ![](<https://images.velog.io/images/cherrycock/post/b2db5569-96b9-4f26-9129-c85a4c84b952/(redux-org1).JPG>)<code>redux</code>๋ฌธ์์์ ๋ณด๋ฉด ์ด๊ฒ์ **mapStateToProps**๋ผ๊ณ  ๋ถ๋ฅด๊ณ ์๋ค.๊ธฐ๋ณธ์ ์ผ๋ก
> **mapStateToProps**๋ ํจ์์ธ๋ฐ ๋์ข๋ฅ์ <code>argument</code>์ ํจ๊ป ํธ์ถ๋๋ค.
> <code>state</code>๋ **redux store๋ก๋ถํฐ์จ state**
> <code>ownProps</code>๋ **component์ props**

์ ๊ทธ๋ผ <code>getCurrentState</code>ํจ์๋ฅผ ์ด์ฉํด์ **store**๋ก๋ถํฐ **state**๋ฅผ ๊ฐ์ง๊ณ ์ค์.

### ๐Home.js

```
function getCurrentState(state, ownProps) {
  console.log(state, ownProps);

};
export default connect(getCurrentState)(Home);
```

์ด๋ ๊ฒ <code>getCurrentState</code>ํจ์๋ฅผ ์คํ์ํค๊ณ  ์ฝ์์ ํ์ธํด๋ณด๋ฉด ๋ค์๊ณผ ๊ฐ๋ค.

### โ Console

> ![](<https://images.velog.io/images/cherrycock/post/05f86449-f5a0-4b2c-bd08-42b532a8d689/(console.log1).JPG>)์๋ฌ๋ฅผ ๋ณด๋ฉด **connect**์ <code>mapStateToProps</code>์ ์๋ฌ๊ฐ ์๊ฒผ๋ค๊ณ ํ๊ณ 
> ์ด๊ฒ์ <code>object</code>๋ฅผ ๋ฆฌํดํด์ผ๋๋ค๋ ๋ง์ด๋ค.
> ๋ง๋ ๋ง์ด๋ค ํ์ฌ ์ฐ๋ฆฐ ์๋ฌด๊ฒ๋ <code>return</code>ํด์ฃผ์ง์๊ณ ์๋ค.
> ํ์ง๋ง ์ค์ํ ๋ถ๋ถ์ ์ฝ์๋ก๊ทธ์ ์ฐํ
> <code>Redux store</code>๋ก ๋ถํฐ **state**๋ฅผ ๋ฐ์์ค๊ณ ์์์ ์ ์ ์๋ค.
> ํ์ธํ๊ธฐ ์ํด **default state**๋ฅผ ์ค์ ํด๋ณด์.

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

![](<https://images.velog.io/images/cherrycock/post/59840282-4e11-4f03-a2f6-90fbac1b7a27/(console.log2).JPG>)์ฝ์์ ํ์ธํด๋ณด๋ฉด
**์ฒซ๋ฒ์งธ argument๋ ํ์ฌ redux store์์ ์จ state์ด๋ค.**
<code>Hello?</code>
**๋๋ฒ์งธ argument๋ component์ props์ด๋ค.**
<code>๋ฆฌ์กํธ๋ผ์ฐํฐ์ ์ํด ์ฃผ์ด์ง history, location, match...</code>

<code>mapStateToProps</code>๋ฅผ ์ฌ์ฉํ๋ค๋ ๊ฑด **store**๋ก ๋ถํฐ ๋ฌด์์ธ๊ฐ๋ฅผ ๊ฐ์ ธ์ค๊ณ ์ถ๋ค๋๊ฒ์ด๋ค. ๊ทธ๋ฆฌ๊ณ ๋์ ์ปดํฌ๋ํธ์ <code>props</code>์ ๋ฃ๋๋ค.

์ฆ ํ์ฌ ์ผ์ด์ค์์์ **connect**ํจ์์ธ <code>getCurrentState</code>ํจ์๋
**Home**์ผ๋ก ๋ณด๋ด๋ <code>props</code>์ ์ถ๊ฐ๋  ์ ์๋๋ก ํ์ฉํด์ฃผ๋๊ฒ์ด๋ค.

```
function getCurrentState(state, ownProps) {
  return { toDos: state };
};

export default connect(getCurrentState)(Home);
```

์ด์  ํจ์์ด๋ฆ์ ๊ธฐ๋ณธ์ ์ผ๋ก <code>mapStateToProps</code>๋ก ๋ฐ๊ฟ์ค ๋ค์  
๋ฆฌํด๋ฌธ์ ์์ฑํ๊ณ  ์ฝ์์ ํ์ธํด๋ณด๋ฉด

> ![](<https://images.velog.io/images/cherrycock/post/057a7221-c971-45c7-a281-b4c22c155929/(console.log3).JPG>)**props์ state๊ฐ ์ถ๊ฐ๋์ด์๋ค.**

์ ๋ฆฌํ์๋ฉด, ํจ์์ ์ปดํฌ๋ํธ๋ฅผ ์ด์ฉํด์ **connect**๋ฅผ ์ฌ์ฉํ๊ธฐ๋ง ํ๋ฉด๋๋ค.

## 1.3 mapDispatchToProps

์ด๋ฒ์ **connect**์ ๋๋ฒ์งธ ์ธ์์ธ **mapDispatchToProps**๋ฅผ ์ ์ฉํด๋ณด๊ฒ ๋ค.

๋จผ์  **mapDispatchToProps**ํจ์๋ฅผ ์์ฑํ๊ณ 
<code>์ธ์๋ก๋ dispatch์ ownProps๊ฐ ์์ง๋ง ์ง๊ธ์ dispatch๋ง ์ฌ์ฉํ๊ฒ ๋ค.</code>

```
function mapDispatchToProps(dispatch){
}
```

**connect**์ ๋๋ฒ์งธ ์ธ์๋ก ์๋ ฅํด์ค๋ค.

```
export default connect(mapStateToProps, mapDispatchToProps)(Home);
```

์ด์  <code>prop</code>์ ๋ง๋ค์ด์ฃผ์.
๋จผ์  <code>store.js</code>์์ <code>addToDo</code>, <code>DeleteToDo</code>๋ฅผ <code>unexport</code>ํด์ฃผ๊ณ 
<code>actionCreators</code>ํจ์๋ฅผ ๋ง๋  ๋ค์ ์ด๊ฒ์ <code>export</code>ํด์ฃผ๊ฒ ๋ค.

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

๋ค์ **Home**์ผ๋ก ์์ **mapDispatchToProps**ํจ์๋ฅผ ์์ฑํด๋ณด๊ฒ ๋ค.
**store**์ **addToDo**๋ฅผ <code>retrun</code>ํ๊ฒ๋๋ง์ด๋ค.

```
function mapDispatchToProps(dispatch){
  return {
    addToDo: text => dispatch(actionCreators.addToDo(text))
  };
}
```

์ด๋ ๊ฒ **addToDo**๋ผ๋ ํจ์๋ฅผ ๋ง๋ค์๋ค.
**addToDo**๋ <code>text argument</code>๋ฅผ ํ์๋กํ๊ณ 
**addToDo** ๊ฐ ํ๋์ผ์ **dispatch**๋ฅผ ํธ์ถํ๋ค ๊ทธ๋ฆฌ๊ณ 
**dispatch**๋ <code>actionCreators</code>๋ฅผ ํธ์ถํ ๊ฒ์ด๊ณ 
**addToDo**๋ <code>text</code>๋ฅผ ๋ฐ์์ผํ๋ค.
์กฐ๊ธ ์ ๋ฆฌํ์๋ฉด..
์ด ํจ์๋ <code>text</code>๋ฅผ ์ธ์๋ก ๋ฐ๊ณ  ์ด ํจ์๊ฐ ์คํ๋๋ฉด
**dispatch**๋ฅผ ํธ์ถํ๋ค <code>actionCreators.addToDo(text)</code>์ ํจ๊ป

๊ทธ๋ผ ์ด์  ์ฑ๊ณต์ ์ผ๋ก ๋ฆฌ์กํธ ์ปดํฌ๋ํธ๋ก๋ถํฐ
**reducer**์๊ฒ **dispatch**๋ฅผ ํ๋๊ฒ์ด๋ค.
<br/>

**๊ทธ๋ผ ์ด์  ToDo์ปดํฌ๋ํธ๋ฅผ ์์ฑํด ๋ ๋๋ง์ ํด๋ณด๊ณ  ์ญ์ ๊ธฐ๋ฅ์ ๋ง๋ค์ด๋ณด์.**

## 1.4 Deleting To Do

### ๐ ToDo.js

> ![](<https://images.velog.io/images/cherrycock/post/d0a37834-719a-4cd8-bfcc-f548094298c0/(todo.js1).JPG>)<code>props</code>๋ก <code>text</code>๋ฅผ ๋ฐ์์ค๋ **ToDo์ปดํฌ๋ํธ**์ด๋ค.

### ๐ Home.js

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

**mapStateToProps**ํจ์๋ก๋ถํฐ ๋ฐ์์จ <code>prop</code>์ธ **toDos**์ <code>Array.prototype.map()</code>๋ฉ์๋๋ฅผ ์ด์ฉํ์ฌ
**ToDo component**๋ฅผ ๋ ๋๋งํ๋ค.
**ToDo component**๋ <code>text</code>๋ฅผ ๋ฐ์์ค๊ณ  {text}๋ liํ๊ทธ์ ์๋ค.
์ด์  <code>submit</code>๋ ๋๋ง๋ค ๋ฆฌ์คํธ๋ค์ด ์ถ๊ฐ๊ฐ ๋ ๊ฒ์ด๋ค.

์ด์  ๋ณธ๊ฒฉ์ ์ผ๋ก ์ญ์ ๊ธฐ๋ฅ์ ๋ง๋ค์ด๋ณด์.
๋๊ตฐ๊ฐ๊ฐ del๋ฒํผ์ ๋๋ ์๋ ๊ทธ ํด๋น **ToDo**๋ฅผ ์ง์์ผํ๋ค.
**ToDo**๋ฅผ ์ง์ฐ๊ธฐ์ํด ๋ญ๊ฐ ํ์ํ ๊น?
id๊ฐ ํ์ํ๋ค.
**store.dispatch()**๋ฅผ ํธ์ถํด์ผ๋๋๋ฐ
<code>store.dispatch({ type:del, id })</code> (์ด๋ฐ์์ผ๋ก)
ํ์ฌ ์ด๋ค ๋ฐฉ๋ฒ์ผ๋ก dispatch๋์์ ์ ๊ทผ์ ํด์ผํ ๊น?
์ด์ ์ฑํฐ์์ ์ ์ฉ์์ผฐ๋ **mapDispatchToProps**๋ฅผ ์ด์ฉํด๋ณด์.
**ToDo**๋ ์ค๋ก์ง **dispatch**๋ง ์ ๊ฒฝ์ฐ๋ฉด๋๋ค.
**ToDo**๋ **reducer**์๊ฒ ๋ฉ์ธ์ง๋ฅผ ๋ณด๋ด์ผํ๋ค.
์ฆ, **ToDo**๋ <code>state</code>์๋ ์ ๊ฒฝ์์ฐ์ง์์๋ ๋๋ค.

๊ทธ๋ ๋ค๋ฉด **ToDo**์๋ **connect**ํด๋ณด์.

### ๐ ToDo.js

> ![](<https://images.velog.io/images/cherrycock/post/a800bcea-be2b-4010-8e80-41d486b5e0eb/(todo.js2).JPG>)
> **ToDo**๋ฅผ ์ง์ฐ๊ธฐ์ํด์๋ id๊ฐ ํ์ํ์ง๋ง
> ํ์ฌ <code>onBtnClick</code>ํจ์๋ ์ธ์๋ก id๋ฅผ ๋ฐ์ ํ์๊ฐ ์๋ค.
> ์๋ํ๋ฉด **home**์์์ id๋ฅผ <code>prop</code>์ผ๋ก ๋ฐ์๊ธฐ๋๋ฌธ์
> <code>ToDo key={toDo.id}</code>
> **mapDispatchToProps**ํจ์์ ๋๋ฒ์งธ ์ธ์์ธ
> <code>ownProps</code>๋ฅผ ์ฌ์ฉํ์ฌ id์ ์ ๊ทผํ๋ฉด๋๋ค.

**์ด๋ ๊ฒ ์ญ์ ๊น์ง ๊ฐ๋ฅํ๊ฒํ์๊ณ  ๋ง์ง๋ง์ผ๋ก detail์ปดํฌ๋ํธ๋ฅผ ๋ค๋ค๋ณด์.**

## 1.5 Detail Screen

### ๐App.js

> ![](<https://images.velog.io/images/cherrycock/post/c5bbad3c-fd5a-4322-8361-b7142c8e7b73/(app.js3).JPG>)**detail์ path๊ฐ์ "/detail"์์ "/:id"๋ก ์์ ํ์๋ค.**

### ๐ToDo.js

> ![](<https://images.velog.io/images/cherrycock/post/5f1bed0a-54f5-4e1f-aa86-e9bb404ee0ea/(todo.js3).JPG>)**ํด๋ฆญํ๋ฉด ๋ค๋ฅธ ์ฃผ์๋ก ์ด๋ํ๋ React-router์ <code>Link</code>์ปดํฌ๋ํธ๋ฅผ ์ฌ์ฉํด id๊ฐ์ ๋๊ฒจ์ฃผ๋ฉฐ detail์ปดํฌ๋ํธ๋ก ์ด๋์ํจ๋ค.**

### ๐Detail.js

> ![](<https://images.velog.io/images/cherrycock/post/a6d3c2c0-07d1-4490-81fa-4a5237843c9f/(detail.js2).JPG>)
> **connect๋ฅผํ๊ณ  mapStateToProps์ ์์ฑํด toDo๋ฅผ ๋ฆฌํดํด์ค๋ค.**
> **toDo์ text์ id๊ฐ ์๋ค๋ฉด ๊ทธ ๊ฐ์ ๋ ๋๋งํ๋ค.**
