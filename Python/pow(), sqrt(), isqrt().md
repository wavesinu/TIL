### `sqrt()`, `isqrt()`의 차이
sqrt(), isqrt() 모두 제곱근을 계산하는데 사용되지만, 두 함수는 계산 결과와 사용 방법에 몇가지 차이점이 존재한다.

1. `math.sqrt(x)` : x의 제곱근을 계산하고, 결과를 부동소수점 수로 반환한다. x는 **0 이상의 숫자**여야 한다.
	- 만약 x가 음수라면, `ValueError`가 발생한다.
2. `math.isqrt(x)` : x의 제곱근을 계산하고, 결과는 항상 가장 가까운 정수로 내림된다. 즉 소수점 이하를 버리며, x는 항상 **0 이상의 정수**여야 한다.
	- 만약 x가 부동소수점 수라면, `TypeError`가 발생한다.

### 예제

[[정수 제곱근 판별]]
```python
import math  
  
  
def solution(n):  
    return (math.isqrt(n) + 1) ** 2 if math.isqrt(n) ** 2 == n else -1  
  
  
n = int(input())  
print(solution(n))
```

