# [리액트 무료 강좌(웹게임)🤖🎳]
> #### 출처: [리액트 무료 강좌(웹게임)_ZeroChoTV](https://www.youtube.com/playlist?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)  
***

## 목차
[1 React Class](#1-React-Class)  
[2 Hooks 및 웹팩설치](#2-Hooks-및-웹팩설치)  
[3 React에서 사용하는 함수와 숫자야구](#3-React에서-사용하는-함수와-숫자야구)  
[4 ](#4-)  
[5 ](#5-)  
[6 ](#6-)  
[7 ](#7-)  
[8 ](#8-)  
[9 ](#9-)  
[10 개인 추가 공부](#10-개인-추가-공부)  
* * *


## 1 React Class
### 🟥 [1-1. 리액트를 왜 쓰는가?](https://youtu.be/aYwSrzeyUOk?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- 한국에선 react가 대세
- 18버전 나옴, 하지만 17버전 사용하는 회사들도 많을 것
- Single Page Application : 서버로부터 새로운 페이지를 가져오는 것이 아닌, 하나의 페이지에서 내용을 동적으로 변경함으로써 사용자 웹앱을 의미
- 요즘은 웹에서 '사이트❌'가 아닌 다양한 '앱⭕'을 돌림
### 🟧 [1-2. 강의 수강 시 주의할 점](https://youtu.be/8M_q50Vff4M?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- react배우느라 html, css, js를 소홀히 해선 안됨
- js는 기본으로 익혀둬야함 (인간js엔진되기 강좌)
- **creat react app**으로 실행하는 경우가 많음, 하지만 입문자를 대상으로 한 강의이기 때문에 기본기를 다잡는 수업을 할 예정
### 🟨 [1-3. 첫 리액트 컴포턴트(아직은 Class)](https://youtu.be/5lgITNI0ZJo?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- react로 프로그래밍 하더라도 html,css, js가 나와야 프로그램이 파일들을 읽어냄
- 원시적인 형태부터 강좌 시작할거임  


```html
<script crossorigin src="https://unpkg.com/react@16/umd/react.development.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script> //개발용 추후 배포용으로 바꿔야함
```
```jsx
'use strict';

1. class 방식 => 99% 요즘 안씀, 1%는 error boundary에서 사용함
class LikeButton extends React.Component{
    constructor(props){
        super(props);
        this.state = {liked::false}
    }
    render(){
        if(this.state.liked){
            return 'u liked this'
        }
        return React.creatElement('button',{onClick:()=>this.setState({liked:true})}, 'Like')
    }
}



2. function 방식
const LikeButton = () => {};
function LikeButton(){}
```
- component: 데이터(state)와 화면(render)을 하나로 묶어둔 덩어리
- 화면 바뀌는 부분: state   

### 🟩 [1-4. 가독성을 위한 JSX(XML임!)](https://youtu.be/MtbLgbJFoss?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- 가독성을 위해 **xml + javascript = jsx** 탄생! 😝
- jsx 문법  
    (1) tag는 소문자로 시작  
    (2) js코드는 {중괄호}로 감싸기  
    (3) 삼항연산자, 배열 많이.. 사용 ..  
    (4) return안에 형제끼리는 나란히 올수없어서 <></>로 묶어줘(fragment)
    (5) 닫는 tag 꼭 넣어줘야함 ``(예)<input />``
```js
return(
    <button onClick={()=>this.setState({liked:true})}>Like</button>
)
```
- Babel library가 jsx를 만나면 `` return React.creatElement(~~)``로 바꿔줌  
- ➕ Babel 추가하는 방법  
``<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>``  
``<script type="text/babel">`` 추가함
- ✔ react 17버전  
``ReactDOM.render(<LikeButton/>, document.querySelector('#root'))``
- ✔ react 18버전  
``ReactDOM.creatRoot(document.querySelector('#root').render(<LikeButton/>))``

### 🟦 [1-5. 클래스 컴포넌트의 형태와 리액트 데브툴즈](https://youtu.be/fpc7KnqFGrs?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- 화면에 나올 모든것들을 return에 적어
- **데이터 중심 사고** : 화면에서 달라질 부분을 state로!  
- ✔ [react dev tools 사용하기](https://youtu.be/fpc7KnqFGrs?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&t=504)
- 객체를 함부로 바꾸지 마라! (불변성💫) => 👯‍♀️복사해라👯‍♀️ 
```js
pop, push, shift, unshift, splice //배열을 직접적으로 수정 => react에선 금지❌
concat, slice //새로운 배열을 만들어냄⭕
```
### 🟪 [1-6. 함수 컴포넌트(함수형아님)](https://youtu.be/Sph9Pqi1Mz0?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- class 에선  this 문제가 생김
- 함수형컴포넌트❌, 함수컴포넌트⭕ => **this 쓸 일이 없다!**
- *<span style="color:#000;background:#d9d9d9; font-weight:bold">&ensp;The Best Code is No Code At All...👥👤...👤👥...👤...👥👤...👤👥...👤&ensp;</span>*
- ✔ [react dev tools로 state 감 잡기](https://youtu.be/Sph9Pqi1Mz0?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&t=697)
```js
function LikeButton(){
    
    // 구조분해: 배열에 해당하는 것을 꺼내서 변수에 대입함
    const [liked, setLiked] = React.useState(false); 
    if(liked){
        return 'You liked this.'
    }

    //뭔짓을 하든 return한게 화면이다 ㅋ💣
    return(
        <button onClick={()=>{setLiked(true)}}>Like</button>
    )
}
```
### 🟫 [1-7. 구구단 리액트로 만들기 ~ 1-11. ref](https://youtu.be/XW6mw7yNFxQ?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- 과거로 돌아간 제로초...
```js
<script type="text/babel">
  class GuGuDan extends React.Component {
    //🧹constructor 지워도 됨, 실무에선 바로 state 선언만 쓰는 경우가 많음🧹
    //constructor(props){ 
        //super(props)
        state = {
        first: Math.ceil(Math.random() * 9),
        second: Math.ceil(Math.random() * 9),
        value: '',
        result: '',
        };
    //}


    ➡ this가 달라지기 때문에 무조건‼‼ 화살표함수 사용
    (직접 자기가 만든 함수 ㅇㅇ)

    onSubmit = (e) => {
      e.preventDefault();
      if (parseInt(this.state.value) === this.state.first * this.state.second) {
        
        ✔ 현재값과 이전값을 구분하기 위해서
        setState안에 함수로 return을 넣어주는 방법
        👍🏼[장점] prevState(예전값)을 다음 상태값에 활용할 수 있음 
        (예) counter 예제

        this.setState((prevState) => {
          return {

            result: '정답: ' + prevState.value,
            first: Math.ceil(Math.random() * 9),
            second: Math.ceil(Math.random() * 9),
            value: '',
          };
        });
        this.input.focus();
      } else {
        this.setState({
          result: '땡',
          value: '',
        });
        this.input.focus(); //DOM이 선택 됨
      }
    };

    onChange = (e) => {
      this.setState({ value: e.target.value });
    };

    input;

    onRefInput = (c) => { this.input = c; };

    ✔ render는 화살표 함수 사용할 필요없음, 써도된다
    ✔ render가 자주 실행되면 성능저하, 함수는 바깥으로 빼줘...
    render() {
      return (

        1. 👎🏼[react의 단점] 
            예전에는 div로 감싸줬어야 했음 => root안에 쓸데없는 div가 생성
        2. 👍🏼[개선점]
            빈태그로 감싸줌 <></>
            만약, 에러날 경우(바벨이 처리를 못할경우 )
            <React.Fragment></React.Fragment>

        <React.Fragment> 
          <div>{this.state.first} 곱하기 {this.state.second}는?</div>
          <form onSubmit={this.onSubmit}>
            <input ref={this.onRefInput} type="number" value={this.state.value} onChange={this.onChange}/>
            <button>입력!</button>
          </form>
          <div>{this.state.result}</div>
        </React.Fragment>
      );
    }
  }

</script>
<script type="text/babel">
  //✔ react 17버전  
  ReactDOM.render(<GuGuDan/>, document.querySelector('#root'));
</script>
```
* * *
## 2 Hooks 및 웹팩설치
### 🟥 [2-1. React Hooks 사용하기](https://youtu.be/EUQnxfZgFJU?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn) ~ [2-2. Class와 Hooks 비교하기](https://youtu.be/ZyOOdGBqZbk?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
```js
✔ 기존 class 구조
class GuGuDan = () =>{
...
}

✔ 함수형 구조
const GuGuDan = () => {
  return <div>Hello, Hooks</div>
}
```
1. setState나 Ref를 사용하지않는 컴포넌트는 함수형으로 만들었음
2. 함사모(👥함수를 사랑하는 모임👥)에서 함수에서도 setState나 Ref를 사용하고픔  
=> ❤react Hook 탄생❤  
```js
const GuGuDan = () => {
    
    ✔ state를 각각으로 분해 => 통으로 하나로 쓰면 state 할 때마다 귀찮아짐
    const [first, setFirst] = React.useState(Math.ceil(Math.random() * 9));
    const [second, setSecond] = React.useState(Math.ceil(Math.random() * 9));
    const [value, setValue] = React.useState('');
    const [result, setResult] = React.useState('');
    const inputEl = React.useRef(null); //걍외워

    const onSubmitForm = (e) => {
      e.preventDefault();
      if (parseInt(value) === first * second) {
        setResult('정답');
        setFirst(Math.ceil(Math.random() * 9));
        setSecond(Math.ceil(Math.random() * 9));
        setValue('');
        inputEl.current.focus(); //DOM에 접근, current 넣어줘야함 
      } else {
        setResult('땡');
        setValue('');
        inputEl.current.focus(); //DOM에 접근, current 넣어줘야함 
      }
    };
    return (
      <React.Fragment>
        <div>{first} 곱하기 {second}는?</div>
        <form onSubmit={onSubmitForm}>
          <input
            ref={inputEl}
            type="number"
            value={value}
            onChange={(e) => setValue(e.target.value)}
          />
          <button>입력!</button>
        </form>
        <div id="result">{result}</div>
      </React.Fragment>
    );
  };
```
- react 작성 시 주의할 점  
  class => className  
  for => htmlFor  

### 🟧 [2-2. 웹팩 설치하기](https://youtu.be/66_D4RYpFqY?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- 웹팩을 사용하는 이유?  
  facebook 컴포넌트 2만개 => 유지보수가 어려움  
  src로 script를 불러오기 => 코드 중복의 위험   
  **So, 웹팩을 사용함✨**
  
- 웹팩이란 ?   
여러 개의 js파일을 한방에 합쳐서 하나의 js파일로 만드는 것.  
하나로 합치면서 바벨도 적용할 수 있고 쓸데없는 코드들도 없앨 수 있음(예. console.log)

- node (= 자바스크립트 실행기)
```
npm i react react-dom
npm i -D webpack webpack-cli

설치하면 헤더에 작성했던거(react,바벨) 필요 없음  
왜냐? npm에서 불러오기 때문에..
```
```
create react app 

자동으로 만들어줌 
But,기본원리를 이해할 수 없음(비추)
```

### 🟨 [2-4. 모듈 시스템과 웹팩 설정](https://youtu.be/jQh5_jvZVzI?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn) ~ [2-7. @babel/preset-env와 plugins](https://youtu.be/LoMFC4kdrnQ?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
```js
✔ 쪼개었던 파일들을 필요에 따라 불러옴

const React = require('react');
const ReactDom = require('react-dom');
const WordRelay = require('./WordRelay');

ReactDom.render(<WordRelay />, document.querySelector('#root'))
```
```js
✔ webpack.config.js에서 파일을 합쳐줌

const path = require('path'); //경로 조작을 쉽게
resolve: {
  extensions: ['.js', '.jsx'], //확장자(알아서 웹팩이 찾아냄)
},
entry: { 
  app: './client', //확장자생략
}, //입력
output: {
  path: path.join(__dirname, 'dist'), //경로를 합쳐줌
}, //출력
.
.
.

```
- 참고사항 : [웹팩 사이트](https://webpack.js.org/concepts/)

### 🟩 [2-8. 끝말잇기 Class 만들기](https://youtu.be/KDJNjLZrqJk?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
```js
  render() {
    return (
      <>
        <div>{this.state.word}</div>
        <form onSubmit={this.onSubmitForm}>
          <input ref={this.onRefInput} value={this.state.value} onChange={this.onChangeInput} /> 
          <button>클릭!!!</button>
        </form>
        <div>{this.state.result}</div>
      </>
    );
  }

  ✔ onChage, value가 없으면 defaultValue를 넣어야 함
  ✔ 자동으로 빌드를 해주는 설정을 하지않는다면 런타임 오류가 남
  ✔ 수동으로 하면 매번 빌드를 해주기 귀찮음
```
### 🟦 [2-9. 웹팩 데브 서버와 핫 리로딩(2021년 버전 )](https://youtu.be/RCb0UF7Lu90?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- 미래에서 온 제로초
```js
1. 기존 웹팩 명령어
"scripts":{
  "dev" : "webpack serve --hot"
}

2. 바뀐 웹팩 명령어
"scripts":{
  "dev" : "webpack serve --env development"
}

3. 리프레쉬 웹팩 플러그인 추가 작성 +상단에도
pligins : [
  new RefreshWebpackPlugin();
]

4. front개발 편의를 위한 devsercer 작성
- dist폴더에 결과물을 저장해줌
- 변경점✨을 감지함

```

- 더 미래에서 온 제로초(2021.ver)
```js
1. devServer이 바뀜
- 웹팩이 빌드한 dist폴더 =>express.static과 비슷함(node강좌에서 다룸)
- 실제로 존재하는 파일들
```
- 실무에서 웹팩을 사용하니, 에러찾기도 좋고 페이지가 자동으로 바뀜👍🏼
### 🟪 [2-10. 끝말잇기 Hooks로 전환하기](https://youtu.be/Zb70S1I6u6U?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&t=2)
- class를 hooks로 전환
- 확연히 짧아진 코드
```js
const React = require('react');
const { useState } = React;

const WordRelay = () => {
  const [word, setWord] = useState('제로초'); //초기값은 '제로초' 
  const [value, setValue] = useState('');
  const [result, setResult] = useState('');
  const inputEl = React.useRef(null);

  const onSubmitForm = (e) => { //class가 아니기때문에 변수로 선언! 
    e.preventDefault();

    //✔ hooks를 쓰게되면 this, this.state를 사용하지않음
    if (word[word.length - 1] === value[0]) {
      setResult('딩동댕');
      setWord(value);
      setValue('');
      inputEl.current.focus(); //ref는 current붙여줘야함
    } else {
      setResult('땡');
      setValue('');
      inputEl.current.focus();
    }
  };

  return (
    <>
      <div>{word}</div>
      <form onSubmit={onSubmitForm}>
        <input
          ref={inputEl} value={value} onChange={(e) => setValue(e.currentTarget.value)}
        />
        <button>입력!</button>
      </form>
      <div>{result}</div>
    </>
  );
};

module.exports = WordRelay;
```
- console창에서 [HMR]은 웹팩데브서버임
- 어떤 컴포넌트가 바뀌어서 업데이트 해주는지 알려줌
- 나중에 웹이 복잡해지면 console창도 복잡해짐, 그래도 보는 버릇들면 나중에 좋음
- className, htmlFor 사용하는거 잊쥐마..

### 🟫 [2-11. 컨트롤드 인풋 vs 언컨트롤드 인풋](https://youtu.be/wSs1xa8CPQI?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- 미래에서 온 제로초

- controlled input  
(1) value와 onchage 존재  
(2) 더 권장함👍🏼

- uncontrolled input  
(1) value와 onchage 존재하지 않음  
(2) 원시적인 html형태  
(3) 앱이 간단하면 사용가능 = onsubmit에서만 특정동작을 하는 경우
* * *
## 3 React에서 사용하는 함수와 숫자야구
### 🟥 [3-1. import vs require!](https://youtu.be/3X4J2L_PhiY?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- require는 node의 모듈시스템, 다른파일에서 불러올수있음
- export는 변수, 함수, 클래스 앞에 export 키워드를 붙여서 모듈의 기능을 외부에서 사용할 수 있도록 내보냄
- import는 export로 내보낸 모듈을 가져오는 기능을 담당
- 웹팩에서는 노드가 돌리는거라서 import 쓰면 에러남. const사용해야함
- 다른곳에서는 바벨이 바꿔주기때문에 import 사용해도 됨
### 🟧 [3-2. 리액트 반복문(map)](https://youtu.be/OO5gXdPR6HI?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- 숫자야구  
```js
1. 숫자 4개를 뽑기   
   function get Numbers()  
   <input maxLength={4}/>  

2. 10번안에 맞추기  => 사용자가 시도함으로 계속 변화함  
  {this.state.tries.length}

3. 시도하는 것을 배열로 보이기위해 반복문 사용
  {['a','b','c','d','e','f']}.map((v)=>{
    return <li>v</li>
  })
```
### 🟨 [3-3. 리액트 반복문(key)](https://youtu.be/A-ydulnj8lk?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&t=2)
```js
1. 이중배열 반복문 예제
  {[['a - good'],['b - good'],['c - bad'],['d - bad'],['e - good'],['f - good']]}.map((v)=>{ 
    return <li><b>{v[0]}</b> - {v[1]}</li>
  })

2. 이차원 배열 반복문 예제
  {[
    {'name: a, feel: good'},
    {'name: b, feel: good'},
    {'name: c, feel: bad'},
    {'name: d, feel: bad'},
    {'name: e, feel: good'},
    {'name: f, feel: good'}  
  ]}.map((v)=>
    <li><b>{v.name}</b> - {v.feel}</li> //return 생략
  )

  => 가독성 bad 👎🏼 그래서 Props👍🏼✨ 사용


3. Key
- key는 화면에 표시되진않지만 리액트 성능최적화(key로 바뀐걸 판단)에 사용
- key는 중복x 고유o!!!
- 예) key = {v.name + v.feel}

```
### 🟩 [3-4. 컴포넌트 분리와 props](https://youtu.be/6YZhSvRqddw?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&t=1)
- 컴포넌트 분리하기   
- 👍🏼 컴포넌트 분리의 이점  
  (1) 간결함 굿~  
  (2) 재사용성 굿~  
  (3) 불러오면 바로 v,i를 사용할수없기 때문에 value={v} index={i}로 작성
```js
{this.name.map((v,i)=>{
  return(
    </Try value={v} index={i}> 
  );
})}
```

- ```</Try>```를 불러오는 곳
```js
import React, {Component} from 'react';

class Try extends Component{
  render(){
    return(
      <li><b>{this.props.value.name}</b> - {this.props.index.feel}</li>
    )
  }
}

export default Try;
```
### 🟦 [3-5. 주석과 메서드 바인딩](https://youtu.be/Cu4-aOsagOA?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn) ~  [3-7. 강좌 Q&A](https://youtu.be/AaQ0Mo8a-BU?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- 주석처리 ``{/* */}`` 한번더 감싸줘야함
- key없으면 에러남
```js
{this.name.map((v,i)=>{
  return(
    </Try value={v} index={i} key = {v.name + v.feel}> 
  );
})}

- props의 상속이 너무 많아지면 컨텍스트랑 리덕스를 사용함
- 리덕스는 은행이라고 생각해(유산을 자식한테 나눠주는걸 관리 ㅋㅋ)
```

```js
onSubmitForm() = > {}
```
- 내가 만든 함수를 화살표 함수를 안쓰면? 에러남❌  
  그래도 쓰고 싶으면 constructor을 사용해야함..
- 리액트가 방식이 다양해서 헷갈릴 위험성이 높음😫
### 🟪 [3-6. 숫자야구 만들기](https://youtu.be/vvJVwekTbaw?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&t=1)
```js
  /*
    ❔ 언제 함수를 바깥으로 빼도 되는지? this를 안쓰면!😎
    안에 넣어도 무방하나... 함수를 재활용✨하는 경우도 있기때문에 ! 
  */
  function getNumbers() { 
    /*...(생략)*/
  }

  onSubmitForm = (e) => {
    const { value, tries, answer } = this.state;
    e.preventDefault();
    if (value === answer.join('')) {
      this.setState((prevState) => {
        return {
          result: '홈런!', //맞춘경우

          /*
          [ 기존 배열에 값을 넣어줌 push❌를 쓰면 안됨!! ]
          이유: 리액트가 뭐가 바뀐건지 감지를 못함😫
          So, 기존배열을 복사하고 새로운 배열을 만들어 => 감지 가능⭕
          */
          tries: [...prevState.tries, { try: value, result: '홈런!' }], 
        }
      });
      alert('게임을 다시 시작합니다!');
      this.setState({
        value: '',
        answer: getNumbers(),
        tries: [],
      });
      this.inputRef.current.focus();
    } else { /*...(생략)*/
  };

  /*...(생략)*/
  render()에서는 props로 넘겨주면 객체로 받아
    {tries.map((v, i) => {
      return (
        <Try key={`${i + 1}차 시도 :`} tryInfo={v} /> 
      );
    })}
}
```
### 🟫 [3-8. 숫자야구 Hooks로 전환하기(+useState lazy init)](https://youtu.be/HYpapSlFlCc?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&t=5)
```js
  //빼두면 Hooks로 바꿀때 독립적이기때문에 영향을 받지않아
  function getNumbers() { 
    /*...(생략)*/
  }
const NumberBaseball = () => {
  ❌const [answer, setAnswer] = useState(getNumbers()); //리렌더링될때마다 실행❌
  ⭕const [answer, setAnswer] = useState(getNumbers); //처음한번만 적용⭕ 
  //=> lazy init(늦은초기화: 함수가 실행될때동안 리액트가 기다려줘)
  const [value, setValue] = useState('');
  const [result, setResult] = useState('');
  const [tries, setTries] = useState([]);
  const inputEl = useRef(null);
  /*...(생략)*/
};

```
### ⬛ [3-9. React Devtools](https://youtu.be/d_aytX00fqc?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- [React Devtools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=ko) 설치
- 예시사이트 : 다방, 페이스북
- 개발모드일 경우 상단 버튼이 빨갛게 뜸
- devTools로 보면 컴포넌트가 표시됨
- 변화가 보이기때문에 최적화된 코드를 짤 수 있음
### ⬜ [3-10. ]()
### 🔳 [3-11.]()
### 🔲 [3-12.]()
### 🟥 [3-13.]()
***
## 4
### 🟥 [4-1.]()
### 🟧 [4-2. ]()
### 🟨 [4-3. ]()
### 🟩 [4-4. ]()
### 🟦 [4-5. ]()
### 🟪 [4-6. ]()
### 🟫 [4-7. ]()
### ⬛ [4-8. ]()
### ⬜ [4-9. ]()
### 🔳 [4-10.]()
### 🔲 [4-11.]()
***
## 5
### 🟥 [5-1.]()
### 🟧 [5-2. ]()
### 🟨 [5-3. ]()
### 🟩 [5-4. ]()
### 🟦 [5-5. ]()
### 🟪 [5-6. ]()
### 🟫 [5-7. ]()
### ⬛ [5-8. ]()
### ⬜ [5-9. ]()
### 🔳 [5-10.]()
### 🔲 [5-11.]()
***
## 6
### 🟥 [6-1.]()
### 🟧 [6-2. ]()
### 🟨 [6-3. ]()
### 🟩 [6-4. ]()
### 🟦 [6-5. ]()
### 🟪 [6-6. ]()
### 🟫 [6-7. ]()
### ⬛ [6-8. ]()
### ⬜ [6-9. ]()
### 🔳 [6-10.]()
### 🔲 [6-11.]()
***
## 7
### 🟥 [7-1.]()
### 🟧 [7-2. ]()
### 🟨 [7-3. ]()
### 🟩 [7-4. ]()
### 🟦 [7-5. ]()
### 🟪 [7-6. ]()
### 🟫 [7-7. ]()
### ⬛ [7-8. ]()
### ⬜ [7-9. ]()
### 🔳 [7-10.]()
### 🔲 [7-11.]()
***
## 8
### 🟥 [8-1.]()
### 🟧 [8-2. ]()
### 🟨 [8-3. ]()
### 🟩 [8-4. ]()
### 🟦 [8-5. ]()
### 🟪 [8-6. ]()
### 🟫 [8-7. ]()
### ⬛ [8-8. ]()
### ⬜ [8-9. ]()
### 🔳 [8-10.]()
### 🔲 [8-11.]()
***
## 9
### 🟥 [9-1.]()
### 🟧 [9-2. ]()
### 🟨 [9-3. ]()
### 🟩 [9-4. ]()
### 🟦 [9-5. ]()
### 🟪 [9-6. ]()
### 🟫 [9-7. ]()
### ⬛ [9-8. ]()
### ⬜ [9-9. ]()
### 🔳 [9-10.]()
### 🔲 [9-11.]()
***

## 10 개인 추가 공부
## 1 React Hooks에 취한다
### 🟥 [1-1. useState 15분만에 마스터하기](https://youtu.be/G3qglTF-fFI?list=PLZ5oZ2KmQEYjwhSxjB_74PoU6pmFzgVMO)  

#### Hooks란? 
- 함수형 컴포넌트를 class형 컴포넌트의 기능을 사용할 수 있도록 해주는 기능
- 함수형 컴포넌트는 리렌더링 할때 무조건 새롭게 선언, 초기화, 메모리 할당을 함(stateless)
- class형 컴포넌트는 state, life cycle로 상태관리가 용이함
- 공식문서에서는 함수형 컴포넌트를 권장하는 추세
#### Hooks 규칙
1. 웬만하면 최상위에서만 호출(반복, 조건, 중첩문에서 호출할순없음)  
  단, 반복문안에 useState는 가능.(순서가 확실할 경우)
2. Hooks를 만들땐 앞에 'use'를 붙이기
3. React는 Hooks 호출되는 순서에 의존함
4.  Hooks안에 Hooks 선언 금지
***
#### useState
- = 동적상태관리
```js
function Forem(){
    const[name, setName] =  useState('Maby');
          변수, 함수                  초기값
}
```


### 🟧 [1-2. useEffect 깔끔하게 마스터하기](https://youtu.be/kyodvzc5GHU?list=PLZ5oZ2KmQEYjwhSxjB_74PoU6pmFzgVMO)
#### useEffect
- = sideEffect를 수행
- (생명주기함수: mount/update/unmount)
-  class에서 componetDidMount/componetDidUpdate/componetWillUnmount
```js
useEffect(function persistForm(){
    localStorage.setItem('formData', name);
});


1. }) 일 경우, 공란인 경우 => 렌더링될때마다 실행
1. }[]) 일 경우, = 의존성배열이 없는 경우 => 초기에만 렌더링
1. }[aa]) 일 경우, = 의존성배열이 있는 경우 => 배열이 실행될때만 렌더링
```

```js
useEffect(()=>{
    ...
    return()=>{

    }
}[])

✔ 여기서, return부분은 컴포넌트가 언마운트될 때 호출
- clean up
- componetWillUnmount
```
### 🟨 [1-3. useRef 완벽 정리 1# 변수 관리](https://youtu.be/VxqZrL4FLz8?list=PLZ5oZ2KmQEYjwhSxjB_74PoU6pmFzgVMO)
#### useRef
1. 저장공간으로 사용
    state의 경우, 렌더링시 내부변수들을 모두 초기화 시킴  
    ref의 경우 변수값을 유지하되, 렌더를 발생시키지 않음(변화는 감지함)
2. DOM에 접근
    (예) 아이디 작성 input에 사용자가 직접 focus하지 않아도 렌더시 focus()되어있게 하는 예제

```js
```
### 🟩 [1-4. useRef 완벽 정리 2# DOM 요소 접근](https://youtu.be/EMK8oUUwP5Q?list=PLZ5oZ2KmQEYjwhSxjB_74PoU6pmFzgVMO)
### 🟦 [1-5. useContext + Context API ](https://youtu.be/LwvXVEHS638?list=PLZ5oZ2KmQEYjwhSxjB_74PoU6pmFzgVMO)
### 🟪 [1-6. useMemo 제대로 사용하기](https://youtu.be/e-CnI8Q5RY4?list=PLZ5oZ2KmQEYjwhSxjB_74PoU6pmFzgVMO)
#### useMemo
- 컴포넌트 최적화🧹
- 함수의 리턴값을 메모리에 기억하여 값을 재사용한다.
- 무분별한 사용은 성능을 악화시킴
```js
const value = useMemo(()=>{
    return calculate() //useMemo가 리턴해주는 값
}[item])
```
### 🟫 [1-7. useCallback 짱 쉬운 강의](https://youtu.be/XfUF9qLa3mU?list=PLZ5oZ2KmQEYjwhSxjB_74PoU6pmFzgVMO)
#### useCallback
- 컴포넌트 최적화🧹
- 컴포넌트가 렌더링 될때 특정함수를 재사용해서 재렌더링 방지
- 자식컴포넌ㅌ츠에 props로 매번 함수전달할수 없기때문에 useCallback을 꼭 사용해야함
```js
const onSave = useCallback(()=>{
    console.log(name)
}[])

[]이 공란인 배열이면 렌더링될때마다 초기값을 0으로 받아오기때문에 
꼭! 재생성할 기준을 할당해야함
```
### ⬛ [1-8. useReducer 확실히 정리해드려요](https://youtu.be/tdORpiegLg0?list=PLZ5oZ2KmQEYjwhSxjB_74PoU6pmFzgVMO)
### ⬜ [1-9. React.memo로 컴포넌트 최적화하기 (ft. useMemo, useCallback)](https://youtu.be/oqUgcxwrnSY?list=PLZ5oZ2KmQEYjwhSxjB_74PoU6pmFzgVMO)
### 🔳 [1-10. Custom Hooks 커스텀 훅](https://youtu.be/S6POUU2-tr8?list=PLZ5oZ2KmQEYjwhSxjB_74PoU6pmFzgVMO)


