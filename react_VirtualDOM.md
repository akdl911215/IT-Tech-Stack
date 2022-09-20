## 리액트 정의 : Virtyal DOM은 무엇인가?
Virtual DOM(VDOM)은 UI의 이상적인 또는 "가상"적인 표현을 메모리에 저장하고 ReactDOM과 같은 라이브러리에 의해 
"실제" DOM과 동기화하는 프로그래밍 개념이다.  이 과정을 재조정(Reconciliation)이라고 한다.



이 접근방식이 React의 선언적 API를 가능하게 한다. React에게 원하는 UI의 상태를 알려주면 DOM이 그 상태와 일치하도록 한다. 
이러한 방식은 앱 구축에 사용해야 하는 어트리뷰트 조작, 이벤트 처리, 수동 DOM 업데이트를 추상화한다.



"virtual DOM"은 특정 기술이라기보다는 패턴에 가깝기 때문에 사람들마다 의미하는 바가 다르다. 
React의 세계에서 "virtual DOM"이라는 용어는 보통 사용자 인터페이스를 나타내는 객체이기 떄문에 
React elements와 연관된다. 그러나 React는 컴포넌트 트리에 대한 추가 정보를 포함하기 위해 "fivers"라는 
내부 객체를 사용한다. 또한 React 에서 "virtual DOM" 구현의 일부로 간주할 수 있다.



## 재조정 이란?
React는 선언적 API를 제공하기 때문에 갱신이 될 때마다 매번 무엇이 바뀌었는지를 걱정할 필요가 없다. 
이는 애플리케이션 작성을 무척 쉽게 만들어주지만, React 내부에서 어떤 일이 일어나고 있는지는 명확히 눈에 
보이지 않는다. 이 글에서는 우리가 React의 "비교 (diffing)" 알고리즘을 만들때 어떤 선택을 했는지를 소개한다. 
이 비교 알고리즘 덕분에 컴포넌트의 갱신이 예측 가능해지면서도 고성능 앱이라고 불러도 손색없을 만큼 충분히 빠른 앱을 만들 수 있다."



------------------------------------------------------------------------------------------------------------



솔직히 리액트 홈페이지의 설명만으로는 어떤 이야기인지 잘모르겠다.
밑에서 차근차근하게 알아가보자.



-------------------------------------------------------------------------------------------------------------



## DOM 이란?
DOM(Document Object Modal)은 HTML / XML 문서에 접근하기 위한 인터페이스이다. 
DOM은 문서의 구조화되 표현(structured representation)을 제공하며 프로그래밍 언어가 
DOM 구조에 접근할 수 있는 방법을 제공하여 그들이 문서 구조, 스타일, 내용 등을 변경할 수 있게 돕는다. 
DOM은 nodes와 objects로 문서를 표현한다. 
이들은 웹 페이지를 스크립트 또는 프로그래밍 언어들에서 사용될 수 있게 연결시켜주는 역할을 담당한다. 

웹 페이지는 일종의 문서(document)다. 이 문서는 웹 브라우저를 통해 그 내용이 해석되어 웹 브라우저 화면에 
나타나거나 HTML 소스 자체로 나타나기도 한다. 동일한 문서를 사용하여 이처럼 다른 형태로 나타날 수 있다는 
점에 주목할 필요가 있다. DOM은 동일한 문서를 표현하고, 저장하고, 조작하는 방법은 제공한다. 
DOM은 웹 페이지의 객체 지향 표현이며, 자바스크립트와 같은 스크립팅 언어를 이용해 DOM을 수정할 수 있다.



## DOM을 조작하는 방법
리액트를 사용하지 않더라도 개발자는 자바스크립트(JS)에서 직접 그리고 빠르게 돔을 조작 할 수 있다.
Virtual DOM을 사용해서 DOM을 조작하는것은 2단계를 거쳐야하며, 바로 DOM을 조작하는것은 1단계이기 때문이다.


  // js
  function addItem () {
    const value = document.getElementById('input').value;
    const list = document.getElemendById('list');
    const newItem = document.createElement('li');
    const text = document.createTextNode(value);
  
    newItem.appendChild(text);
    list.appendChild(newItem);
  }

  // html
  ...
  <ul id="list">
    <li>a</li>
    <li>b</li>
  </ul>
  <input id="input"></input>
  <button onclick="addItem">+</button>
  ...
  
  
  
  
## 그렇다면 ViruDOM 을 사용하는 이유는?
Web의 복잡도가 점차 증가하고 많은 요구사항들이 생겨나기 시작했다. 
그러면서 DOM 조작의 빈도가 높아지고 자연스럽게 DOM 조작은 브라우저 렌더 과정을 계속 발생시켜, 
상당한 비용을 발생시켜 비효율적으로 만들었다. 그렇기 때문에 Virtual DOM이 탄생하게 되었다.



일단 이해하기 위해서는 브라우저의 동작 과정에 대한 이해가 필요하다.



렌더링 엔진은 통신으로부터 요청한 문서의 내용을 얻는 것으로 시작하는데 문서의 내용은 보통 8KB 단위로 전송된다.



다음은 렌더링 엔진의 기본적인 동작 과정이다.



<img width="514" alt="1" src="https://user-images.githubusercontent.com/76759835/191286472-0cae0d36-b413-442f-8cef-a0a02a6259f4.PNG">


