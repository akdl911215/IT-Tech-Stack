## HTTP(HyperText Transfer Protocol)
HTTP는 웹상에서 클라이언트와 서버 간에 요청/응답으로 HTML 문서와 같은 리소스들을 가져올 수 있도록 해주는 프로토콜이다. 
HTTP는 웹에서 이루어지는 교환의 기초이며, 클라이언트-서버 프로토콜이기도 하다. 클라이언트가 HTTP 프로토콜을 통해 서버에게 요청을
보내면 서버는 요청에 맞는 응답을 클라이언트에게 전송한다. 하나의 완전한 문서는 텍스트, 레이아웃 설명, 이미지, 비디오, 스크립트 등 
불러온(fetched) 하위 문서들로 재구성 된다.
클라이언트와 서버들은 개별적인 메시지 교환에 의해 통신한다. 보통 브라우저인 클라이언트에 의해 전송되는 메시지를 요청(requests)이라고 
부르며, 그에 대해 서버에서 응답으로 전송되는 메시지를 응답(responses)이라고 부른다. 1990년대 초에 설계된 HTTP는 거듭하여 진화해온 확장
가능한 프로토콜이다. HTTP는 애플리케이션 계층의 프로토콜로, 신뢰 가능한 전송 프로토콜이라면 이론상으로는 무엇이든 사용할 수 있으나 TCP 
혹은 암호화된 TCP 연결인 TLS를 통해 전송된다. HTTP의 확장성 덕분에, 오늘날 하이퍼텍스트 문서 뿐만 아니라 이미지와 비디오 혹은 HTML 폼 결과와 
같은 내용을 서버로 포스트(POST)하기 위해서도 사용된다. HTTP는 또한 필요할 때마다 웹 페이지를 갱신하기 위해 문서의 일부를 가져오는데 사용될 수 있다.










## HTTPS
HTTP의 본안 취약점을 해결한 HTTP 프로토콜의 보안 버전이다. HTTP에 S(Secure Socket)가 추가되어 HTTPS가 된것이다. 
HTTPS는 기본 골격이나 사용 목적 등은 HTTP와 거의 동일하지만, 데이터를 주고 받는 과정에 SSL/TLS 프로토콜 암호화 및 
인증을 사용함으로써 '보안'요소가 추가되었다는 것이 가장 큰 차이점이다.
HTTPS를 사용하면 서버와 클라이언트 사이의 모든 통신 내용이 암호화된다. HTTPS는 위와 같은 상황에서 페이지를 암호화한 키가 
그 페이지를 보는 특정 사용자에게만 알려지도록 한다. HTTPS 프로토콜을 사용하면 웹 사이트 사용자가 인터넷을 통해 신용 카드 번호,
은행 정보 및 로그인 자격 증명과 같은 중요한 데이터를 안전하게 전송할 수 있다. 이러한 이유로 HTTPS는 쇼핑, 뱅킹 및 원격 작업과 
같은 온라인 활동을 보호하는데 특히 중요하다. 그렇기 때문에 HTTPS는 빠르게 표준 프로토콜이 되고 있다.










<img width="898" alt="GET" src="https://user-images.githubusercontent.com/76759835/165109318-ecb94cb3-30f6-4bc4-9b5c-8907a3347843.png">


## GET
GET 방식은 HTTP/1.1 스펙인 RFC2616의 Section9.3에 따르면 GET은 서버로부터 정보를 조회하기 위해 설계된 메소드이다.


클라이언트가 서버로 데이터를 요청하기 위해 사용되는 Method이며 GET 요청을 할 때는 Body 부분은 비어있고 헤더에 Body의 
콘텐츠 타입을 명시하는 Content-Type 헤더 필드도 적지 않는다. URL 뒤에 쿼리스트링을 통해 전송한다. URL의 끝에 ?와 함께 
이름(name)과 값(value)으로 쌍을 이루는 요청 파라미터를 쿼리스트링이라고 부른다. 만약, 요청 파라미터가 여러개일 경우에는 
&로 연결한다. 쿼리스트링을 사용하게 되면 URL에 조회 조건을 표시하기 때문에 특정 페이지를 링크하거나 북마크한다.


쿼리스트링을 포함한 URL의 샘플은 아래와 같다. 여기서 요청 파라미터명은 name1, name2이고, 각각의 파라미터는 value1, 
value2라는 값으로 서버에 요청을 보내게 된다.

  www.example.com/resouces?name1=value1&name2=value2  
  
  
