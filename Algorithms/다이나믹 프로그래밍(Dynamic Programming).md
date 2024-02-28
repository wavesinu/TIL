동적계획법(다이나믹 프로그래밍, Dynamic Programming)이란 큰 문제에 대한 답을 얻기 위해 동일한 문제이지만, 크기가 더 작은 문제들을 먼저 해결한 뒤, 그 결과들을 이용해 큰 문제를 비교적 간단하게 해결하는 기법이다.

동적계획법을 구현하는 방법은 다음의 2가지 방법이 있다.
1. **for loop을 이용**
2. **재귀함수를 이용**

# 메모이제이션(Memoization)
동적계획법으로 해결하기 위한 방법 중 하나로 재귀함수가 가능하다. 예를 들어 피보나치 수열에서 n번째 원소의 값을 재귀함수를 이용해 구할 수 있다.
```python
def fibbo(n):
	if n <= 2:
		return 1
	else:
		return fibbo(n - 1) + fibbo(n -2)
```
그러나, 이 코드를 통해 50번째 수를 구하면, 시간이 오래 걸린다.

```python
n = 6
memo = [-1] * (n+1)

def fibbo(n):
	# 이미 n번째 값을 구해본 적이 있다면
	# memo에 적혀있는 값을 반환한다.
    if memo[n] != -1:
        return memo[n]

	if n <= 2:
		memo[n] = 1
    # 점화식을 이용하여 답을 구한 뒤
    # 해당 값을 memo에 저장한다.
	else:
		memo[n] = fibbo(n - 1) + fibbo(n -2)
```
