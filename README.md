# [리액트 무료 강좌(웹게임)🤖🎳]
> #### 출처: [리액트 무료 강좌(웹게임)_ZeroChoTV](https://www.youtube.com/playlist?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)  
***

## 목차
[1 React Class](#1-React-Class)  
[2 Hooks 및 웹팩설치](#2-Hooks-및-웹팩설치)
[3 ](#3-)  
[4 ](#4-)  
[5 ](#5-)  
[6 ](#6-)  
[7 ](#7-)  
[8 ](#8-)  
[9 ](#9-)  
[10 추가](#10-추가)  
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
### 🟫 [1-7. 구구단 리액트로 만들기](https://youtu.be/XW6mw7yNFxQ?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
### ⬛ [1-8. 클래스 메서드](https://youtu.be/cmuQAQ87vvo?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
### ⬜ [1-9. Fragment와 기타 팁들](https://youtu.be/BEZ4l474rxQ?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&t=1)
### 🔳 [1-10. 함수형 setState](https://youtu.be/6WXnpf1HA_E?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&t=1)
### 🔲 [1-11. ref](https://youtu.be/nsS5mbyDDBw?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
- 과거로 돌아간 제로초...
```js
<script type="text/babel">
  class GuGuDan extends React.Component {
    constructor(props){
        super(props)
        state = {
        first: Math.ceil(Math.random() * 9),
        second: Math.ceil(Math.random() * 9),
        value: '',
        result: '',
        };
    }

    onSubmit = (e) => {
      e.preventDefault();
      if (parseInt(this.state.value) === this.state.first * this.state.second) {
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
        this.input.focus();
      }
    };

    onChange = (e) => {
      this.setState({ value: e.target.value });
    };

    input;

    onRefInput = (c) => { this.input = c; };

    // 컨텐츠
    render() {
      return (
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
### 🟥 [2-1. ]()
### 🟧 [2-2. ]()
### 🟨 [2-3. ]()
### 🟩 [2-4. ]()
### 🟦 [2-5. ]()
### 🟪 [2-6. ]()
### 🟫 [2-7. ]()
### ⬛ [2-8. ]()
### ⬜ [2-9. ]()
### 🔳 [2-10.]()
### 🔲 [2-11.]()


* * *
## 3
### 🟥 [3-1. ]()
### 🟧 [3-2. ]()
### 🟨 [3-3. ]()
### 🟩 [3-4. ]()
### 🟦 [3-5. ]()
### 🟪 [3-6. ]()
### 🟫 [3-7. ]()
### ⬛ [3-8. ]()
### ⬜ [3-9. ]()
### 🔳 [3-10.]()
### 🔲 [3-11.]()
