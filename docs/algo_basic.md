# 1. 알고리즘 기초
---

## Brute Force
<br>

- 알고리즘 문제에 있어, 해가 존재할 수 있는 모든 영역을 탐색하는 단순 완전 탐색 방법이다. 

- 알고리즘이 직관적이고, 확실한 해를 구할 수 있다는 장점이 있다. 

- 알고리즘 실행 시간이 매우 오래걸린다. 
<br><br>

넓은 의미로는 모든 완전 탐색 알고리즘으로 볼 수 있지만, 일반적으로 선형문제에 국한하고 단순 완전 탐색을 의미한다. 따라서 Brute Force는 __문제를 선형구조화 하고, 탐색하는 것이 핵심이다.__


Brute Force에 비해 비교적 효율적인 완전 탐색 알고리즘으로는 Bitmasking, Permutation, Recursive Function, BFS, DFS가 있다.
<br>

```Markdown
     - - - [선형 구조를 가진 Brute Froce 문제] - - -

         1018 체스판 다시 칠하기     1065 한수  
         2798 블랙잭                7568 덩치        
```
<br>

---
## Recursion


### __Reductions__ 

Recursion(재귀)에 대해 바로 설명하기 전에 Reduction(환원)에 대해 잠깐 짚고 넘어가자. 보통 Reduction개념은 P, NP, NP-hard 문제를 다룰 때 나온다. 



>두 문제 X, Y에 대해 X를 polynomial time(다항 시간)안에 풀 수 있고, Y문제를 polynomial time 안에 X문제로 바꿀 수 있다면, Y는 X로 polynomial-time reducible 하다.

여기서 polynomial time(다항 시간)이란 $n^k + ...$ 로 표현된다. 주로 $2^n$ 과 같은 exponential time(지수 시간)과 구분되어 사용된다. 


Reduction의 정확한 예는 아니지만, 곱셈은 더하기를 여러번 함으로써 풀 수 있다. 핵심은 지수 시간을 가지는 문제를 다항 시간문제로 변환하는데 있고, Recursion은 강력한 Reduction의 한 예로 볼 수 있다.
<br><br>

### __Recursive Function__

Recursive Function은 자기 자신을 호출 하는 함수로 정의된다. 단순히 반복되는 작업을 할당하여 알고리즘을 구성할 수 있지만, 그러면 Brute Force를 사용하는 것과 구분되지 않는다. 
<br>

바로 연상되지는 않지만, 위에서 설명한 Reduction의 개념으로 접근하면, 재귀는 동일한 문제를 풀 수 있는 문제로 환원 되어야한다. __호출될 수록 쉬워지거나, 차수가 낮아져야 한다.__ 
<br><br>

> 핵심은 __귀납적 사고__ 에 있다. 

<br>

$f(n)$ 다양한 $f(a(n-b))$ 조합으로 나누어 구현하는 과정에서 Recursive Function이 활용된다. 

```
 - - - [Recursive Function을 사용하여 푸는 문제들] - - -

        Finbonachi Number, Tower of Hanoi
        Fast Multiplication(Karatsuba)
        Merge Sort, Quik sort
```


- c, java, python 에서 재귀함수는 호출될 때마다 스택 프레임으로 쌓이게 되므로 Depth가 깊어지면 stackoverflow가 발생 할 수 있다.

- 따라서 무한 호출이 되지않게 Stop point를 설정하거나,  Memoization을 통해 중복연산을 줄여 리소스 낭비를 줄여야한다.
