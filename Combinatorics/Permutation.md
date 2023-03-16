# Permutation
---

## Basic Permutation
<br>

순열은 순서가 부여된 임의의 집합을 다른 순서로 뒤섞는 연산이다. 순열의 수는 다음과 같이 나타낸다.

$$
nPr = n(n-1)(n-2)...(n - r + 1)
$$

우리의 주 관심사는 알고리즘 문제에서 탐색해야하는 Case, 즉 순열군을 구하는데 있다. Brute Froce와 밀접하며, 그렇기 때문에 Pruning을 염두해 두어야한다. 

내장 함수 `itertools` 를 쓰면 참 편하지만, 문제의 요구사항에 맞게 구현해야 될 수도 있기 때문에(시간 복잡도), 직접 구현해 보자.

```python

n, r = 3, 2
arr = [1, 2, 3]
choose = [0] * n
ans = []

def permutation1(r):
    if r == 0:
        print(ans)
    else:
        for i in range(n):
            if not choose[i]:
                ans.append(arr[i])
                choose[i] = 1
                permutation(r - 1)
                choose[i] = 0
                ans.remove(arr[i])


def permutation2(idx):
    if idx == n:
        print(ans)
    else:
        for i in range(idx, n):
            arr[idx], arr[i] = arr[i], arr[idx]
            permutation2(idx + 1)
            arr[idx], arr[i] = arr[i], arr[idx]
            
permutation2(r)
```
---

- 중복 순열의 경우 permutation1에서 choose를 기억할 필요가 없다.
$$
n\Pi r = n^r
$$

yield를 사용하면 간편하게 구현할 수 있다.

```python 
n, r = 3, 2
arr = [1, 2, 3]

def perm_repeatation:
    for i in range(n):
        if r == 1:
            yield arr[i]
        else:
            for choose in perm_repeatation(r - 1):
                yield [arr[i]] + [choose]

for p in perm_repeatation(r):
    print(p)

```
