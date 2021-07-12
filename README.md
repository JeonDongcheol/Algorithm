Algorithm 기본 정리
====================

## 기본 용어 정리

> Algorithm에서 사용되는 기본적인 개념에 대한 정리


#### Index :
1. [__Time Complexity__](#i1)
2. [__Big O notation__](#i2)
3. [__MVC Pattern__](#i5)
4. [__MongoDB__](#i3)

#### Link :
1. [__Tutorial__](./example2/README.md)
2. [__Graduation Project__](./graduation/README.md)

### 1. 시간 복잡도(Time Complexity) <a name="i1"/>

알고리즘을 수행하는 것에 대하여 연산들이 몇 번 이루어지를 숫자로 나타낸 것

여기서 연산은 **산술, 대입, 비교, 이동** 을 말함

연산의 실행 횟수는 보편적으로 입력한 데이터의 개수를 나타내는 n 값에 따라 변하게 되며, 이것을 기반으로 시간 복잡도에 대한 수식을 나타내는 정의는 **T(n)** 이라고 표기

#### Example

> 양의 정수 n을 n 번 더하는 계산을 진행

> 방법에는 n x n 을 해주거나 n을 n 번 더하는 등 여러가지가 존재


```
/* Case 1 */
sum <- n * n;

/* Case 2 */
sum <- 0
for i <- 1 to n do
	sum <- sum + n;

/* Case 3 */
sum <- 0
for i <- 1 to n do
	for j <- 1 to n do
		sum <- sum + 1;
```

|연산종류|Case 1|Case 2|Case 3|
|:-------:|:------:|:------:|:------:|
|대입 연산|1|n + 1|n * n + 1|
|덧셈 연산| |n|n*n|
|곱셈 연산|1| | |
|나눗셈 연산| | | |
|전체 연산 횟수|2|2n + 1|2n^2 + 1|

하나의 연산이 t만큼의 시간이 필요하다고 가정했을 때 걸리는 시간

- Case 1 : 2t
- Case 2 : (2n + 1)t
- Case 3 : (2n^2 + 1)t


### 2. 빅오 표기법 (Big O notation) <a name="i2"/>

시간 복잡도 함수에서 상대적으로 불필요한 연산을 제거하여 알고리즘의 분석을 조금 더 간단하게 할 목적으로 사용하는 시간 복잡도 표기 방법

#### Example

> 시간 복잡도 예시에서 **Case 2** 를 대표적인 예시로 함

Case 2의 연삿 횟수 2n + 1에 추가로 루프 제어문의 연산인 2n + 2를 더하면 결과적으로 **4n + 3** 의 연산을 필요로 함

하지만 알고리즘의 일반적인 증가 추세로 보았을 때 핵심 포인트는 n에 정비례하여 시간 복잡도가 증가

이를 빅오 표기법을 통해 적용하면 알고리즘의 시간 복잡도를 **O(n)** 이라고 함. 

- 많이 쓰는 빅오 표기법

|빅오 표기법|1|4|8|32|
|:----:|:-----:|:-----:|:----:|:-----:|
|O(1)|1|1|1|1|
|O(logn)|0|2|3|5|
|O(n)|1|4|8|32|
|O(nlogn)|2|8|24|160|
|O(n^2)|1|16|64|1,024|
|O(n^3)|1|64|512|32,768|
|O(2^n)|2|16|256|4,294|
|O(n!)|1|24|40,326|26,313 x 10^33|

#### Reference :

- [https://madplay.github.io/post/time-complexity-space-complexity](https://madplay.github.io/post/time-complexity-space-complexity)
