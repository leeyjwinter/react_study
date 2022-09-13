# react_study

>리액트를 사용해서 프로젝트는 간간히 했는데 막상 문서로 정리한 적은 한번도 없었던 것 같다.
알던 내용은 다잡고 잊은 내용은 다시 되짚도록 
니꼬쌤의 리액트 강의를 듣고 나름대로의 정리를 해봐야지,,
https://nomadcoders.co/react-for-beginners

## 📌리액트 가져오기 (reactjs, react-DOM)

리액트는 라이브러리다. 이전에 프로젝트를 진행할 때는 공식 사이트에서 리액트를 다운받아서 npm 을 통해 앱을 실행시키는 형태로 작업을 했었는데

니꼬쌤의 강의는 unpkg 사이트에서 라이브러리를 script 형식으로 가져와서 사용하였다. 강의 상에서 설명을 위해 이같이 하는 것으로 보인다.

```html
<script src = "https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
<script src = "https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
```

 >`React JS` 는 어플리케이션이 interactive 하게 만들어주는 library, `React-DOM`은 리액트에서 생성한 요소(element)를 html의 body안에 넣을 수 있도록 해준다.
 
<br>

 간단한 html 코드에서
 
 ```html
<!DOCTYPE html>
<html>
<body>
    <div id="root"></div>
</body>
<script src = "https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
<script src = "https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
<script>
    const root = document.getElementById("root");
    const span = React.createElement("span", {id:"sexy-span"}); 
    ReactDOM.render(span, root);
</script>
</html>
```

body 안에 root 아이디를 가진 div를 넣어주고 react 라이브러리를 통하여 요소를 생성하여 react-dom 라이브러리를 통하여 root 안에 span을 렌더링 해준다.

<img src="https://velog.velcdn.com/images/leeyjwinter/post/4f848f4d-ac5e-45be-8660-ad766e770941/image.png">

페이지 검사를 하면 위처럼 root 안에 span이 추가되었다.

## 📌React.createElement


```javascript
<div id="root"></div>
const root = document.getElementById("root");
const span = React.createElement(
        "span",
        {
            id: "sexy-span",
            style: { color: "red" }
        },
        "Hello I'm a span");
const btn = React.createElement("button", null, "Click me!");
const container = React.createElement("div", null, [span,btn]);


ReactDOM.render(container, root);
```

div, span, button 요소들을 생성해주고, 그 생성한 요소들을 리스트 형태로 container 변수의 div안에 `[span, btn]` 과 같이 넣어서 렌더링을 해준다. 

## 📌JSX를 사용하여 element 만들기

>JSX는 javascript의 확장된 문법으로, HTML에서 요소를 만드는 것과 흡사한 방법으로 javascript에서 요소를 바로바로 만들 수 있도록 해준다.
***
지금까지 내가 배워온 리액트가 이 JSX를 사용하는 방식이었다,, 모르고 그냥 썼었네,,,


```js
    const Title = <h3 id="title" onMouseEnter={() => console.log("mouse entered")}>
        Hello I'm a title</h3>
    /*const Title = React.createElement(
        "h3",
        {
            id: "title",
            onMouseEnter: ()=>console.log("mouse entered")
        },
        "Hello I'm a title");*/
```
주석처리된 부분을 JSX로 처리하여 간단하게 표현할 수 있다. 

## 📌JSX 통한 컴포넌트 렌더링

```js
const container = React.createElement("div", null, [Title,btn]);

Title과 Button 변수를 만들어서 html형식으로 저장을 했는데, 
이들을 묶어 렌더링을 하는 것도 위처럼이 아닌 간단하게
표현을 할 수 있다.
```

```js
<script type="text/babel">
    const root = document.getElementById("root");
    const Title = () => <h3 id="title" onMouseEnter={() => console.log("mouse entered")}>
        Hello I'm a title</h3>
    const Button = () => <button onClick={() => console.log("I am clicked")}>Click Me!</button>
    const Container = () => <div>
        <Title />
        <Button />
    </div>
    ReactDOM.render(<Container/>, root);
</script>
```

