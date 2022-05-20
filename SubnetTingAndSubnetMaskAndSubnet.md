## 서브넷마스크의 개요
21세기에 IPv4 주소의 고갈이 현실화되고 있다. 각국의 NIC(Network Infomation Center)에서는 이를 최대한 늦추기 위하여 
각 라우터가 브로드캐스팅하는 로컬 네트워크 영역에 공인 IP 대역을 호스트가 필요한 만큼만 할당하려는 노력을 하였다.


이러한 NIC 기관의 요구에 맞춰서 IETF에서는 로컬 네트워크 내부에서 접속한 호스트의 IP 대역을 외부 네트워크와 명확하게 
구분할 수 있는 수단을 표준화하였고 이것이 서브넷 마스크(Subnet Mask)이다.






### 서브넷이란?
IP 주소는 네트워크 부분과 호스트 부분으로 나누어진다. 하나의 로컬 네트워크란 하나의 라우터를 거쳐가는 여러개의 연결된 
브로드캐스트 영역이다. 즉, 어떤 네트워크에서 한 노드가 브로드캐스트를 했을 때 그 네트워크의 모든 노드가 신호를 받았다면 
그 네트워크는 하나의 네트워크라고 볼 수 있다. 호스트란 그냥 각각의 노드(PC, 스마트폰 등)들 이다.


정리하자면, 하나의 로컬 네트워크에서는 IP 주소의 네트워크 부분은 같아야 하고, 호스트 부분은 달라야 한다는 것이다.


예를 들자면, A동 아파트의 201호에 있는 사람이 A동 아파트의 501호에 있는 사람을 찾아가려고 할 때 201호 사람은 건물을 나갈 필요가 없다. 
이처럼 쓸데없이 건물을 나갔다오는 불필요한 비용이 없이 효율적인 네트워크 통신과, 브로드캐스팅을 위해 장치들을 일정한 규칙에 따라 하나의 
그룹으로 묶고자 하였고, 이것이 서브넷의 기본 개념이다. 기본적으로 서브넷 내의 호스트는 같은 서브넷의 호스트끼리만 통신이 가능하다.


그렇다면 건물 밖의 대상(=같은 서브넷에 속하지 않은 호스트)를 찾아간다면 어떻게 할까? 
만약 A동 아파트의 201호사람이 B동의 아파트 301호로 찾아간다면 일단은 A동 건물 출입구를 통해 밖으로 나가야 한다. 
출입구가 바로 게이트웨이가 된다. 즉, 게이트웨이가 없다는 것은 출입구가 없다는 것과 동일하다. 또한 B동이 아니라 C동, D동 또는 
다른 지역을 가더라도 출입구(게이트웨이)를 나가는 행위는 동일하게 적용된다. 그러므로, 통신하고자 하는 대상 호스트가 현재 장치가 
속한 네트워크의 서브넷의 범위를 벗어나는 경우에는 게이트웨이를 통해 해당 네트워크 밖으로 나간 후, 여러 라우터를 거치며 대상 호스트가 
속한 네트워크를 찾아내는 식으로 통신이 이루어진다.


그리고 서브넷 마스크는 이런 서브넷을 구분하는 방법 중 하나이다. 위의 아파트 예시에서 서브넷 마스크는 아파트의 동 건물 한채라고 보면 된다. 
이 범위 밖에 있는 장치들은 모두 같은 건물이 아니다. 즉, 로컬 네트워크가 아니다.


따라서 이 서브넷 마스크를 어떤 범위로 하느냐에 따라서 로컬 네트워크 범위가 넓어지기도, 좁아질 수도 있다. 아파트 전체가 같은네트워크 일수도,
1층라만 일 수도, 한 단지 전체일 수도 있는 것이다.





![subnetting](https://user-images.githubusercontent.com/76759835/169008881-35b6dba0-f85e-49db-a406-f58e543f0ef8.JPG)



### 서브네팅이란?
"네트워크 관리자가 네트워크 성능을 향상시키기 위해, 자원을 효율적으로 분배하는 것이다. 여기서 자원을 효율적으로 분배한다는 것은 네트워크 
영역과 호스트 영역을 분할 하는 것이라고 생각하면 된다." 


네트워크적인 측면에서 말하자면, 너무 큰 브로드캐스트 도메인은 네트워크 환경에서 패킷전송을 느리게하고 성능저하를 발생시킨다. 
따라서 네트워크를 쪼개서 통신 성능을 보장하는 것이다. 또한 IP는 32자리 2진수로 표현할 수 있는데 이 말은 결국 최대 2^32만큼의 
표현만 가능하다는 뜻이다. 


즉, 자원의 한계가 존재한다는 뜻이고 결국 제한적인 자원으로 인해 주소에 낭비 없이 아껴써야 한다. 그래서 등장한 것이 서브넷마스크이다.


서브네팅은 많은 측면에서 장점이 존재한다.
- 관리하기 쉬움
- 고급 네트워크 보안
- 네트워크 트래픽 감소
- 네트워크 서브네팅 시 인터넷 서비스 업체(ISP)로부터 추가 IP 주소를 받을 필요가 없음


서브네팅에는 이처럼 많은 장점이 있긴 하지만 서브네팅을 위해 추가 하드웨어가 필요한 경우가 종종 있기에 추가 비용이 들 수 있다는 단점도 존재한다.






![subnet-mask](https://user-images.githubusercontent.com/76759835/169008918-ca31a4b2-d324-4ccb-9ecd-28b6f5aa3f43.JPG)



### 서브넷 마스크란?
필요한 네트워크 주소만 호스트 IP로 할당할 수 있게 만들어 네트워크 낭비를 방지한다. 
이를 전문용어로 서브네팅이라 하며 그 반대는 슈퍼네팅이라고 한다.


IP주소는 무작위로 숫자를 나열한 것처럼 보일 수 있지만, 로직으로 이루어져있다. 
IP 주소를 나눈 작은 네트워크 조각을 서브넷 마스크(subnet mask)라고 부른다. 
서브넷 마스크는 32비트의 숫자로 '0'의 비트는 호스트 부분을 나타내고 '1'의 비트는 네트워크 부분을 나타낸다. 
이러한 방식으로 서브넷 마스크는 IP 주소를 네트워크 및 호스트 주소와 분리한다. 
서브넷마스크는 기본적으로 자체 32비트 숫자를 이용하여 IP주소를 마스킹하기 때문에 여기서 '마스크'라는 단어가 이용된다.