## 캐시란?
캐시는 컴퓨터에서 데이터나 값을 미리 복사해 놓는 임시 장소를 말한다. 
캐시를 사용하는 이유는 캐시의 접근 시간에 비해 원래 데이터를 접근하는 시간이 오래 걸리는 경우나
값을 다시 계산하는 시간을 절약하고 싶은 경우에 사용한다. 캐시에 데이터를 미리 복사해 놓으면 계산이나 
접근 시간 없이 더 빠른 속도로 데이터에 접근할 수 있다. 캐시는 시스템의 효율성을 위해 여러 분야에서 두루 쓰이고 있다.




![memorystructure](https://user-images.githubusercontent.com/76759835/171883918-d0ec44a4-a90d-414d-afc5-2b6c7c0797f4.png)




캐시가 효율적으로 동작하려면, 캐시에 저장할 데이터가 지역성을 가져야 한다. 
지역성이란 데이터 접근이 시간적, 혹은 공간적으로 가깝게 일어나는 것을 의미한다.
1) 시간적 지역성
특정 데이터가 한번 접근되었을 경우, 가까운 미래에 또 한번 데이터에 접근할 가능성이 높은 것을 시간적 지역성이라고 한다
메모리 상의 같은 주소에 여러 차례 읽기 쓰기를 수행할 경우 상대적으로 작은 크기의 캐시를 사용해도 효율성을 꾀할 수 있다.

2) 공간적 지역성
특정 데이터와 가까운 주소가 순서대로 접근되었을 경우를 공간적 지역성이라고 한다. 
CPU 캐시나 디스크 캐시의 경우 한 메모리 주소에 접근할 때 그 주소뿐 아니라 해당 블록을 전부 캐시에 가져오게 된다.
이때 메모리 주소를 오름차순이나 내림차순으로 접근한다면, 캐시에 이미 저장된 같은 블록의 데이터를 접근하게 되므로 캐시의 효율성이 크게 향상 된다.



----------------------------------------------------------------------------------------------------------------



캐시는 언제 적용해야 할까?
원본 데이터에 접근하는데 시간이 오래걸리거나 값을 계산하는데 시간이 오래 걸리는 경우 캐시를 적용하면 처음에는 같은 시간이 걸리지만 똑같은 값을 다시 요청하면 한번에 응답이 가능하다.
