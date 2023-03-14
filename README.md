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

className은 class가 아니지만, 리액트에서 자동으로 class로 등록해주기 때문에