렌더링 엔진은 HTML 문서를 파싱하고 "콘텐츠 트리" 내부에서 태그를 DOM 노드로 변환한다. 
그 다음 외부 CSS 파일과 함께 포함된 스타일 요소도 파싱한다. 스타일 정보와 HTML 표시 규칙은 
"렌더 트리"라고 부르는 또 다른 트리를 생성한다.



렌더 트리는 색상 또는 면적과 같은 시각적 속성이 있는 사각형을 포함하고 있는데 정해진 순서대로 화면에 표시된다.



렌더 트리 생성이 끝나면 배치가 시작되는데 이것은 각 노드가 화면의 정확한 위치에 표시되는 것을 의미한다. 
다음은 UI백엔드에서 렌더 트리의 각 노드를 가로지르며 형상을 만들어 내는 그리기 과정이다. 



일련의 과정들이 점진적으로 진행된다는 것을 아는 것이 중요하다. 
렌더링 엔진은 좀 더 나은 사용자 경험을 위해 가능하면 빠르게 내용을 표시하는데 모든 HTML을 파싱할 때까지 
기다리지 않고 배치와 그리기 과정을 시작한다. 네트워크로부터 나머지 내용이 전송되기를 기다리는 동시에 받은 
내용의 일부를 먼저 화면에 표시하는 것이다. 



<img width="714" alt="1" src="https://user-images.githubusercontent.com/76759835/191286895-8b909a19-3f6c-45de-ad89-26245d05f6fa.PNG">



웹킷과 게코가 용어를 약간 다르게 사용하고 있지만 동작 과정은 기본적으로 동일하다는 것을 그림3과 그림4에서 알 수 있다.



게코는 시각적으로 처리되는 렌더 트리를 "형상 트리(grame tree)"라고 부르고 각 요소를 형상(frame)이라고 하는데 웹킷은 
"렌더 객체(redenr object)"로 구성되어 있는 "렌더 트리(render tree)"라고 용어를 사용한다. 
웹킷은 요소를 배치하는데 "배치(layout)"라는 용어를 사용하지만 게코는 "리플로(reflow)"라고 부른다. 
어태치먼트(attachment)"는 웹킷이 렌더 트리를 생성하기 위해 DOM 노드와 시각 정보를 연결하는 과정이다. 
게코는 HTML과 DOM 트리 사이에 "콘텐츠 싱크(content sink)"라고 부르는 과정을 두는데 이는 DOM 요소를 생성하는 공정으로 
웹킷과 비교하여 의미있는 차이점이라고 보지는 않는다.
  
  
  
위의 그림대로 브라우저는 동기(Synchronous)적으로 HTML, CSS, Javascript를 처리한다.



Critical rendering path(크리티컬 렌더링 패스) 는 브라우저가 HTML 응답을 받아 화면을 그리기 위해 실행하는 과정이다.



<img width="648" alt="1" src="https://user-images.githubusercontent.com/76759835/191287352-4c94d29a-87fb-4eab-9975-6bc3059d25a2.PNG">



총6단계이다.
1단계. HTML 파이이 렌더링 엔진의 HTML 파서에 의해 파싱(Parsing)되어 DOM 생성 
- HTML 태그들 HTML 토큰이 되어 node 객체로 변환되고 이는 트리 형태로 되어 있다.

2단계. CSS 파일이 렌더링 엔진의 CSS 파서에 의해 파싱(Parsing)되어 CSSOM 생성

3단계. Javascript엔진이 Javasciprt 파일을 로드하고 파싱하여 실행 (DOM 생성이 중지됨)

4단계. DOM과 CSSOM을 묶어 Render Tree를 생성

5단계. Layout이 생성되며 객체의 정확한 위치 및 크기를 계산한다.

6단계. 마지막 단계는 최종 렌더링 트리에서 수행되는 페인트이며, 픽셀을 화면에 렌더링 한다.



이런 보기에는 별거아니지만 내부에서 복잡한 일련의 과정들이 DOM을 조작을 통해서 발생하게 되고, 
이것이 1회 2회 수준이 아닌 300회 3000회 이상 넘어가게 되면 엄청난 비용을 치르게 할 것이다. 



그렇기때문에 메타(전 페이스북)에서는 React의 "비교(diffing)"알고리즘을 만들었고 알고리즘 기반으로 컴포넌트가 반환하는 
엘리먼트를 이전에 반환했던 엘리먼트와 재조정(Reconciliation)과정을 거치고 변경된 부분만 DOM에 1번만 적용하는 것이다.



<img width="490" alt="2" src="https://user-images.githubusercontent.com/76759835/191287588-91c15801-ea41-4fec-94e3-d344466f23cc.PNG">



## 결론
Virtual DOM은 DOM을 직접 조작하지 않고 변경사항을 하나의 가상 돔에 모았다가 실제 DOM에 한번만 적용하는 기술이다.




참조
Critical Rendering Path란? : https://wonism.github.io/critical-rendering-path/
React Virtual DOM 이해하기 : https://velog.io/@gwak2837/React-Virtual-DOM-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0
브라우저 동작 원리 : https://aeri-choi.gitbook.io/til/web/browser-workflow
Rect 가 Vitual DOM을 사용하는 이유 : https://velog.io/@woohm402/virtual-dom-and-react
브라우저는 어떻게 동작하는가? : https://d2.naver.com/helloworld/59361
DOM 소개 - WEB API | MDN : https://developer.mozilla.org/ko/docs/Web/API/Document_Object_Model/Introduction
Virtual DOM과 Internals : https://ko.reactjs.org/docs/faq-internals.html
재조정 : https://ko.reactjs.org/docs/reconciliation.html
