### ๐ฒ ์์ํ๊ธฐ์ ์์

๋ธ๋ง๋๊ฐ์์ ์ด๋ณด์๋ฅผ ์ํ ๋ฆฌ๋์ค 101์ ๋ณต์ตํ๋ฉฐ ์ ๋ฆฌํ๋ ค๊ณ  ํฌ์คํํ๋ค.
react์ redux๋ฅผ ์ฌ์ฉํ๊ธฐ ์  ๋ฐ๋๋ผ๋ก ์กฐ๊ธ ๋ ์ฝ๊ฒ ๊ฐ๋์ ์ก์๋ณด๋ ค๊ณ ํ๋ค.

## 1. Vanilla Counter

### ๐ index.html

> ![](<https://images.velog.io/images/cherrycock/post/e55766d2-35be-44e3-aeed-e04619dc55d8/vanilla-redux(index.html).JPG>)html์ ๊ฐ๋จํ๋ค
> add,minus๋ฒํผ๊ณผ ๊ฐ์ด๋ฐ state์ ๊ฐ์ ๋ํ๋ด๋ spanํ๊ทธ๋ก ๊ตฌ์ฑํ์๋ค.

### ๐ index.js

> ![](<https://images.velog.io/images/cherrycock/post/e468b6e4-593e-46c5-84e3-409d1b07b9ef/vanilla-redux(index.js).JPG>)์๋ฐ์คํฌ๋ฆฝํธ ์ฝ๋ ๋ํ ๋งค์ฐ ์ฌํํ๋ค.
> ํด๋ฆญ์ด๋ฒคํธ๋ฅผ ์ด์ฉํด ๊ฐ๊ฐ์ ๋ฒํผ์ ๋๋ ์ ๋
> handleAdd, handleMinusํจ์๋ฅผ ์คํ์ํจ๋ค.
> ๊ฐ๊ฐ์ ํจ์์์๋ count๊ฐ์ <code>+</code>,<code>-</code>์์ผ์ฃผ๋ฉฐ updateTextํจ์๋ฅผ ์คํ์ํค๋๋ฐ
> updateTextํจ์๋ number.innerText = count ํจ์ผ๋ก์จ ํ์ฌ count๊ฐ์ ๋ณด์ฌ์ฃผ๋ ํจ์์ด๋ค.
> ์ด๊ฒ์ ์ด์  ์์ฃผ ์ฌํํ ๋ฆฌ๋์ค๋ก ๊ต์ฒดํ  ๊ฒ์ด๋ค.

## 1-1 Store and Reducer

### ๐ Add redux

> **yarn add redux
> import { createStore } from "redux"**

### ๐ Store?

**Store**</code>๊ฐ ํ๋ ์ผ์ ๊ธฐ๋ณธ์ ์ผ๋ก <code>data</code>๋ฅผ ๋ฃ์ ์ ์๋ ์ฅ์๋ฅผ ์์ฑํ๋ค.
`redux๋ data๋ฅผ (๊ด๋ฆฌํ๋๋ฐ) ๋์์ฃผ๋ ์ญํ ์ ํ๊ธฐ ์ํด ๋ง๋ค์ด์ก๋ค.`
ํ ์ผ์ด์ค์์๋ ๋ฆฌ๋์ค๊ฐ -1์ด๋ +1์ <code>count</code>ํ๋ ๊ฑธ ๋์์ฃผ๊ธฐ ์ํด ํ์ํ๋ค.
์ฐ๋ฆฌ๋ <code>data</code>๋ฅผ ์ด๋๊ฐ์ ๋ฃ์ด์ค์ผํ๊ณ  ๊ทธ ๋ฐ์ดํฐ๋ **store**๋ผ๋ ๊ณณ์
์ ์ฅ ๋์ด์ผ ํ๋ค. **์!! ๊ทธ๋ผ store๋ฅผ ๋ง๋ค์ด๋ณด์.**

> **const store = createStore();**

**ํ์ง๋ง ์๋ฌ๊ฐ ๋ฐ ๊ฒ์ด๋ค.**

> ![](<https://images.velog.io/images/cherrycock/post/ecb05fbc-153d-4b28-9f53-d50e12ba7e0f/vanilla-redux-1(error1).JPG>)**(Reducer๊ฐ function์ด์ด์ผํจ)**

**๊ทธ๋ ๋ค๋ฉด reducer๋ผ๋ function์ ๋ง๋ค์ด๋ณด์.**

### ๐index.js

> ![](<https://images.velog.io/images/cherrycock/post/2741a395-eefe-47a5-bced-ef6c775af33f/vanilla-redux(index.js2).JPG>)**reducer**๋ **ํจ์**์ด๊ณ  ๋์ <code>data</code>๋ฅผ <code>modify</code>ํ๋ค.
> ๋ง์ฝ **reducer**๊ฐ hello๋ผ๊ณ  <code>return</code>ํ๊ฒ๋๋ค๋ฉด
> ํ์ฌ <code>application</code>์ ์๋ <code>data</code>๊ฐ ๋  ๊ฒ์ด๋ค.

### ๐index.js

> ![](<https://images.velog.io/images/cherrycock/post/39bab11d-2a51-42b2-8b74-b27d917f426b/vanilla-redux(index.js3).JPG>)
> **reducer**๋ผ๋ ์ฉ์ด๊ฐ ์ฒ์์ ์ด๋ ค์ธ์ ์์ด rename์ ํด์คฌ๋ค.
> <code>recuer ใก> countModifier</code>

**countStore์ consoleํด๋ณด๋ฉด**

### ๐console

> ![](https://images.velog.io/images/cherrycock/post/2b937f5a-6945-4d74-9a68-6869403e2bcc/console1.JPG)
> <code>dispatch, getState, replaceReducer, subscribe</code>๊ฐ ์๋๊ฒ์
> ํ์ธํ  ์ ์๊ณ  ์ฌ๊ธฐ์ ์ค์ํ ํํธ์ธ <code>getState</code>๋ฅผ ์ฌ์ฉํด๋ณด๊ฒ ๋ค.

### ๐index.js

> ![](<https://images.velog.io/images/cherrycock/post/f273cad9-226f-44bd-a7eb-0c569dd52464/vanilla-redux(index.js4).JPG>)
> **countModifier(reducer)**๋ <code>data</code>๋ฅผ ๋ฐ๊ฟ์ค๋ค.
> ๋ ๋ญ๋ ์ง <code>return</code>ํ๋ ๊ฒ์ <code>application</code>์ ์๋ <code>data</code>์ด๋ค.
> ํ ์ผ์ด์ค์ฒ๋ผ ๋ง์ฝ **countModifer(reducer)**๊ฐ "hello"๋ผ๊ณ  <code>return</code>์ ํ๋ฉด
> ์ฐ๋ฆฌ์ <code>application</code>์ <code>data</code>๊ฐ ๋๋๊ฒ์ด๋ค.<br/>
> **state**์ default๊ฐ์ 0์ผ๋ก ์ค์ ํด์ฃผ๊ณ  **state**๋ฅผ consoleํ๋ฉด
> default๋ก **state**๋ 0์ด ๋ ๊ฒ์ด๋ค.
> <code>์ด๊ฒ์** state**๋ฅผ initializingํ๋ ๊ฒ์ด๋ค.</code>

์ ์ผํ๊ฒ **countModififer**๋ง state๋ฅผ modifyํ  ์ ์๋ค.
์. ๊ทธ๋ ๋ค๋ฉด **countModifier**๋ก ํ์ฌ๊ธ ++, --๋ฅผ ํ  ์ ์์๊น ?
๊ทธ๊ฒ์ <code>action</code>์ ํตํด ๊ฐ๋ฅํ๋ค.

## 1-2 Actions

### ๐ Actions?

**action**์ redux์์ function์ ๋ถ๋ฅผ ๋ ์ฐ๋ ๋๋ฒ์งธ ํ๋ผ๋ฏธํฐ ํน์ argument๋ค.
๊ทธ๋์ ์ด๋ป๊ฒ countModifier์๊ฒ **action**์ ๋ณด๋ผ ์ ์์๊น?
store๋ฅผ ์ฌ์ฉํ๋ ๋ฐฉ๋ฒ ์ฆ <code>countStore.dispatch()</code>๋ฅผ ์๋ ฅํด์
**action**์ ๋ณด๋ผ ์ ์๋ค.<code>action์ object์ด์ด์ผํ๋ค.</code>

### ๐index.js

> ![](<https://images.velog.io/images/cherrycock/post/88704db1-b01d-40be-91ee-cd5e0145aa23/vanilla-redux(index.js5).JPG>)<code>dispatch์ ํจ๊ป countModifier๋ก ๋ฉ์ธ์ง๋ฅผ ๋ณด๋ด๋ ๊ฒ์ด๋ค.</code>
> ์์์ ๋งํ๋ฏ์ด countModifier๊ฐ returnํ๋ ๋ชจ๋  ๊ฒ์, data๊ฐ ๋๋ค.
> ํ ์ผ์ด์ค์์๋ action์ type์ด "ADD"์ผ๋ count+1์ ๋ฆฌํดํ๊ฒ ๋๊ณ 
> <code>console.log(countStore.getState())</code>๋ฅผ ํ๊ฒ ๋๋ค๋ฉด
> ์ฝ์์ state๊ฐ์ผ๋ก 1์ด ์ฐํ ๊ฒ์ด๋ค.
> (ํ์ฌ๋ ๋ฒํผ์ ๋๋ฅด์ง์์๋ <code>countStore.dispatch({ type: "ADD" });</code>
> ๋ก ์ธํด ๋ฉ์ธ์ง๊ฐ ์ ๋ฌ๋๋ค.)

์ ๋ฆฌํ์๋ฉด
data์ store๋ฅผ ๋ง๋ค๊ณ 
<code>const countStore = createStore(countModifier)</code>

data๋ฅผ modifyํ๋ countModifier(reducer)๋ฅผ ๋ง๋ ๋ค.
<code>const countModifier = () => {}</code>

message๋ฅผ store์ ๋ณด๋ผ ์ ์์ผ๋ฉฐ
message๋ฅผ send ํ๋ ๋ฐฉ๋ฒ์ dispatch๋ฅผ ์ฌ์ฉํ๋ฉด๋๋ค.
<code>countStore.dispatch({ type: "ADD" })</code>

๋ด๊ฐ ์ ์กํ message๋ action์ ๋ฃ์ผ๋ฉด ๋๊ณ ,

์ฌ๊ธฐ์ ํด์ผ ํ  ์ผ์ action์ ์ฒดํฌํด๋ณด๋ฉด๋๋ค.
<code>if(action.type === "ADD"</code>

## 1-3 Subscriptions

### ๐Subscribe?

**subscribe**๋ **store์์ ์๋ ๋ณํ๋ค์ ์ ์ ์๊ฒ ํด์ค๋ค.**
**subscribe**๋ ์ฝ๋๋ก ๋ ์์ธํ ์์๋ณด์.

### ๐index.js

```
import { createStore } from "redux";

const add = document.getElementById('add');
const minus = document.getElementById("minus");
const number = document.querySelector('span');

number.innerText = 0;

//reducer
const countModifier = (count = 0, action) => {
  console.log(count, action);
  if (action.type === "ADD"){
    return count + 1;
  }else if(action.type === "MINUS"){
    return count - 1;
  }else {
   return count;
  }
};

//store
const countStore = createStore(countModifier);


const onChange = () => {
  console.log("๋ณํ์๊น");
  number.innerText = countStore.getState();
}

countStore.subscribe(onChange);

//์ต๋ชํจ์ ๋์  ํธ๋ค๋งํด์ฃผ๋ ํจ์๋ฅผ ๋ง๋ค์ด์คฌ๋ค.
const handleAdd = () => {
  countStore.dispatch({ type: "ADD" });
}

const handleMinus = () => {
  countStore.dispatch({ type: "MINUS" });
}

add.addEventListener('click', handleAdd);
minus.addEventListener('click', handleMinus);
```

store์์ subscribe์ํ๊ณ 
<code>countStore.subscribe();</code>

subscribe์์ onChangeํจ์๋ฅผ ์คํ์ํจ๋ค.
<code>countStore.subscribe(onChange);</code>

onChangeํจ์๋ number์ innerText๊ฐ์
store์ data๊ฐ์ผ๋ก ๋ฐ๊ฟ์ค๋ค.
์ธ์ ? data์ ๋ณํ๊ฐ ์๊ฒผ์๋
<code>const onChange = () => {
console.log("๋ณํ์๊น");
number.innerText = countStore.getState();
}
</code>

**console.log๋ฅผ ํ์ธํด๋ณด๋ฉด**

### ๐console

> ![](https://images.velog.io/images/cherrycock/post/5947a710-5b78-4b00-8698-82e1deabaa89/console2.JPG)๋ฒํผ์ ๋๋ ์๋ ๋ณํ๊ฐ ์๊ฒผ๋ค๊ณ  ์๋ ค์ค๋ค.

## 1-4 Recap Refactor

**๋ง์ง๋ง์ผ๋ก ์ฝ๋๋ฅผ ์กฐ๊ธ ๋ ๊ฐ์ ํด๋ณด์.**

### โ ๊ฐ์ ์ฌํญ(1)

> ![](https://images.velog.io/images/cherrycock/post/bc6a46bd-fda4-4f4c-b52b-38397eeba391/redux%20%EA%B3%B5%EC%8B%9D%EB%AC%B8%EC%84%9C1.JPG)![](<https://images.velog.io/images/cherrycock/post/5796e2b1-7078-45eb-826b-74a903da4b7a/vanilla-redux(index.js6).JPG>)redux ๊ณต์๋ฌธ์์ฒ๋ผ <code>if๋์  switch๋ฌธ์ผ๋ก ๋ฐ๊ฟ์ฃผ์๋ค.</code>

### โ ๊ฐ์ ์ฌํญ(2)

> ![](https://images.velog.io/images/cherrycock/post/102c6ddd-1f70-4d3c-8260-46cd490739e6/%EA%B0%9C%EC%84%A0%EC%82%AC%ED%95%AD2.JPG)reducer์๊ฒ dispatchํ ๋ type์
> <code>stringํ์์ธ ์๋ ๋ณ์๋ฅผ ์ ์ธํ์ฌ ๊ทธ๊ฒ์ ์ด์ฉํด์ฃผ์๋ค.</code><br/>
> ๋ง์ฝ type์ MINUS๊ฐ ์๋ MIN๋ก ์๋ชป์ ์์ ๋
> <code>const handleMinus = () => {
> countStore.dispatch({ type: MIN ~~US~~ });
> }</code> ์๋ฌ๋ฅผ ํ์ธํด๋ณด๋ฉด
> ![](https://images.velog.io/images/cherrycock/post/53432a3d-be4c-400c-a42a-7cdbd2d892d2/error1.JPG)**"MIN" is not defined**
> ์ฆ "MIN"์ด defined๋์ง์์๊ธฐ ๋๋ฌธ์ด๋ผ๊ณ  ์๋ฐ์คํฌ๋ฆฝํธ๊ฐ ์น์ ํ๊ฒ ์๋ ค์ค๋ค.๋ง์ฝ string์ ์ด๋ค๋ฉด ์๋ฐ์คํฌ๋ฆฝํธ๊ฐ ์๋ฌด๊ฒ๋ ๋งํด์ฃผ์ง์๋๋ค.
