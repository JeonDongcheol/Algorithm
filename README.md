Algorithm 기본 정리
====================

## 기본 용어 정리

> Algorithm에서 사용되는 기본적인 개념에 대한 정리

#### Index :
1. [__Time Complexity__](#i1)
2. [__Big O notation__](#i2)
3. [__Best, Average, Worst Cases__](#i3)
4. [__Space Complexity__](#i4)

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

하나의 연산이 **t** 만큼의 시간이 필요하다고 가정했을 때 걸리는 시간

- Case 1 : **2t**
- Case 2 : **(2n + 1)t**
- Case 3 : **(2n^2 + 1)t**

---------------------

### 2. 빅오 표기법 (Big O notation) <a name="i2"/>

시간 복잡도 함수에서 상대적으로 불필요한 연산을 제거하여 알고리즘의 분석을 조금 더 간단하게 할 목적으로 사용하는 시간 복잡도 표기 방법

#### Example

> 시간 복잡도 예시에서 _Case 2*_ 를 대표적인 예시로 함

Case 2의 연삿 횟수 _2n + 1_ 에 추가로 루프 제어문의 연산인 _2n + 2_ 를 더하면 결과적으로 **4n + 3** 의 연산을 필요로 함

하지만 알고리즘의 일반적인 증가 추세로 보았을 때 핵심 포인트는 **n에 정비례** 하여 시간 복잡도가 증가

이를 빅오 표기법을 통해 적용하면 알고리즘의 시간 복잡도를 **O(n)** 이라고 함. 

- 많이 쓰는 빅오 표기법

|빅오 표기법|1|4|8|32|
|:----:|:-----:|:-----:|:----:|:-----:|
|O(1)|1|1|1|1|
|O(log n)|0|2|3|5|
|O(n)|1|4|8|32|
|O(nlog n)|2|8|24|160|
|O(n^2)|1|16|64|1,024|
|O(n^3)|1|64|512|32,768|
|O(2^n)|2|16|256|4,294|
|O(n!)|1|24|40,326|26,313 x 10^33|

![Alt Text][big_o_complexity]

- 빅오 표기법의 예제

1. **O(1)** : 스택에서 Push, Pop

2. **O(log n)** : 이진트리

3. **O(n)** : for 문

4. **O(n log n)** : 퀵 정렬(quick sort), 병합정렬(merge sort), 힙 정렬(heap Sort)

5. **O(n^2)** : 이중 for 문, 삽입정렬(insertion sort), 거품정렬(bubble sort), 선택정렬(selection sort)

6. **O(2^n)** : 피보나치 수열

-------------------

### 3. 최선, 평균, 최악의 경우(Best, Average, Worst Cases) <a name = "i3"/>

동일한 알고리즘도 입력되는 데이터에 따라 실행 시간이 다를 수 있음

ex) 정렬하는 알고리즘에 대부분 정렬이 완료 되어있는 데이터를 입력한다면, 뒤죽박죽 섞여있는 데이터보다 정렬 속도가 더 빠를 것

따라서 **알고리즘의 효율성** 은 입력되는 데이터의 집합에 따라 3가지의 경우로 나누어 평가

- **최선의 경우 (Best Case)** : 실행 시간이 가장 적은 경우
- **평균적인 경우 (Average Case)** : 모든 입력을 고려하고 각 입력이 발생하는 확률을 고려한 평균 수행 시간
- **최악의 경우 (Worst Case)** : 알고리즘의 수행 시간이 가장 오래 걸리는 경우

광범위한 데이터 집합에 대하여 알고리즘을 적용시켜 평균 값을 계싼하는 것은 매우 어렵기 때문에 시간 복잡도의 척도를 계산할 때는 보통 **최악의 경우 (Worst Case)** 를 주로 사용

#### Example

정렬되지 않은 배열을 순차적으로 탐색하여 특정한 값을 찾는 경우

```
int sequencialSearch(int list[], int n, int key) {
	int i;
	for(i = 0; i < n; i++) {
		if(list[i] == key) {
			return i; //탐색에 성공하면 키 값의 Index 반환
		}
	}
	return -1; //탐색에 실패하면 -1 반환
}
```

|값(Value)|위치(Index)|
|:-----:|:-----:|
|5|0|
|8|1|
|9|2|
|15|3|
|23|4|
|48|5|
|7|6|

- Best Case : 찾으려는 값이 배열의 가장 처음에 있는 경우 -> **O(1)**
- Worst Case : 찾으려는 값이 배열의 가장 마지막에 있는 경우 -> **O(n)**

-----------------

### 4. 공간 복잡도 (Sapce Complexity) <a name = "i4"/>

프로그램을 실행시킨 후 완료하는 데 필요로 하는 자원 공간의 양

```
총 공간 요구 = 고정 공간 요구 + 가변 공간 요구
S(P) = c + Sp(n)
```

- **고정 공간** : 입력과 출력의 횟수나 크게와 관계 없는 공간의 요구 _(ex : 코드 저장 공간, 단순 변수, 고정 크기의 구조 변수, 상수...)_
- **가변 공간** : 해결하려는 문제의 특정 인스턴스에 의존하는 크기를 가진 구조화 변수들을 위해서 필요로 하는 공간, 동적으로 필요한 공간 _(ex : 함수가 순환 호출을 할 경우 요구되는 추가 공간...)_

#### Example

```
int factorial(int n) {
	if(n > 1) return n * factorial(n - 1);
	else return 1;
}
```

n이 1 이하일 때까지 함수가 재귀적으로 호출되므로, 스택에는 n부터 1까지 모두 쌓임 -> **O(n)**

```
int factorial(int i) {
	int i = 0;
	int fac = 1;
	for(i = 1; i <= n; i++) {
		fac = fac * i;
	}
	return fec;
}
```

n의 값에는 상관없이 스택에는 n, i, fac 변수만 저장 -> **O(1)**

#### Reference :

- [https://madplay.github.io/post/time-complexity-space-complexity](https://madplay.github.io/post/time-complexity-space-complexity)
- [https://noahlogs.tistory.com/27](https://noahlogs.tistory.com/27)

[big_o_complexity]:https://i.imgur.com/SAcM4Dj.png