그리고 GET은 불필요한 요청을 제한하기 위해 요청이 캐시될 수 있다. js, css, image 같은 정적 컨텐츠는 데이터양이 크고, 
변경될 일이 적어서 반복해서 동일한 요청을 보낼 필요가 없다. 정적 컨텐츠를 요청하고 나면 브라우저에서는 요청을 캐시해두고, 
동일한 요청이 발생할 때 서버로 요청을 보내지 않고 캐시된 데이터를 사용한다. 





<img width="896" alt="POST" src="https://user-images.githubusercontent.com/76759835/165109354-928d8391-515b-422c-b10c-dec45f707dad.png">






## POST
POST는 리소스를 생성/변경하기 위해 설계되었기 때문에 GET과 달리 전송해야될 데이터를 HTTP 메세지의 Body에 담아서 전송한다. 
HTTP 메세지의 Body는 길이의 제한없이 데이터를 전송할 수 있다. 그래서 POST 요청은 GET과 달리 대용량 데이터를 전송할 수 있다. 
이처럼 POST는 데이터가 Body로 전송되고 내용이 눈에 보이지 않아 GET 보다 보안적인 면에서 안전하다고 생각할 수 있지만, 
POST 요청도 크롬 개발자도구, Fiddler와 같은 툴로 요청 내용을 확인할 수 있기 때문에 민감한 데이터의 경우에는 반드시 암호화해 전송해야 한다.


그리고 POST로 요청을 보낼 때는 요청 헤더의 Content-Type에 요청 데이터 타입을 표시해야 한다. 데이터 타입을 표시하지 않으면 
서버는 내용이나 URL에 포함된 리소스의 확장자명 등으로 데이터 타입을 유추한다. 만약, 알 수 없는 경우에는
application/octet-stream 으로 요청을 처리한다.

### application/octet-stream란?
MIME의 개별 타입 중 application에 속하는 8비트 단위의 binary data이다. 특별히 표현할 수 있는 프로그램이 존재하지 
않는 데이터의 경우 기본값으로 octet-stream을 사용한다. Content-Disposition 헤더를 attachment로 줌으로써 해당 데이터를 
수신받은 브라우저가 파일을 저장 또는 다른이름으로 저장 여부를 설정할 수 있다.


### mdn application/octet-stream 정의
다른 모든 경우를 위한 기본값이다. 알려지지 않은 파일 타입은 이 타입을 사용해야 한다. 브라우저들은 이런 파일들을 다룰 때, 
사용자를 위험한 동작으로부터 보호하도록 개별적인 주의를 기울여야 한다.


### Content-Dispotion이란?
HTTP Response 헤더의 종류. 브라우저에 Content가 inline으로 표시되야 하는 웹페이지 자체이거나 웹페이지의 일부인지, 
attachment로써 다운로드 되거나 로컬에 저장될 용도로 쓰이는 것인지 알려주는 헤더이다.









<img width="665" alt="비교표" src="https://user-images.githubusercontent.com/76759835/165109365-e2fd9054-bcea-4553-86ed-1f74d024dc8b.png">


## GET과 POST의 차이
GET은 Idempotent, POST는 Non-idempotent하게 설계되어 있다.
Idempotent(멱등)은 수학적 개념으로 다음과 같이 나타낼 수 있다.
수학이나 전산학에서 연산의 한 성질을 나타내는 것으로. 연산을 여러 번 적용하더라도 겨과가 달라지지 않는 성질


즉, 멱등이라는 것은 동일한 연산은 여러번 수행하더라도 동일한 결과가 나와야 한다. 여기서 GET이 Idempotent하도록 
설계되었다는 것은 GET으로 서버에게 동일한 요청을 여러 번 전송하더라도 동일한 응답이 돌아와야 한다는 것을 의미한다. 
이에 따라 GET은 설계원칙에 따라 서버의 데이터나 상태를 변경시키지 않아야 Idempotent하기 때문에 주로 조회를 할 때에 
사용해야 한다. 예를 들어, 브라우저에서 웹페이지를 열어보거나 게시글을 읽는 등 조회를 하는 행위는 GET으로 요청하게 된다.


반대로 POST는 Non-idempotent하기 때문에 서버에게 동일한 요청을 여러 번 전송해도 응답은 항상 다를 수 있다. 이에 따라 
POST는 서버의 상태나 데이터를 변경시킬 때 사용된다. 게시글을 쓰면 서버에 게시그이 저장이 되고, 게시글을 삭제하면 해당 
데이터가 없어지는 등 POST로 요청을 하게 되면 서버의 무언가는 변경되도록 사용된다. 이처럼 POST는 생성, 수정, 삭제에 사용할 수 있다. 
그렇지만, 생성에는 POST, 수정은 PUT || PATCH, 삭제는 DELETE 가 더 용도에 맞는 메소드이다.





[이정현 블로그 구경 https://akdl911215.tistory.com/409](https://akdl911215.tistory.com/409)
