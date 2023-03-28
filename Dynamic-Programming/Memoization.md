# Memoization
- 동일한 연산을 반복적으로 해야 할 때, **이전에 게산한 값을 메모리에 저장**함으로써 중복되는 계산을 제거하여 실행 속도를 빠르게 해주는 기법
- DP(Dynamic Programming, 동적계획법)의 핵심이 됨
- 메모리 공간을 희생하고 수행 속도를 향상

### [ 수행 가능한 조건 ]
1. 연산에 있어 많은 메모리를 사용하지 않는 함수
2. 같은 입력에 대해 같은 출력을 내는 함수
3. 반복되는 함수 결과 값 사용

# Recursive Function
- 내부적으로 자기 자신을 호출하는 함수
- **반드시 종료조건이 필요함**
- 재귀 호출을 너무 많이 하게 되면 stack overflow 발생

### [ 재귀함수를 구현할 때 고려할 것 ]
1. 결과를 향한 방향 
  - 정방향/역방향
2. 반환값 
  - 있음/없음
3. 종료 조건


# 피보나치 수열 예제
![image](https://user-images.githubusercontent.com/108309396/228179231-fb1ac314-b4c1-4c89-93df-e3353eda551a.png)  
&rarr; 연산이 중복됨

## Memoization
```python
dic = {1:1, 2:1}
def fib_memoization(n):
  if n in dic:
    return dic[n]
  
  dic[n] = fib_memoization(n-1) + fib_memoization(n-2)
  return dic[n]
```

## Recursive Function
```python
def fib_recursive(n):
  if n == 1:
    return 1
  elif n == 2:
    return 1
  else:
    return fib_recursive(n-1) + fib_recursive(n-2)
```