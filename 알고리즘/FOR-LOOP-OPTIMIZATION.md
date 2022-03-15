### for 문 ++i 와 i++ 차이

for문에서 ++i와 i++의 차이는 속도이다. 내부 operator 로직을 보면 i++ 연산이 한번 더 연산을 거치게 된다. 
물론 요즘 컴파일러와 하드웨어가 워낙 빨라져서 거의 차이가 없지만 ++i가 미세하게 빠르다.

코드로 확인해보자. C계열에서 확인해보면 i++의 경우에 임시 변수를 생성하기 때문이다.


<pre>
<code>
1) ++i 의 경우
for (int i = 0; i < 1000; ++i) {
	printf("n = %d ", i);
}
operator 코드
int int::operator++() {
	this = this + 1;
	return this;
}
2) i++ 의 경우
for (int i = 0; i < 1000; i++) {
	printf("n = %d ", i);
}
operator 코드
int int::operator++() {
	int returnval = this;
	i = i + 1;
	return returnval;
}

</clode>
</pre>