먼저 element 들을 모두 함수화한다. `=() = >` .
그 다음 같이 묶어주고 싶다면 `Container`함수에 사용한 것처럼 안에 컴포넌트 태그 형태로 넣어줄 수 있다. 

	컴포넌트는 모두 첫 문자가 대문자로 시작해야 한다! 
    Title, Button, Container 등등
 마지막으로 요소들을 담은 컴포넌트를 (위 예시에서는 Container) 렌더링 해준다. 
 

 
 ![](https://velog.velcdn.com/images/leeyjwinter/post/f5834f39-22f3-4545-9351-16c91e035b2d/image.png)


> 내가 아는 리액트 사용법까지 오기까지의 듀토리얼이었다. 사실 내가 사용하는 것이 JSX였구나~ 라는 것도 모른 채 무지성으로 리액트를 대했던거 같다. 아무래도 1주일 안에 프로젝트 하나를 완성시키려다보니,,ㅎㅎㅎ


## 📌State에 앞서,,


### 🔑인터렉티브한 리액트
Vanilla JS와 다른 React의 장점은 바뀌려고 하는 데이터가 업데이트 될 때, Vanilla는 바뀌는 데이터가 포함된 태그 전체를 새로고침하는 반면, 리액트는 바뀌는 부분만을 새로고침해준다.

### 🔑JSX에서 태그안에 변수 내용 넣기

vanilla 에서는 

```js
span.innerText = `total clicks : ${counter}`;
```
로 표현하여 버튼의 클릭 수 변수를 태그의 innerText에 넣어줬다면, 리액트의 JSX는 
```js
<h3>Total Clicks : {counter}</h3>
```
와 같이 백틱을 사용하지 않고 중괄호에 변수명을 넣어준다.


>버튼을 클릭하면 클릭 수를 화면에 표시해주는 코드
```js
const root = document.getElementById("root");
    let counter = 0;
    function countUp() {
        counter = counter + 1;
        ReactDOM.render(<Container />, root);
    }
    const Container = () => <div>
        <h3>Total Clicks : {counter}</h3>
        <button onClick={countUp}>Click Me!</button>
    </div>
    ReactDOM.render(<Container />, root);
```
countUp 함수에서 클릭을 할 때마다 새로 렌더링을 하여 화면에 보이는 숫자를 계속 업데이트 해준다.


## 📌React.useState

인터렉티브하게 변수값을 화면에 노출시켜주려면은 계속 바뀌는 값 전체에 re-rendering함수를 사용해야 하는 것은 아니다.

`React.useState()`
함수 안에는 state를 변경해주고 싶은 값, 그리고 그것을 바꾸는 function을 리스트 형태로 넣을 수 있다. 

```js
const data = React.useState(0,countUp);
        const counter = data[0];
        const modifier = data[1];
```
위에서 0이 counter 값, countUp함수가 modifier로 들어가는 것이다.

그리고 보통은 아래와 같이 한번에 변수를 할당해준다.
>
```js
const [counter, modifier] = React.useState(0);
```

### 🔑state 변경 함수

```js
function App() {
        let [counter, setCounter] = React.useState(0);
        function onClick() {
            setCounter(counter + 1);
        }
        return (
            <div>
                <h3>Total Clicks : {counter}</h3>
                <button onClick={onClick}>Click Me!</button>
            </div>)
    }
```

App 컴포넌트를 봤을 때 SetCounter가 counter의 값을 바꿔주는 함수이다. 이는 `setCounter(counter + 1)`과 같이 안에 return될 counter값을 바로 넣어주면 된다. 
>setCounter는 counter값을 바꿔주는 동시에 화면에 렌더링도 새로 해줘 따로 렌더링 함수가 필요 없다.

### 🔑current로 state 에 따른 값 변경

앞서 설명한대로 지정된 변수 값을 직접 변경하는 형태로 modifying 함수를 작성할 수도 있지만 변수 값에 직접 접근하는 것이므로, 변수가 다른 곳에서 바뀌었을 수 있으므로 안정된 방법이 아니다.

이에 대비하여 `그 변수의 현재 상태에 따른 값 변경`을 위하여 `current` 키워드를 사용한다.

```js
function onClick() {
            setCounter(current => current + 1);
        }
```
>current는 useState의 0번째 값의 현재 값을 뜻하는 키워드이다.

***

### 🔑참고 - JSX와 HTML은 비슷하지만 다르다

HTML의 사용법과 완전히 동일하게 JSX를 작성하면 일반적으로 큰 무리는 없지만, class속성이나, label태그의 for 속성은 JSX에서는

**class - className
for - htmlFor**

등으로 바꿔 사용해야 한다.
***

### 🔑입력한 값을 useState로 업데이트

```js
function App() {
        const [minutes, setMinutes] = React.useState();
        const onChange = (event) => {
            setMinutes(event.target.value)
        }
        return (
            <div>
                <h1>Super Converter</h1>
                <label for="minutes">Minutes</label>
                <input
                    value={minutes}
                    id="minutes"
                    placeholder='Minutes'
                    type="number"
                    onChange={onChange} />
                <h4>You want to convert {minutes}</h4>
                <label for="hours">Hours</label>
                <input id="hours" placeholder='Hours' type="number" />
            </div>
        );
    }
```

js의 event를 가져와 그 event(여기서는 onChange event)의 target의 value값을 가져오면 현재 내가 input에 입력하고 있는 값을 가져와 useState로 minutes에 값을 넣을 수 있다. 

![](https://velog.velcdn.com/images/leeyjwinter/post/91ee94b9-642b-4b3b-82f3-39ed7d38a686/image.gif)

#### ex) minutes to hours 변환기

>**전체코드**
```js
<!DOCTYPE html>
<html>
<body>
    <div id="root"></div>
</body>
<script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
<script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
<script type="text/babel">
    const root = document.getElementById("root");
    function App() {
        const [minutes, setMinutes] = React.useState();
        const onChange = (event) => {
            setMinutes(event.target.value)
        }
        const reset = () => setMinutes(0);
        return (
            <div>
                <h1>Super Converter</h1>
                <label for="minutes">Minutes</label>
                <input
                    value={minutes}
                    id="minutes"
                    placeholder='Minutes'
                    type="number"
                    onChange={onChange} />
                <h4>You want to convert {minutes}</h4>
                <label for="hours">Hours</label>
                <input value={minutes / 60} id="hours" placeholder='Hours' type="number" />
                <div>
                    <button onClick={reset}>reset</button>
                </div>
            </div>
        );
    }
    ReactDOM.render(<App />, root);
</script>
</html>
```

hour 박스에서 useState로 받은 minutes를 hour로 변환시키고, reset 버튼을 만들고 setMinutes를 통해 minutes를 0으로 reset 해주는 코드이다. 


![](https://velog.velcdn.com/images/leeyjwinter/post/8b00f805-28e5-4750-a704-ea9fc3db2bb2/image.gif)


## Props에 앞서,,,

![](https://velog.velcdn.com/images/leeyjwinter/post/23800241-3c24-433d-854b-22df24c999b0/image.png)

버튼의 이름만을 제외한 색이나 패딩같은 스타일은 같은 버튼을 여러개 만들고 싶다면 CSS에 작성하여 같은 스타일을 가져올 수도 있고

```js
function SaveBtn() {
        return (
            <button style={{
                backgroundColor: "tomato",
                color: "white",
                padding: "10px 20px",
                border: 0,
                borderRadius: 10
            }}>Save Changes</button>
        );
    }
    function ConfirmBtn() {
        return (
            <button>Confirm</button>
        );
    }
```
위의 JSX의 SaveBtn 안에 스타일에 적은 값들을 ConfrimBtn에도 똑같이 옮겨 담을 수도 있을 것이다. 하지만 많은 속성이 겹치는 버튼에서 몇가지만 다르게 하기 위하여 **매개변수로 값을 전달**할 수 있으면 재사용성이 훨씬 좋아질 것이고, 이를 위하여 사용하는 것이 `props`이다.


## 📌Props 사용법

```js
function App() {
        return (
            <div>
                <Btn banana="Save Changes" x={false} />
                <Btn banana="Continue" y={7} />
            </div>
        );
    }
```

먼저 최종 Btn 컴포넌트에서 `banana`라고 하는 임의의 값을 전달해 준다고 하자, 내가 만든 banana, x는 오브젝트로 묶여 function Btn의 props로 들어간다.
나는 여기서 banana를 button의 텍스트로 사용할 것이므로 
button 함수를

```js
function Btn(props) {
        return (
            <button style={{
                backgroundColor: "tomato",
                color: "white",
                padding: "10px 20px",
                border: 0,
                borderRadius: 10
            }}>{props.banana}</button>
        );
    }
```
이와 같이 작성해준다.
`props.banana`에서 props 오브젝트의 banana 값만을 가져온다. 만약 매개변수로 사용할 값이 오직 banana 뿐이라면

```js
function Btn({banana}) {
        return (
            <button style={{
                backgroundColor: "tomato",
                color: "white",
                padding: "10px 20px",
                border: 0,
                borderRadius: 10
            }}>{banana}</button>
        );
    }
```
와 같이 banana자체를 매개변수 값으로 지정해줄 수도 있다.

## 📌React.memo

또한 useState를 사용하여 value값을 바꾸는 함수도 props로 줄 수 있다.

>useState선언 및 setValue선언
```js
const [value, setValue] = React.useState("Save Changes");
        const changeValue = () => setValue("Revert Changes");
```

>value값 및 changeValue함수 props로 전달
```
<Btn text={value} changeValue={changeValue} />
<Btn text="Continue" />
```

>Btn 함수의 onclick리스너에 changeValue 할당
```js
function Btn({ text, changeValue }) {
        return (
            <button
                onClick={changeValue}
                style={{
                    backgroundColor: "tomato",
                    color: "white",
                    padding: "10px 20px",
                    border: 0,
                    borderRadius: 10
                }}>{text}</button>
        );
    }
```

이wp SaveChanges 버튼을 클릭하면 Revert Changes로 텍스트가 바뀐다. 그런데 이 과정에서 text가 Continue인 것 까지 렌더링이 다시 된다. 부모 요소에서 state가 바뀌면서 리렌더링 되는 과정에서 자식들도 리렌더링되기 때문인데, `React.memo`기능으로 바뀌지 않는 버튼의 리렌더링을 방지할 수 있다.

```js
const MemorizedBtn = React.memo(Btn);
    function App() {
        const [value, setValue] = React.useState("Save Changes");
        const changeValue = () => setValue("Revert Changes");
        return (
            <div>
                <MemorizedBtn text={value} changeValue={changeValue} />
                <MemorizedBtn text="Continue" />
            </div>
        );
    }
```
이제 Continue를 텍스트로 가지는 버튼은 다른 버튼이 눌려 리렌더링이 되도 함께 다시 렌더링 되지 않아 메모리 소모를 줄일 수 있다.

## 📌PropTypes
Props의 형을 제한하는 조건을 줄 수 있다.
예를 들어
```
            <div>
                <Btn text={value} changeValue={changeValue} fontSize={18} />
                <Btn text={14} />
            </div>
```
다음과 같이 text가 string이 아닌 number이 들어가는 경우에 개발자나, 사용자에게 경고 문구를 해줘야 할 수 있다.

```
<script src="https://unpkg.com/prop-types@15.7.2/prop-types.js"></script>
```
위 스크립트 파일을 가져오고,

```js
Btn.propTypes = {
        text: PropTypes.string.isRequired,
        fontSize: PropTypes.number
    };
```
버튼의 propTypes 속성을 정의해주면 된다. 형 외에 값을 둘 중 하나로 해야한다거나, 필수적으로 입력해야 되는 것 등의 조건을 지정해줄 수 있다.


