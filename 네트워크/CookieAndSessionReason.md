## HTTP의 특징으로 인한 쿠키와 세션을 사용하는 이유

- HTTP 프로토콜의 특성이자 약점을 보완하기 위해서 쿠키 또는 세션을 사용한다.
기본적으로 HTTP 프로토콜 환경은 "connectionless, stateless"한 특성을 가지기 때문에 
서버는 클라이언트가 누구인지 매번 확인해야 한다. 이 특성을 보완하기 위해서 쿠키와 세션을 사용한다.



### Connectionless(비연결 지향)란?


클라이언트가 요청을 한 후 응답을 받으면 그 연결을 끊어버리는 특징이 있다.
HTTP는 먼저 클라이언트가 request를 서버에 보내면, 서버는 클라이언트에게 요청에 맞는 response를 보내고 
접속을 끊는 특성이 있다. 헤더에 keep-alive라는 값을 줘서 커넥션을 재활용하는데 HTTP1.1에서는 이것이 디폴트다.


HTTP가 tcp위에서 구현되었기 때문에 네트워크 관점에서 keep-alive는 옵션으로 connectionless의 연결비용을 줄이는 
것을 장점으로 비연결지향이라 한다.






### Stateless(무상태)란?


클라이언트와 서버 관계에서 서버가 클라이언트의 상태를 보존하지 않음을 의미한다.
연결을 끊는 순간 클라이언트와 서버의 통신이 끝나며 상태 정보를 유지하지 않는 특성이 있다.
쿠키와 세션은 위의 두 가지 특징을 해결하기 위해 사용된다. 예를 들어, 쿠키와 세션을 사용하지 않으면 쇼핑몰에서 
옷을 구매하려고 로그인 했음에도, 페이지를 이동할 때 마다 계속 로그인을 해야 한다.
쿠키와 세션을 사용했을 경우, 한 번 로그인 하면 어떠한 방식에 의해서 그 사용자에 대한 인증을 유지하게 된다.




## 쿠키(Cooki)란?
쿠키란 하이퍼 텍스트의 HTTP의 일종으로서 인터넷 사용자가 어떠한 웹사이트를 방문할 경우 그 사이트가 사용하고 
있는 서버를 통해 인터넷 사용자의 컴퓨터에 설치되는 작은 데이터 파일이다. 웹사이트는 쿠키를 통해 접속자의 장치를 
인식하고, 접속자의 개인장치에 다운로드 되고 브라우저에 저장되는 키와 값의 형태를 가진 파일이다.


HTTP 쿠키, 웹 쿠키, 브라우저 쿠키라고도 한다. 이 기록 파일에 담긴 정보는 인터넷 사용자가 같은 웹사이트를 방문할 때마다 
읽히고 수시로 새로운 정보로 바뀐다. 쿠키는 넷스케이프의 프로그램 개발자였던 루 몬툴리가 고안한 뒤로 오늘날 많은 서버 및
웹사이트들이 브라우저의 신속성을 위해 즐겨 쓰고 있다.


쿠키는 소프트웨어가 아니며, 컴퓨터 내에서 프로그램처럼 실행될 수 없고 바이러스를 옮길 수도, 악성코드를 설치할 수도 없다.
하지만 스파이웨어를 통해 유저의 브라우징 행동을 추적하는데에 사용될 수 있고, 누군가의 쿠키를 훔쳐서 해당 사용자의 웹 계정 
접근권한을 획득할 수 있다. 일반적으로 쿠키에는 만료일이 있다. 예를 들어, 브라우저를 닫는 경우 자동으로 삭제되는 쿠키도
있으며(세션 쿠키), 일부는 수동으로 삭제되기 전까지 남아있는 등 더 오랜기간 동안 컴퓨터에 저장되는 쿠키도 있다(지속적 쿠키). 


쿠키는 일반적으로 이름, 주소, 장바구니의 내용, 웹 페이지의 기본 레이아웃, 보고있는 지도 등 개인 등록 데이터를 저장하는데 사용된다. 
쿠키를 사용하면 웹 서버가 웹사이트를 방문 할 때 특정 요구 사항과 기본 설정에 맞게 정보를 쉡게 사용자 지정할 수 있다.




### 쿠키의 특징
- 쿠키는 클라이언트 로컬에에 저장되는 키와 값의 작은 데이터 파일이다.
- 사용자 인증이 유효한 시간을 명시할 수 있으며, 유효 시간이 정해지면 브라우저가 종료되어도 유지된다는 특징이 있다.
- 쿠키는 클라이언트의 상태 정보를 로컬에 저장했다가 참조한다.
- Response Header에 Set-Coolie 속성을 사용하면 클라이언트에 쿠키를 만들 수 있다.
- 쿠키는 클라이언트의 상태정보를 로컬에 저장했다가 참조한다.
- 쿠키는 사용자가 따로 요청하지 않아도 브라우저가 Request시에 Request Header를 넣어서 자동으로 서버에 전송한다.




