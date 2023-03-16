# React_Perfect_Guide

리액트는 사용자 인터페이스를 구축하는 자바스크립트 라이브러리다. 리액트와 같은 라이브러리를 구축하면 기존의 방식보다 쉽게 인터페이스 구축이 가능하다. 이를 가능케 하는 개념은 `컴포넌트` 이다. 웹 인터페이스에서 반복적으로 나타나는 블록을 컴포넌트로 만들어 재사용할 수 있도록 하였다. 따라서 컴포넌트는 HTML,CSS,JavaScript 코드가 집약된 블록이며, 이를 통해 재사용성과 반응성을 구현했다.
컴포넌트가 구현될 수 있는 이유는 리액트가 `선언적 접근 방식`을 채택했기 때문이다. 기존의 바닐라 JavaScript에서 DOM에 직접 아이템을 추가하는 방식이 아닌 그거 리액트에게 최종 형태의 산출물만을 제시하면, 알아서 DOM에 객체를 추가해준다.

# Create-React-App

Create-React-App을 통해 리액트 개발 환경을 빠르게 구축할 수 있다. 이를 위해서는 Node.js를 설치해 노드 패키지 매니저를 이용해 명령어를 실행한다.

터미널에서 create-react-app을 설치하는 모습

![](https://velog.velcdn.com/images/heeyoon1302/post/9a1b68a8-eefc-4abb-a344-7b9536d90a28/image.png)

이후 VSC를 열어 터미널에서
`npm install`
`npm run start`
를 차례대로 입력하여 실행한다.

# 파일로 보는 리액트 원리

## index.js

가장 중요한 파일은 `index.js` 파일이다.![](https://velog.velcdn.com/images/heeyoon1302/post/27166ef0-3584-46a6-ba65-c75bffd0bf48/image.png)
처음 실행하면 다음과 같이 뜨는데, 기존 javascript에서는 유효하지 않는 문법이 존재한다. CSS파일을 import한다던지, 아니면 `<App />`과 같이 HTML 태그를 넣는 일 말이다.
index.js가 중요한 이유는 리액트에서 가장 먼저 실행되는 파일이기 때문이다.
index.js에는 DOM에서 객체를 가져와 Root ReactDOM을 만든다. 이것이 정확히 무엇을 뜻하는 지는 추후에 설명하겠다. 중요한 점은 react-dom이라는 패키지에서 해당 모듈을 가져왓다는 점이다.

## index.html

리액트는 SPA(Single Page Application)이다. 즉 오직 페이지가 하나 뿐이다. 따라서 리액트로 구축하는 웹사이트는 한 페이지 안에서 자바스크립트의 업데이트로 여러 페이지인 것 처럼 보이는 것이다.

index.html 파일에는 id가 root인 div태그가 있다. 이 태그는 내용이 비어있지만, index.js에서 해당 태그를 선택해 ReactDOM을 만들고, 이 DOM을 RootDOM으로 지정한다. 이후 해당 루트 돔에 컴포넌트를 렌더링 함으로써 리액트 프로젝트가 만들어지는 것이다.

렌더링 할 컴포넌트들은 서로 다른 파일에 존재하며, 이를 index.js에서 import하여 최종 조립해 렌더링한다.

# JSX

컴포넌트 파일을 보면 함수가 존재하며, 그 함수의 리턴값이 HTML임을 알 수 있다. 기본적인 javascript에서는 오류가 나야하는데, 리액트는 `jsx`라는 리액트의 문법체계를 만들고, 이렇게 코드를 작성하여도 특별한 과정을 통해 브라우저에서는 오류가 나지 않도록 변환한다.

실제로 브라우저의 개발자 도구를 확인하면 렌더링 파일들은 우리가 작업한 파일들과 다르다는 점을 알 수 있다.
![](https://velog.velcdn.com/images/heeyoon1302/post/c693bb8f-be1e-4355-8f9a-1f5a4f3a04e2/image.png)

# 명령형 접근 방식 vs 선언적 접근 방식

명령형 접근 방식은 바닐라 자바스크립트에서 기존 DOM객체에 새로운 DOM객체를 추가하고자 할 때 사용하는 방식이다. 우리가 일일이 새로운 DOM객체를 만들고 추가하는 과정을 명시해야 한다. 하지만 선언적 접근 방식을 채택한 React에서는 결과만을 명시하면 된다. 왜냐하면 우리가 결과만 알려주면 React에서 알아서 과정을 수행해주기 때문이다.
다음 코드를 통해 명령형과 선언형을 직관적으로 이해할 수 있다.

```javascript
//명령형 접근 방식, 생성,수정,추가의 과정을 명시함.
const item = document.createElement("p");
item.textContent = "This is me";
document.getElementById("para").append(item);

//선언적 접근 방식, 오직 결과만을 알려줌
<div>
  <p>hi</p>
  <p>This is me</p>
</div>;
```

# 컴포넌트

위에서 봤듯이 우리는 index.html이라는 유일한 html파일에 존재하는 id가 root인 div에 우리가 만든 모든 컴포넌트를 렌더링한다. 여러 컴포넌트가 존재할 때, 가장 최상단에 존재하는 컴포넌트를 root 컴포넌트라고 부르며, 컴포넌트 계층 구조를 자연스럽게 만들게 된다.
기본적으로 루트 컴포넌트는 App.js로 설정되어있다.

컴포넌트는 보통 파일을 단위로 작성된다. 즉 하나의 파일안에 하나의 컴포넌트가 존재한다. 따라서 리액트 프로젝트에서 수많은 컴포넌트 파일이 생기는 것은 흔한 일이며, 이를 폴더를 통해 체계적으로 관리하는 것이 좋다.

컴포넌트 파일의 이름은 대문자로 시작해 이후는 Camel Case를 적용하고, 컴포넌트 이름(함수 이름) 또한 마찬가지로 짓는다. 이유는 리액트에서 HTML 태그와 컴포넌트를 구분할 때, 소문자로 시작하는 것은 HTML태그로, 대문자로 시작하는 것은 사용자 지정 컴포넌트로 인식하기 때문이다.

컴포넌트 안의 태그들은 반드시 조상태그를 가져야 한다. 따라서 컴포넌트 내부에 조상태그 없이 여러태그가 존재해서는 안된다,

컴포넌트 내부에 존재하는 태그들에 CSS를 적용하는 기본적인 방법은 `className`을 지정하고, 해당하는 CSS 클래스를 작성하는 것이다.
그리고 해당 CSS 클래스가 작성되어있는 CSS 파일을 컴포넌트 파일에 import하면 된다.

```javascript
import "./ExpenseItem.css";

function ExpenseItem() {
  return (
    <div className="expense-item">
      <div>March 28th 2023</div>
      <div className="expense-item__description">
        <h2>Car Insurance</h2>
        <div className="expense-item__price">$235.4</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```

className은 class가 아니지만, 리액트에서 자동으로 class로 등록해준다

## props

props는 인자로서 컴포넌트에 정보를 전달하기 위해 사용되는 개념이다. 인자로 전달되는 props를 받기 위해 컴포넌트에서 매개변수를 선언해줘야 한다. 리액트 컴포넌트의 계층구조에서 상위 계층이 하위 계층으로 데이터를 전달할 때 props가 이용된다.

```javascript
function App() {
  const expenses = [
    {
      title: "Car Insurance",
      date: new Date(2021, 2, 28),
      amount: 313.32,
    },
    {
      title: "MESPPP Insurance",
      date: new Date(2021, 2, 28),
      amount: 23.32,
    },
    {
      title: "DSX DWW",
      date: new Date(2021, 2, 28),
      amount: 413.32,
    },
  ];
  return (
    <div className="App">
      <h1>hello this is my new Project</h1>
      <Expenses item={expenses} />
      //props로 expenses를 전달함.
    </div>
  );
}

//expenses.js
function Expenses(props) {
  //expenses는 매개변수 선언으로 props를 전달받음.
  return (
    <Card className="expenses">
      <ExpenseItem
        title={props.item[0].title}
        amount={props.item[0].amount}
        date={props.item[0].date}
      />
      <ExpenseItem
        title={props.item[1].title}
        amount={props.item[1].amount}
        date={props.item[1].date}
      />
      <ExpenseItem
        title={props.item[2].title}
        amount={props.item[2].amount}
        date={props.item[2].date}
      />
    </Card>
  );
}
```

props 전달 시 HTMl의 태그 속성으로 사용자가 속성의 이름을 지정해 데이터를 전달한다. 예를 들어

```
<MyCom name={name} age=12 />
```

라고 할 때, MyCom에서 각각의 데이터를 활용하는 방안은 다음과 같다.

```javascript
function MyCom(props) {
  console.log(props.name);
  console.log(props.age);
  return (
    <div>
      my name is {props.name} and age is {props.age}
    </div>
  );
}
```

어떤 컴포넌트가 Wrapper컴포넌트로서의 역할을 할 경우, 즉 다른 컴포넌트들의 최상위부모가 되는 컴포넌트가 되는 경우 다음과 같은 작업이 필요하다.

```javascript
function Expenses(props) {
  return (
    <Card className="expenses">
      <ExpenseItem
        title={props.item[0].title}
        amount={props.item[0].amount}
        date={props.item[0].date}
      />
      <ExpenseItem
        title={props.item[1].title}
        amount={props.item[1].amount}
        date={props.item[1].date}
      />
      <ExpenseItem
        title={props.item[2].title}
        amount={props.item[2].amount}
        date={props.item[2].date}
      />
    </Card>
  );
}
```

현재 여기서 Card 컴포넌트가 Wrapper 컴포넌트이다. 이와 같이 Wrapper 컴포넌트로서 다른 여러 컴포넌트나 태그들을 포함할 경우, Wrapper 컴포넌트에서는 다음과 같은 별도의 설정이 필요하다.

```javascript
import "./Card.css";

function Card(props) {
  const classes = "card " + props.className;
  return <div className={classes}>{props.children}</div>;
}

export default Card;
```

Card는 props로 전달받은 데이터가 없지만, 매개변수로 props로 지정하고, {props.children}을 명시해줘야 한다.

### 이벤트 핸들링

우리는 바닐라 자바스크립트에서 클릭 이벤트를 감지하고, 특정 함수를 호출하기 위해 `addEventListner` 를 사용했다. 리액트에서도 그러한 문법은 유효하지만, 다른 더 간편한 방법이 준비되어있다. 리엑트에서는 이벤트와 관련된 문법을 모두 on으로 시작하는 props명으로 준비했다. 따라서 어떤 태그나 컴포넌트에 클릭 이벤트 감지기를 추가하고 싶다면 props로 `onClick` 과 실행 함수를 전달하면 된다.

```javascript
function ExpenseItem(props) {
  const clickMeHandler = () => {
    console.log("햐이");
  };
  return (
    <Card className="expense-item">
      <button onClick={clickMeHandler}>click me</button>
    </Card>
  );
}
```

버튼 클릭 시에 콘솔에 햐이라는 글자가 출력될 것이다.

# useState

onClick을 통해 특정 함수를 실행할 때, ui를 업데이트를 업데이트 할 수 있을까? 실제로 다음과 같이 코드를 작성하여도 ui는 업데이트 되지 않는다.

```javascript
function ExpenseItem(props) {
  let title = props.title;
  const clickMeHandler = () => {
    title = "changed!";
    //title을 동적으로 바꾸고자 시도하지만 ui는 업데이트 되지 않음
    console.log("햐이");
  };
  return (
    <Card className="expense-item">
      <ExpenseDate date={props.date} />
      <div className="expense-item__description">
        <h2>{title}</h2>
        <div className="expense-item__price">${props.amount}</div>
      </div>
      <button onClick={clickMeHandler}>click me</button>
    </Card>
  );
}

export default ExpenseItem;
```

그 이유는 컴포넌트가 함수이기 때문이다. 그리고 리액트는 해당 컴포넌트의 실행을 처음 index.html을 불러올 때 평가하고 실행한다. 따라서 ui가 업데이트 되기 위해서는 해당 컴포넌트가 재평가된 후 재실행 되어야 한다. 이것을 가능하게 하기 위해 도입된 개념이 State이다. State는 리액트에서 제공하는 여러가지 내장함수 중 하나로, 이러한 것들을 `훅` 이라고 부르며, 모든 훅은 use로 시작한다. 따라서 리액트에서 사용하는 state는 useState()이다.

useState()는 ui업데이트와 관련있는 동적인 값을 저장하는 state(일반적인 변수와 다르다)와, 해당 변수의 값을 설정하는 setter함수를 리턴한다. 그리고 만약 setter함수를 통해 새로운 값을 설정하면, 해당 useState를 가지고 있는 컴포넌트가 재평가 후 재실행되어, 새로 설정한 값이 ui에 업데이트 된다.

```javascript
import { useState } from "react";
//useState를 사용하기 위해서는 리액트 라이브러리에서 import해줘야 함.

function ExpenseItem(props) {
  const [title, setTitle] = useState(props.title);
  //useState가 리턴하는 state와 setter를 모두 받기 위해
  //구조 분해 할당으로 처리하는 것이 국룰이다.
  const clickMeHandler = () => {
    setTitle("changed!");
  };
  return (
    <Card className="expense-item">
      <ExpenseDate date={props.date} />
      <div className="expense-item__description">
        <h2>{title}</h2>
        <div className="expense-item__price">${props.amount}</div>
      </div>
      <button onClick={clickMeHandler}>click me</button>
    </Card>
  );
}
```

state와 변수가 다른 점은 만약 state가 저장되어있는 컴포넌트가 여러번 사용되었을 때, 각각의 호출되는 컴포넌트마다 state가 독립적으로 값을 관리한다.
즉 첫 번째 컴포넌트의 버튼을 눌러서 첫 번째 컴포넌트의 title 글자만 바뀌고, 두 번째 컴포넌트의 title글자는 바뀌지 않게 한다.

## prevState

state가 변경될 때, 즉 setter함수가 실행되면, 해당 함수를 실행하는 컴포넌트는 리렌더링 되어 ui가 업데이트 된다. 문제는 해당 setter함수를 포함하고 있는 함수의 실행이 모두 종료되면 컴포넌트가 리렌더링 된다는 점이다. 따라서 해당 함수 안에 여러 setter함수를 실행시키고자 하면, 새로 업데이트 된 값을 이용하지 못하고 기존 값을 업데이트 하는 작업만 반복할 뿐이다. 다음의 예를 통해 이해해보자.

```javascript
  const [count, setCount] = useState(0);
  const onClickCount = () => {
    setCount( count + 1);
    setCount( count + 1);
        //아직 컴포넌트가 리랜더링 되지 않아서, 이전 값인 0에서 다시 1을 더한다.
    setCount( count + 1);
    setCount( count + 1);
        //여전히 0에서 1을 더함으로, 최종 값은 4가 아닌 1이다.
  };
  return (
    <div>
      <div>현재카운트:{count}</div>
      <button onClick={onClickCount}>카운트 올리기</button>
    </div>
  );
};
```

따라서 컴포넌트가 리랜더링 되기 전에 미리 변경한 state값을 사용하는 방법은 다음과 같다.

```javascript
  const [count, setCount] = useState(0);
  const onClickCount = () => {
    setCount((count) => count + 1);
    setCount((count) => count + 1);
    setCount((count) => count + 1);
    setCount((count) => count + 1);
  };
  return (
    <div>
      <button onClick={onClickCount}>+1</button>
    </div>
  );
};
```

## 부모 관계로 데이터 전달

위에서 설명했다시피, 리액트는 컴포넌트 트리를 구성한다. 그리고 부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달하고 싶으면 props를 전달하면 된다. 그러면 자식은 어떻게 부모로 데이터를 전달하는가? 이때에도 props를 이용하지만, 정확히는 부모 컴포넌트에서 정의내리는, 매개변수는 자식 컴포넌트의 값을 수용하는 함수를 props로 전달하면 된다. 그렇게 하면 자식 컴포넌트에서는 props로 받은 부모컴포넌트의 함수를 실행하여 인자를 전달할 수 있기 때문이다.

따라서 만약 당신이 형제 관계의 컴포넌트로 데이터를 전달하고 싶으면, 먼저 부모님에게 데이터를 전달한 뒤, 부모님보고 형제한테 전달해달라고 하면 된다.

귀찮으니까 그냥 리덕스나 다른 편한 상태관리 프레임워크를 사용하면 된다.

# 투 두 리스트 만들기 - 리스트 다루기

투-두를 기본적으로 객체로 다루고, 여러가지 객체(투-두)들을 배열에 담아서 활용한다. 배열은 useState로 선언하여, 배열에 값이 추가되거나 삭제될 때 ui가 업데이트 되도록 한다.

배열에 기본값(기본적으로 저장되어 있는 객체)을 저장하고 싶을 때, 다음과 같이 분리해서 선언할 수 있다.

```javascript
const INITIAL_EXPENSE = [
  {
    title: "Car Insurance",
    date: new Date(2021, 2, 28),
    amount: 313.32,
    id: 1,
  },
  {
    title: "i wanna go home",
    date: new Date(2021, 2, 28),
    amount: 23.32,
    id: 2,
  },
  {
    title: "DSX DWW",
    date: new Date(2021, 2, 28),
    amount: 413.32,
    id: 3,
  },
];

function App() {
  const [expenseData, setExpenseData] = useState(INITIAL_EXPENSE);

```

새로운 값을 추가할려면 useState의 setter함수를 이용해야 한다. 보통 데이터를 보여주는 컴포넌트와 데이터를 추가하는 컴포넌트는 서로 다른 컴포넌트로 분리하며, 해당 컴포넌트는 서로 형제관계인 경우가 많으므로, 부모 컴포넌트에서 state를 선언하고, 보여주는 컴포넌트에게는 state를 props로 전달하고, 추가하는 컴포넌트에는 setter함수를 props로 전달하면 된다.
만약 기존 state에 새로운 값을 추가하는 경우라면 setter함수 안에 스프레드 연산자를 이용해서 state를 다시 넣어줘야 하기 때문에, 이러한 경우에는 부모 컴포넌트에서 stter함수를 실행하는 함수를 만들어 그 함수를 props로 전달하기도 한다.

함수를 전달받은 아이템 추가 컴포넌트는 input창으로부터 사용자가 입력한 정보를 토대로 객체를 만들고, 그 객체를 전달받은 함수의 인자로 넘겨주면 새로운 아이템이 추가되어 Ui에 나타나도록 설계한다.

이 과정에서 다음과 같은 코드 구성이 사용된다.

```javascript
  const onSaveExpenseData = (expense) => {
    setExpenseData((prevExpense) => {
      return [expense, ...prevExpense];
      //스프레드 연산자를 통해 기존 state를 유지하고, 새로운 객체를 추가함.
    });
  };

  return (
    <div className="App">
      <h1 className="mainTitle">hello this is my new Project</h1>
      <NewExpense onSaveExpenseData={onSaveExpenseData} />
//state배열에 객체를 추가하는 함수를 props를 전달함.
      <Expenses item={expenseData} />
    </div>
  );
}

```

```javascript
  const [inputTitle, setTitleInput] = useState("");
  const [inputDate, setDateInput] = useState("");
  const [inputAmount, setAmountInput] = useState("");

  const titleInputHandler = (e) => {
    setTitleInput(e.target.value);
  };
//onChange가 감지되면, 해당 input창의 value를 state값으로 설정함.

  const amountInputHandler = (e) => {
    setAmountInput(e.target.value);
  };

  const dateInputHandler = (e) => {
    setDateInput(e.target.value);
  };


...생략

          <input
            type="text"
            onChange={titleInputHandler}
//입력창의 값에 변화가 생기면, 지정 함수를 실행함.
            value={inputTitle}
            //입력창 초기화를 위함임. 지금은 보이지 않는 submit 버튼을 누르면
//inputTitle 값이 공백이 됨. 따라서 input창도 초기화 됨.
          ></input>
        </div>
        <div className="new-expense__control">
          <label>Amount</label>
          <input
            type="number"
            min="0.01"
            step="0.01"
            onChange={amountInputHandler}
            value={inputAmount}
            //입력창 초기화를 위함임.
          ></input>
        </div>
        <div className="new-expense__control">
          <label>Date</label>
          <input
            type="date"
            min="2019-01-01"
            max="2022-12-31"
            onChange={dateInputHandler}
            value={inputDate}
            //입력창 초기화를 위함임.
          ></input>
```

그리고 이런 입력창과 button 조합 구성은 form 태그로 감싸주는 것이 시맨틱하다. 하지만 문제는 button을 클릭했을 때 페이지가 리로드 된다. 그것을 막기 위해 다음과 같이 작성한다.

```javascript
//제출버튼을 클릭했을 실행되는 함수임.

e.preventDefault();
//form태그 안에 button태그가 존재하면 그것을 눌렀을 때 페이지가 리로드 되는데,
//해당 함수를 실행하면 페이지가 리로드 되지 않음
const expenseData = {
  title: inputTitle,
  amount: +inputAmount,
  //+연산자를 사용하면 숫자로 형변환 된다.
  date: new Date(inputDate),
  id: Math.random(),
};
//입력값을 토대로 객체를 만든다.
props.onSaveExpenseData(expenseData);
//props로 전달 받은 객체 추가 함수에 인자로 새로 맏는 객체를 전달함.
setTitleInput("");
setAmountInput("");
setDateInput("");
//submit 후 입력창 초기화를 위함임.
```

# 필터

javascript의 filter함수를 사용한다.

```javascript
const filteredExpenses = props.item.filter((expense) => {
  return expense.date.getFullYear() === filterYear;
});
```

내가 선택한 해의 객체만 보여주는 코드이다.

# 조건부 내용 출력

조건에 따라 보여지는 내용을 달리 하는 것이다. 프론트엔드 개발 시 거의 필수적으로 사용되는 방법이다.

**삼항연산자 이용
**

```javascript
<div className="new-expense">
  {showAddExpenseForm ? (
    <ExpenseForm
      onSaveExpenseData={props.onSaveExpenseData}
      newExpenseHandler={newExpenseHandler}
    />
  ) : (
    <button onClick={newExpenseHandler}>Add New Expense</button>
  )}
</div>
```

showAddExpenseForm이라는 boolean값을 저장하는 state를 이용해 삼항연산자로 위와 같이 표현할 수 있다.

또는 변수에 jsx구문을 저장하고, 조건문으로 변수의 내용을 달리할 수 있다. 즉, return 문 안에는 {변수이름} 이것만 넣고, return 위에 자바스크립트 코드 작성하는 곳에서 처리한다는 뜻이다.
