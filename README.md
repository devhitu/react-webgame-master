# [리액트 무료 강좌(웹게임)🤖🎳]
> #### 출처: [리액트 무료 강좌(웹게임)_ZeroChoTV](https://www.youtube.com/playlist?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)  
***

## 목차
[1 React Class](#1-React-Class)  
[2 Hooks 및 웹팩설치](#2-Hooks-및-웹팩설치)  
[3 React에서 사용하는 함수와 숫자야구](#3-React에서-사용하는-함수와-숫자야구)  
[4 반응속도와 성능체크](#4-반응속도와-성능체크)  
[5 라이프사이클과 가위바위보 게임](#5-라이프사이클과-가위바위보-게임)  
[6 로또 추첨기와 Hooks 활용](#6-로또-추첨기와-Hooks-활용)  
[7 틱택토와 reducer](#7-틱택토와-reducer)  
[8 Context API](#8-Context-API)  
[9 Router와 useLayoutEffect](#9-Router와-useLayoutEffect)  
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
  function getNumbrs() { 
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
### ⬜ [3-10. shouldComponentUpdate](https://youtu.be/dFbdTkgaLNs?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- React Devtools를 쓰면 state나 props가 바뀌었을때(=렌더될때) highlight기능이 반짝거림
- 렌더가 많이 일어나면 highlight가 붉은색
- 렌더가 안일어나도 되는곳이 렌더되면 성능에 문제가 발생하기 시작함😫
```js
setState가 ㄱㅖ속 호출될때...
리액트는 ㅂr보라서 바뀌는 걸 알려줘야함....✨

shouldComponentUpdate(nextProps, nextState, nextContext){
  if(this.state.counter !== nextState.counter){
    return true
  }
  return false
}
```
### 🔳 [3-11. 억울한 자식 리렌더링 막기(PureComponent와 memo)](https://youtu.be/MHYbt8v1X3U?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&t=1)
1. PureComponent 
  (1) shouldComponentUpdate가 복잡하면 PureComponent로 바꾼다  
  (2) PureComponent는 shouldComponentUpdate의 T/F를 알아서 판단함✨  
  (3) BUT. 복잡한 구조일경우 판단이 어려움😫  
  (4) PureComponent가 잘 알아차릴 수 있게 간결하게 작성  
  (5) 레퍼런스 주소만을 비교하여 비교(얕은비교, 바로 state 수정 불가❌)

2. 미래에서 온 제로초 - memo  
  (1) "함수형 컴포넌트"에서 PureComponent의 기능과 같이 수행.  

* [참고페이지](https://velog.io/@kihyeon8949/React-PureComponent-memo-React-%EC%84%B1%EB%8A%A5%EA%B0%9C%EC%84%A0)
### 🔲 [3-12. React.createRef](https://youtu.be/qE02-oSDPlg?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
```js
1. class의 ref를 hooks의 ref처럼 만들기

inputRef = createRef;를 넣어서
this.current.inputRef;로 씀

=> 통일성을 줌 👍🏼
```
### 🟥 [3-13. props와 state 연결하기](https://youtu.be/siiFLSey834?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- reder안에 this.setState실행하면 무한반복....절대 쓰지마❌

```js
1. props  
  
  (1) props는 자식(Try.jsx)이 직접 값을 바꾸면 안됨, 부모(``<Try/>``)가 바꿔야함 

  (2) 근데 바꿔야한다? 그럼 자식 파일에서 state로 바꾼다...  
  state = {
    result: this.props.result,
    try: this.props.try,
  }
  render(){
    const { tryInfo } = this.props;
    return(
      ...
    )
  }

2. constructor
  (1) 정밀한 동작이 필요할때...

3. A -> B -> C -> D ...
  (1) 받아오려면 쓸데없이 렌더될수있음
  (2) A에서D를 바로 전달해주는거 => 리덕스, 컨텍스트(?)
```
***
## 4 반응속도와 성능체크
### 🟥 [4-1. React 조건문](https://youtu.be/RPz-JKCfnIs?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- 반응속도 체크
- 초록색이되면 클릭하는 게임💚
- 리액트에서 조건문 : 삼항연산자(보이고 안보이고 할때) 지저분하긴함..
### 🟧 [4-2. setTimeout 넣어 반응속도체크](https://youtu.be/9bo3fG7brCs?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)

```js
  //렌더링을 일으키고 싶지 않은 애들
  timeout; //setTimeout 초기화 시켜줘야함.=> clearTimeout
  startTime; 
  endTime; 

  onClickScreen = () => {
    const { state } = this.state;
    if (state === 'waiting') {
      timeout.current = setTimeout(() => {
        this.setState({
          state: 'now',
          message: '지금 클릭',
        });
        this.startTime = new Date();
      }, Math.floor(Math.random() * 1000) + 2000); // 랜덤
      this.setState({
        state: 'ready',
        message: '초록색이 되면 클릭하세요.',
      });
    } else if (state === 'ready') { // 성급하게 클릭
      clearTimeout(this.timeout); 
      this.setState({
        state: 'waiting',
        message: '너무 성급하시군요! 초록색이 된 후에 클릭하세요.',
      });
    } else if (state === 'now') { // 반응속도 체크
      endTime.current = new Date();
      this.setState((prevState) => {
        return {
          state: 'waiting',
          message: '클릭해서 시작하세요.',
          result: [...prevState.result, this.endTime - this.startTime], // 시간차
        };
      });
    }
  };
```
### 🟨 [4-3. 성능 체크와 Q&A](https://youtu.be/mw3HN6QOn3U?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- reset버튼 만들기
```js
  onReset = () => {
    this.setState({
      result: [],
    });
  };

  renderAverage = () => {
    const {result} = this.state;
    return result.length === 0
      ? null //아무것두 없서..
      : <>
        <div>평균 시간: {result.reduce((a, c) => a + c) / result.length}ms</div>
        <button onClick={this.onReset}>리셋</button>
      </>
  };
```
- 리셋시 불필요한 렌더링이 일어남  
  => result가 바뀌는거랑 ``renderAverage`` 가 계산되는게 합쳐있는데, 이걸 분리해야함(최적화)
```js
  render() {
    const { state, message } = this.state;
    return (
      <>
        <div
          id="screen"
          className={state}
          onClick={this.onClickScreen}
        >
          {message}
        </div>
        {this.renderAverage()}
      </>
    )
  }
```
### 🟩 [4-4. 반응속도체크 Hooks로 전환하기](https://youtu.be/deS_DJzT1no?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
```js
  const timeout = useRef(null);
  const startTime = useRef(0);
  const endTime = useRef(0);

  😏 ref는 접근시 current로 접근하는것! 실수하지말것~
```
  - class에서는 this의 속성들을 적어줬는데 hooks로 표현할때는 ref를 사용  
  ✨ ref는 DOM에 접근할때, this의 속성들을 표현할때 사용한다.   

  - state와 ref의 차이  
  1. state는 return이 다시 실행⭕  
  2. ref는 다시실행되지 않음. 불필요한 렌더링을 막는다.❌  
  => 화면은 바뀌는데, 값은 안바뀌는것들

### 🟦 [4-5. return 내부에 for과 if 쓰기](https://youtu.be/FX6uO1GkXsc?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
```js
1. if문 
{(()=>{ //즉시실행함수
  if(...){
    ...
  }else{
    ...
  }
})()}


2. for문 
{(()=>{ //즉시실행함수
  for(...){
    ...
  }
})()}
```
- for과 if 사용하면 코드가 지저분해짐
- 이걸 하느니 바깥으로 함수를 빼서 인라인으로 쓰는게 깔끔함
- 제일 좋은건 자식컴포넌트로 만드는것

```js
return [
  <div key="사과">사과</div>
]
```
- jsx에서 [] 배열을 받아오는경우
- key를 적어줘야함
- 잘 안씀
***
## 5 라이프사이클과 가위바위보 게임
### 🟥 [5-1. 리액트 라이프사이클 소개](https://youtu.be/ltw4FYagLfM?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
```js
componentDidMount(){
}
componentWillUnMount(){
  //컴포넌트 제거되기 직전
}
componentDidUpdate(){
  //컴포넌트 리렌더링
}
shouldComponentUpdate(){
  return true //렌더링 할지 판단
}
```
### 🟧 [5-2. setInterval과 라이프사이클 연동하기](https://youtu.be/5aFCwolam4k?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&t=7)
- 비동기 요청
```js
interval;

componentDidMount(){
  this.interval.setInterval(()=>{
    //리액트는 ㅂr보라서 화면에 사라져도 계속 됨
    //메모리 먹음...🍔
  })  
}

componentWillUnMount(){
  clearInterval(this.interval); //취소해줘야함
}


✔조심 ‼비동기함수가 바깥에 있는 변수를 참조하면 클로저 발생!‼
```
### 🟨 [5-3. 가위바위보 게임 만들기](https://youtu.be/F8eqh1Y4n3k?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
```js
  interval;

  componentDidMount() { 
    this.interval = setInterval(this.changeHand, 100);
  }

  changeHand = () => {
    ...
  };
```
- clearInterval로 멈춘 걸 다시 복구하기
- 그럼 코드가 중복되기 때문에 밖으로 뺀다
### 🟩 [5-4. 고차 함수와 Q&A](https://youtu.be/BdKBcRJInP4?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
```js
✔ 매서드안에 함수를 호출하는 경우  
<button id="rock" className="btn" onClick={() = >this.onClickBtn('바위')}>바위</button>

1. ()=> 화살표를 지운다.
<button id="rock" className="btn" onClick={this.onClickBtn('바위')}>바위</button>

2. ✨여기에 화살표를 넣어줌!
onClickBtn = (choice) => () => {
  ...
};
```
### 🟦 [5-5. Hooks와 useEffect](https://youtu.be/2DFXAcck-DQ?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
```js
✔ ✨ componentDidMount, componentDidUpdate 역할
- 1대1 대응은 아님, BUT 비슷한 역할

  useEffect(() => { 
    interval.current = setInterval(changeHand, 100); 
    return () => { // componentWillUnmount 역할
      clearInterval(interval.current);
    }
  }, [imgCoord]); //의존성배열 = 함수 시작 기준
```

### 🟫 [5-6. 클래스와 Hooks 라이프사이클 비교](https://youtu.be/aUXwUqgYREI?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- useLayoutEffect : 화면 늘렸다 줄였다 할때(바뀔 때) 사용  
  잘 사용하진않음
- useEffect : 화면이 바뀌고 난 후 실행

```js
                      | result, imgCoord, score
-----------------------------------------------
componentDidMount     |
componentDidUpdate    |
componentWillUnmount  |

//한번에
componentDidMount() {
  this.setState({
    imgCoord: 3,
    score: 1,
    result: 2,
  })
}

//두번써서
useEffect(() => {
  setImgCoord();
  setScore();
}, [imgCoord, score]);

useEffect(() => {
  setResult();
}, [result]);

👀 class는 가로로 볼 것(모두 담당)
👀 Hooks는 세로로 볼 것(하나만 담당, 물론 useEffect도 다 담당할수있지만 class와 차이점임)
```
### 🟪 [5-7. 커스텀훅으로 우아하게 interval하기](https://youtu.be/gtDT26Htn44?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- 기존의 ref, useEffect, setInterval, clearInterval를 가독성있게 변경 ?  
  => customHook : 직접 훅을 만드는것, 재사용성 good  
  => devTools에서 확인 가능
- setInterval, clearInterval사용시 callback을 받으면 딜레이가 됨, 지양❌
- ref(= 항상최신객체 참조)를 사용해 최신 callback을 받아옴 지향⭕
***
## 6 로또 추첨기와 Hooks 활용
### 🟥 [6-1. 로또 추첨기 컴포넌트](https://youtu.be/oKPtGBEtR3k?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- 로또 당첨숫자 7개를 미리 뽑는것,  
   대부분의 게임들이 미리 수를 뽑아놓아 준비를 해놓고 실행
```js
✔ 로또 1번 실행후 재실행하는 state => "한번더 해볼래?" 버튼
class Lotto extends Component { ... redo : false ...}

-----------------------------------------------------------------------
✔ 반복문을 기점으로 컴포넌트 분리, 
반복문이 props로 값을 전달하는 좋은 기점이 되기때문

<div id="결과창">
    {winBalls.map((v) => <Ball key={v} number={v} />)}
</div>


-----------------------------------------------------------------------
✔ 해당코드는 Hooks가 아님! 
✔ state를 쓰지 않는 애들은 그냥 함수컴포넌트로 실행
✔ 자식컴포넌트에는 memo를 넣어줘야 불필요한 렌더링을 막을수있음

const Ball = memo(({ number }) => {
  let background;
  if (number <= 10) {
    background = 'red'; 
  ...
  } else {
    background = 'green';
  }
  return (
    <div className="ball" style={{ background }}>{number}</div>
  )
});

export default Ball;
-----------------------------------------------------------------------

👀 단, pureComponent 사용하고싶다면
memo로 감싸주기 => 이를 '하이 오더 컴포넌트(고차컴포넌트, HOC)'라고함

import React, {memo} from 'react';
const Ball =  memo({number}) => { ... }
```
### 🟧 [6-2. setTimeout 여러 번 사용하기](https://youtu.be/fWYFW6shsrs?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
```js
componentDidMount() { // 시작하자 마자 생성
  1. 비동기에 변수쓰면 클로저 문제 발생하나, ✨let을 사용하면 해결할수있음.(es6)
  2. 공 6개 순서대로 1초마다 넣어주기 (보너스 공은 6개 후 출력)

  this.runTimeouts(); 
}

componentWillUnmount() { //종료
  1. clear안해주면 메모리 상에서 계속 실행되기때문에 this.state에서 에러가 남😫
    => 브라우저가 껐다 생각하지 말구 부모컴포넌트가 날 없앴다라고 생각
  2. setTimeout, setInterval은 항상! componentWillInmount✨에서 관리해줘야함
  3. componentWilReceiceProps,componentDidcatch등등은 사용❌ 사라질꼬야.. 

  this.timeouts.forEach((v) => {
    clearTimeout(v); 
  });
}
```
### 🟨 [6-3. componentDidUpdate](https://youtu.be/D2OWLw3KZRQ?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn) 
```js
componentDidUpdate(prevProps, prevState) { // update시 실행 

  //👀 redo를 눌렀을때만 동작하도록 ! 
  if (this.state.winBalls.length === 0) {     
    this.runTimeouts(); //함수 중복되는경우는 바깥으로 빼기
  }
}

onClickRedo = () => {
  //처음 state로 초기화 하기
  this.setState({
    winNumbers: getWinNumbers(), // 당첨 숫자들
    winBalls: [],
    bonus: null, // 보너스 공
    redo: false,
  });
  this.timeouts = [];
};

```
### 🟩 [6-4. useEffect로 업데이트 감지하기](https://youtu.be/qdaZaC0AWq0?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&t=1) ~ [6-5. useMemo와 useCallback](https://youtu.be/6H6KncvVc8s?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- Hooks로 바꿔보기
```js

const Lotto = () => {
  ❌const [winNumbers, setWinNumbers] = useState(getWinNumbers()); 
  => getWinNumbers가 계속 실행

  - ✨useMemo ?
  1. 로또숫자를 잠깐 기억할수있게 useMemo(함수실행한 결과값 저장)를 사용함
  2. 두번째 인자[]가 바뀌진않는한 다시 실행되진 않음
  const lottoNumbers = useMemo(() => getWinNumbers(), []);

  ✔ 리액트가 기억한 ✨lottoNumbers를 넣어줌
  const [winNumbers, setWinNumbers] = useState(lottoNumbers);
  ...

----------------------------------------------------------------------

  useEffect(() => {
    ...
  }, [timeouts.current]); 

  1. winBalls.length === 0이면 초기 렌더되고 실행되어서 2번 실행되기때문에 수정
  2. 빈 배열이면 componentDidMount와 동일
  3. 배열에 요소가 있으면 componentDidMount랑 componentDidUpdate 둘 다 수행
  4. 필수로 적용해야하는 경우
    => 자식컴포넌트에 props로 함수를 넘길때는 꼭‼ useCallback을 사용해야함😎
    => 부모가 새로 함수를 주네?👨🏼‍🦳 하고 매번 리렌더할수있음...그래서 꼭 기억하게 해야함
----------------------------------------------------------------------
  const onClickRedo = useCallback(() => {
    console.log('onClickRedo');
    console.log(winNumbers);
    setWinNumbers(getWinNumbers());
    setWinBalls([]);
    setBonus(null);
    setRedo(false);
    timeouts.current = [];
  }, [winNumbers]);
  
  - ✨useCallback ?
  1. 함수컴포넌트가 재실행되어도 onClickRedo는 재실행되지 않아!
  2. 함수자체의 비용이 클 경우 사용
  3. 모든 것에 ✨useCallback사용하는게 좋을까? => NO!
    => 값을 기억📃하기 때문에 업뎃할때 [의존성배열]에 바뀌는 값을 꼭 넣어줘야함👀

```
### 🟦 [6-6. Hooks에대한 자잘한 팁들](https://youtu.be/IuAcxCce_bY?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- Hooks 시리즈는 순서가 중요해서 바뀌면 안된다.(조건문안에 넣지마라)  
  ㄴ 1-> 2 -> 3 이었던게 중간에 false조건이 되어 1->3이 되면 순서가 달라져서 안됨 
- 다른 Hooks안에 넣지마라
- 반복문안에는 넣어줘도 됨(단, 순서가 확실히 정해진 Hooks일 경우)
***
## 7 틱택토와 reducer
### 🟥 [7-1. 틱택토와 useReducer 소개]()
### 🟧 [7-2. reducer, action, dispatch의 관계]()
### 🟨 [7-3. action 만들어 dispatch하기]()
### 🟩 [7-4. 틱택토 구현하기]()
### 🟦 [7-5. 테이블 최적화 하기]()
***
## 8 Context API
### 🟥 [8-1. Context API 소개와 지뢰찾기]()
### 🟧 [8-2. createContext와 Provider]()
### 🟨 [8-3. useContext 사용해 지뢰 칸 렌]()
### 🟩 [8-4. 왼쪽 오른쪽 클릭 로직 작성하기]()
### 🟦 [8-5. 지뢰 개수 표시하기]()
### 🟪 [8-6. 빈 칸들 한번에 열기]()
### 🟫 [8-7. 승리 조건 체크와 타이머]()
### ⬛ [8-8. Context API 최적화]()
***
## 9 Router와 useLayoutEffect
### 🟥 [9-1. React Router 도입하기]()
### 🟧 [9-2. Link와 브라우저라우터(BrowserRouter)]()
### 🟨 [9-3. 해시라우터, params, withRouter]()
### 🟩 [9-4. location, match, history]()
### 🟦 [9-5. 쿼리스티링과 URL SearchParams]()
### 🟪 [9-6. render props, swith, exact]()
### 🟫 [리액트 라우터6(feat.REMIX)+라이브러리 버전 업그레이드]()
### ⬛ [언젠가는 써먹을 useLayoutEffect]()
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
- 자식컴포넌트에 props로 매번 함수전달할수 없기때문에 useCallback을 꼭 사용해야함
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