### 쿠키의 동작 방식
1. 클라이언트가 페이지를 요청
2. 서버에서 쿠키를 생성
3. HTTP 헤더에 쿠키를 포함 시켜 응답
4. 브라우저가 종료되어도 쿠키 만료 기간이 있다면 클라이언트에서 보관하고 있음
5. 같은 요청을 할 경우 HTTP 헤더에 쿠키를 함께 보낸다.
6. 서버에서 쿠키를 읽어 이전 상태 정보를 변경 할 필요가 있을 때 쿠키를 업데이트하여 변경된 쿠키를 HTTP 헤더에 포함시켜 응답




### 쿠키의 구성 요소
- 이름 : 각각의 쿠키를 구별하는 데 사용되는 이름
- 값 : 쿠키의 이름과 관련된 값
- 유효시간 : 쿠키의 유지시간
- 도메인 : 쿠키를 전송할 도메인
- 경로 : 쿠키를 전송할 요청 결로



## 세션(Session)이란?
세션이란 일정 시간동안 같은 사용자(정확하게 브라우저를 의미)로 부터 들어오는 일련의 요구를 하나의 상태로 
보고 그 상태를 일정하게 유지시키는 기술이다. 또한 여기서 일정 시간이란 방문자가 웹 브라우저를 통해 웹 서버에
접속한 시점으로부터 웹 브라우저를 종료함으로써 연결을 끝내는 시점을 말한다. 즉, 방문자가 웹서버에 접속해 있는 
상태를 하나의 단위로 보고 그것을 세션이라고 한다. 


상호작용적인 정보 교환을 전제하는 둘이상의 통신 장치나 컴퓨터와 사용자 간의 대화나 송수신 연결상태를 의미하는 
보안적인 다이얼로그 및 시간대를 가리킨다. 따라서 세션은 연결상태를 유지하는것보다 연결상태의 안정성을 더 중요시 하게 된다.


그렇기 때문에 세션은 쿠키를 기반하고 있지만, 사용자 정보 파일을 브라우저에 저장하는쿠키와 달리 세션은 서버 측에서 관리한다. 
서버에서는 클라이언트를 구분하기 위해 세션 ID를 부여하며 웹 브라우저가 서버에 접속해서 브라우저를 종료하 때까지 인증상태를 
유지한고,접속 시간에 제한을 두어 일정 시간 응답이 없다면 정보가 유지되지 않게 설정이 가능하다.


사용자에 대한 정보를 서버에 두기 때문에 쿠키보다 보안에 좋지만, 사용자가 많아질수록 서버 메모리를 많이 차지하게 된다. 
(즉, 동접자 수가 많은 웹사트인 경우 서버에 과부하를 주게 되므로 성능 저하의 요인이 된다.)


클라이언트 Request를 보내면, 해당 서버의 엔진이 클라이어트에게 유일한 ID를 부여하는 데 이것이 세션 ID이다.




### 세션의 특징
- 각 클라이언트에게 고유 ID를 부여
- 세션 ID로 클라이언트를 구분해서 클라이언트의 요구에 맞는 서비스를 제공
- 보안 면에서 쿠키보다 우수
- 사용자가 많아질수록 서버 메모리를 많이 차지하게 됨
- 저장 데이터에 제한이 없다.


### 세션 동작순서
1. 클라이언트 요청 (사용자가 웹사이트 접근)
2. 서버는 접근클라이언트의 Request-Header필드인 cookie를 확인하여, 클라이언트가 해당 세션ID를 보냈는지 확인
3. 세션ID가 존재하지 않는다면, 서버는 세션ID를 생성해 클라이언트에게 전송
4. 서버에서 클라이언트로 준 세션 ID를 쿠키를 사용해 서버에 저장한다.
5. 클라이언트는 재접속시, 이 쿠키를 이용하여 세션 ID값을 서버에 전달한다.





## 쿠키와 세션의 차이
- 쿠키는 서버의 자원을 전혀 사용하지 않으며, 세션은 서버의 자원을 사용한다.
- 보안 면에서 세션이 더 우수하며, 요청 속도는 쿠키가 세션보다 더 빠르다.
   (세션은 서버의 처리가 필요하기 때문)
- 쿠키는 클라이언트 로컬에 저장되기 때문에 변질되거나 request에서 스니핑 당할 우려가 있어서 
  보안에 취약하지만, 세션은 쿠키를 이용해서 sessionid만 저장하고 그것으로 구분해서 서버에서 
  처리하기 때문에 비교적 보안성이 좋다.
- 쿠키도 만료시간이 있지만 파일로 저장되기 때문에 브라우저를 종료해도 계속해서 정보가 남아 있을 
  수 있다. 또한 만료기간을 넉넉하게 잡아두면 쿠키삭제를 할 때 까지 유지될 수도 있다. 반면에 세션은 
  만료시간을 정할 수 있지만 브라우저가 종료되면 만료시간에 상관없이 삭제된다.
- 세션은 정보가 서버에 있기 때문에 처리가 요구되어 비교적 느린 속도를 낸다.



### 세션의 사용 

세션은 서버에 자원을 사용하기 때문에 무분별하게 만들다보면 서버의 메모리가 감당할 수 없어질 수가 있고 속도가 느려질 수 있기 때문에 상황에 적합하게 세션을 사용해야 한다.
