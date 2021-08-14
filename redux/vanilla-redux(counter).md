### 😲 시작하기에 앞서

노마드강의의 초보자를 위한 리덕스 101을 복습하며 정리하려고 포스팅한다.
react에 redux를 사용하기 전 바닐라로 조금 더 쉽게 개념을 잡아보려고한다.

## 1. Vanilla Counter

### 😁 index.html

> ![](<https://images.velog.io/images/cherrycock/post/e55766d2-35be-44e3-aeed-e04619dc55d8/vanilla-redux(index.html).JPG>)html은 간단하다
> add,minus버튼과 가운데 state의 값을 나타내는 span태그로 구성하였다.

### 😁 index.js

> ![](<https://images.velog.io/images/cherrycock/post/e468b6e4-593e-46c5-84e3-409d1b07b9ef/vanilla-redux(index.js).JPG>)자바스크립트 코드 또한 매우 심플하다.
> 클릭이벤트를 이용해 각각의 버튼을 눌렀을 때
> handleAdd, handleMinus함수를 실행시킨다.
> 각각의 함수에서는 count값을 <code>+</code>,<code>-</code>시켜주며 updateText함수를 실행시키는데
> updateText함수는 number.innerText = count 함으로써 현재 count값을 보여주는 함수이다.
> 이것을 이제 아주 심플한 리덕스로 교체할 것이다.

## 1-1 Store and Reducer

### 😀 Add redux

> **yarn add redux
> import { createStore } from "redux"**

### 🙄 Store?

**Store**</code>가 하는 일은 기본적으로 <code>data</code>를 넣을 수 있는 장소를 생성한다.
`redux는 data를 (관리하는데) 도와주는 역할을 하기 위해 만들어졌다.`
현 케이스에서는 리덕스가 -1이나 +1을 <code>count</code>하는 걸 도와주기 위해 필요하다.
우리는 <code>data</code>를 어딘가에 넣어줘야하고 그 데이터는 **store**라는 곳에
저장 되어야 한다. **자!! 그럼 store를 만들어보자.**

> **const store = createStore();**

**하지만 에러가 뜰 것이다.**

> ![](<https://images.velog.io/images/cherrycock/post/ecb05fbc-153d-4b28-9f53-d50e12ba7e0f/vanilla-redux-1(error1).JPG>)**(Reducer가 function이어야함)**

**그렇다면 reducer라는 function을 만들어보자.**

### 😀index.js

> ![](<https://images.velog.io/images/cherrycock/post/2741a395-eefe-47a5-bced-ef6c775af33f/vanilla-redux(index.js2).JPG>)**reducer**는 **함수**이고 나의 <code>data</code>를 <code>modify</code>한다.
> 만약 **reducer**가 hello라고 <code>return</code>하게된다면
> 현재 <code>application</code>에 있는 <code>data</code>가 될 것이다.

### 😀index.js

> ![](<https://images.velog.io/images/cherrycock/post/39bab11d-2a51-42b2-8b74-b27d917f426b/vanilla-redux(index.js3).JPG>)
> **reducer**라는 용어가 처음엔 어려울수 있어 rename을 해줬다.
> <code>recuer ㅡ> countModifier</code>

**countStore을 console해보면**

### 📕console

> ![](https://images.velog.io/images/cherrycock/post/2b937f5a-6945-4d74-9a68-6869403e2bcc/console1.JPG)
> <code>dispatch, getState, replaceReducer, subscribe</code>가 있는것을
> 확인할 수 있고 여기서 중요한 파트인 <code>getState</code>를 사용해보겠다.

### 😀index.js

> ![](<https://images.velog.io/images/cherrycock/post/f273cad9-226f-44bd-a7eb-0c569dd52464/vanilla-redux(index.js4).JPG>)
> **countModifier(reducer)**는 <code>data</code>를 바꿔준다.
> 또 뭐든지 <code>return</code>하는 것은 <code>application</code>에 있는 <code>data</code>이다.
> 현 케이스처럼 만약 **countModifer(reducer)**가 "hello"라고 <code>return</code>을 하면
> 우리의 <code>application</code>의 <code>data</code>가 되는것이다.<br/>
> **state**의 default값을 0으로 설정해주고 **state**를 console하면
> default로 **state**는 0이 될것이다.
> <code>이것은** state**를 initializing하는 것이다.</code>

유일하게 **countModififer**만 state를 modify할 수 있다.
자. 그렇다면 **countModifier**로 하여금 ++, --를 할 수 있을까 ?
그것을 <code>action</code>을 통해 가능하다.

## 1-2 Actions

### 🙄 Actions?

**action**은 redux에서 function을 부를 때 쓰는 두번째 파라미터 혹은 argument다.
그래서 어떻게 countModifier에게 **action**을 보낼 수 있을까?
store를 사용하는 방법 즉 <code>countStore.dispatch()</code>를 입력해서
**action**을 보낼 수 있다.<code>action은 object이어야한다.</code>

### 😀index.js

> ![](<https://images.velog.io/images/cherrycock/post/88704db1-b01d-40be-91ee-cd5e0145aa23/vanilla-redux(index.js5).JPG>)<code>dispatch와 함께 countModifier로 메세지를 보내는 것이다.</code>
> 위에서 말했듯이 countModifier가 return하는 모든 것은, data가 된다.
> 현 케이스에서는 action의 type이 "ADD"일때 count+1을 리턴하게 되고
> <code>console.log(countStore.getState())</code>를 하게 된다면
> 콘솔엔 state값으로 1이 찍힐 것이다.
> (현재는 버튼을 누르지않아도 <code>countStore.dispatch({ type: "ADD" });</code>
> 로 인해 메세지가 전달된다.)

정리하자면
data의 store를 만들고
<code>const countStore = createStore(countModifier)</code>

data를 modify하는 countModifier(reducer)를 만든다.
<code>const countModifier = () => {}</code>

message를 store에 보낼 수 있으며
message를 send 하는 방법은 dispatch를 사용하면된다.
<code>countStore.dispatch({ type: "ADD" })</code>

내가 전송한 message는 action에 넣으면 되고,

여기서 해야 할 일은 action을 체크해보면된다.
<code>if(action.type === "ADD"</code>

## 1-3 Subscriptions

### 🙄Subscribe?

**subscribe**는 **store안에 있는 변화들을 알 수 있게 해준다.**
**subscribe**는 코드로 더 자세히 알아보자.

### 😀index.js

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
  console.log("변화생김");
  number.innerText = countStore.getState();
}

countStore.subscribe(onChange);

//익명함수 대신 핸들링해주는 함수를 만들어줬다.
const handleAdd = () => {
  countStore.dispatch({ type: "ADD" });
}

const handleMinus = () => {
  countStore.dispatch({ type: "MINUS" });
}

add.addEventListener('click', handleAdd);
minus.addEventListener('click', handleMinus);
```

store에서 subscribe을하고
<code>countStore.subscribe();</code>

subscribe에서 onChange함수를 실행시킨다.
<code>countStore.subscribe(onChange);</code>

onChange함수는 number의 innerText값을
store의 data값으로 바꿔준다.
언제? data에 변화가 생겼을때
<code>const onChange = () => {
console.log("변화생김");
number.innerText = countStore.getState();
}
</code>

**console.log를 확인해보면**

### 📕console

> ![](https://images.velog.io/images/cherrycock/post/5947a710-5b78-4b00-8698-82e1deabaa89/console2.JPG)버튼을 눌렀을때 변화가 생겼다고 알려준다.

## 1-4 Recap Refactor

**마지막으로 코드를 조금 더 개선해보자.**

### ❗ 개선사항(1)

> ![](https://images.velog.io/images/cherrycock/post/bc6a46bd-fda4-4f4c-b52b-38397eeba391/redux%20%EA%B3%B5%EC%8B%9D%EB%AC%B8%EC%84%9C1.JPG)![](<https://images.velog.io/images/cherrycock/post/5796e2b1-7078-45eb-826b-74a903da4b7a/vanilla-redux(index.js6).JPG>)redux 공식문서처럼 <code>if대신 switch문으로 바꿔주었다.</code>

### ❗ 개선사항(2)

> ![](https://images.velog.io/images/cherrycock/post/102c6ddd-1f70-4d3c-8260-46cd490739e6/%EA%B0%9C%EC%84%A0%EC%82%AC%ED%95%AD2.JPG)reducer에게 dispatch할때 type을
> <code>string타입인 아닌 변수를 선언하여 그것을 이용해주었다.</code><br/>
> 만약 type을 MINUS가 아닌 MIN로 잘못적었을 때
> <code>const handleMinus = () => {
> countStore.dispatch({ type: MIN ~~US~~ });
> }</code> 에러를 확인해보면
> ![](https://images.velog.io/images/cherrycock/post/53432a3d-be4c-400c-a42a-7cdbd2d892d2/error1.JPG)**"MIN" is not defined**
> 즉 "MIN"이 defined되지않았기 때문이라고 자바스크립트가 친절하게 알려준다.만약 string을 쓴다면 자바스크립트가 아무것도 말해주지않는다.
