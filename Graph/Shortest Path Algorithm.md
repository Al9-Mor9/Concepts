# Bellman Ford Algorithm
## 📌요약
![Bellman–Ford_algorithm_example](https://user-images.githubusercontent.com/108309396/224858733-ce1ddd0b-c5c4-466b-9973-50bad7c40aee.gif)
- E번의 매 단계마다 모든 간선을 전부 확인하면서 하나의 정점에서 모든 정점으로 가는 최단 거리를 구함
  - 다익스트라와 차이점은 매 반복마다 "모든" 간선을 확인한다는 점이다.
  - 다익스트라는 방문하지 않은 노드 중에서 최단 거리가 가장 가까운 노드만을 방문함
- 음수 간선이 있어도 최적의 해를 찾을 수 있다.
  - 음수 간선의 순환 감지 가능
- 시간 복잡도가 느림 &rarr; $O(VE)$
  - V번 반복에 대해서 해당 정점과 연결되어 있는 모든 간선(E)를 탐색하기 때문

## 📌벨만-포드 알고리즘 수행과정
1. 출발 노드 설정
2. 최단 거리 테이블 초기화
3. 다음 과정을 V-1(=E)번 반복
   1. 모든 간선 E개를 하나씩 확인
   2. 각 간선을 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블 갱신
   3. V-1까지 단계를 진행하면 모든 노드에 대한 최단 거리가 확정된다.
\* 음수 간선이 발생하는지 확인하고 싶다면 3번 과정을 "한 번 더" 수행  
&rarr; 이 때 최단 거리 테이블이 갱신된다면 음수 간선 순환이 존재하는 것이다. 

## 📌Implement (Answer of BOJ 11657)
```python
import sys

input = sys.stdin.readline
INF = int(1e9)

# 노드의 개수, 간선의 개수를 입력
v, e = map(int, input().split())
# 모든 간선에 대한 정보를 담는 리스트 만들기
edges = []
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF] * (v + 1)

# 모든 간선의 정보 입력
for _ in range(e):
    a, b, c = map(int, input().split())
    # a번 노드에서 b번 노드로 가는 비용이 c라는 의미 (a -> b 의 비용이 c)
    edges.append((a, b, c))


def bellman_ford(start):
    # 시작 노드에 대해서 초기화
    distance[start] = 0
    # 전체 v - 1번의 라운드(round)를 반복
    for i in range(v):
        # 매 반복마다 '모든 간선'을 확인한다.
        for j in range(e):
            cur_node = edges[j][0]
            next_node = edges[j][1]
            edge_cost = edges[j][2]
            # 현재 간선을 거쳐서 다른 노드로 이동하는 거리가 더 짧은 경우
            if distance[cur_node] != INF and distance[next_node] > distance[cur_node] + edge_cost:
                distance[next_node] = distance[cur_node] + edge_cost
                # v번째 라운드에서도 값이 갱신된다면 음수 순환이 존재
                if i == v - 1:
                    return True
    return False


# 벨만 포드 알고리즘 수행
negative_cycle = bellman_ford(1)

# 음수 순환이 존재하면 -1 출력
if negative_cycle:
    print("-1")
else:
    # 1번 노드를 제외한 다른 모든 노드로 가기 위한 최단 거리를 출력
    for i in range(2, v + 1):
        # 도달할 수 없는 경우, -1 출력
        if distance[i] == INF:
            print("-1")
        # 도달할 수 있으면 거리 출력
        else:
            print(distance[i])
```


# Floyd-Warshall Algorithm
## 📌요약
- 한 번 실행하여 모든 노드 간 최단 경로를 구하는 알고리즘
- 음의 간선이 포함된 그래프에서도 사용 가능
- 알고리즘은 여러 라운드로 구성
  - 라운드마다 각 경로에서 새로운 중간 노드를 선택하고, 더 짧은 길이를 선택하는 과정을 반복
- 시간 복잡도는 $O(V^3)$

## 📌플로이드-워셜 알고리즘 수행과정
1. 모든 노드 간 최단 거리를 구해야 하므로 2차원 인접 행렬 구성
  - 방향이 없을 경우 (1, 4), (4, 1)에 모두 적용, 방향이 있을 경우 (1, 4)에만 적용
2. 그래프의 노드와 간선에 따라 최단 거리 테이블을 갱신한다.
3. 점화식을 적용하며 매 라운드마다 최단 거리 테이블을 갱신한다. a는 출발노드, b는 도착노드, k는 중간노드
![image](https://user-images.githubusercontent.com/108309396/224861005-e1a19e02-01c1-49ef-97e0-acbe78174006.png)

### [step 0] 초기 그래프의 노드와 간선에 따라  최단 거리 테이블을 갱신한다.
![image](https://user-images.githubusercontent.com/108309396/224861119-6f6a2e86-1f37-460f-b09c-787e4c23bfd4.png)  
- 이동 가능한 간선이 없을 시 INF, 제자리는 0
### [step 1] 1번 노드를 거쳐 가는 경우를 고려하여 테이블을 갱신한다.
![image](https://user-images.githubusercontent.com/108309396/224861128-b0b83bc3-5d2e-43f6-bbca-a82eee53c4dd.png)
### [step 2] 2번 노드를 거쳐 가는 경우를 고려하여 테이블을 갱신한다.
![image](https://user-images.githubusercontent.com/108309396/224861133-ddec7923-042b-4c43-91c6-71dbec6a5fc5.png)
### [step ~] 3번, 4번, ... 노드를 거쳐 가는 경우를 고려하여 테이블을 갱신한다.
![image](https://user-images.githubusercontent.com/108309396/224861140-7a252e4b-68b6-4f35-9d7f-481d266fe532.png)  
![image](https://user-images.githubusercontent.com/108309396/224861155-68e1bf54-394f-44bf-b92c-a13807dfdb09.png)


## 📌Implement
```python
import sys

input = sys.stdin.readline
INF = int(1e9)

# 노드의 개수(n)과 간선의 개수(m) 입력
n = int(input())
m = int(input())

# 2차원 리스트 (그래프 표현) 만들고, 무한대로 초기화
graph = [[INF] * (n + 1) for _ in range(n + 1)]

# 자기 자신에서 자기 자신으로 가는 비용은 0으로 초기화
for a in range(1, n + 1):
    for b in range(1, n + 1):
        if a == b:
            graph[a][b] = 0

# 각 간선에 대한 정보를 입력받아, 그 값으로 초기화
for _ in range(m):
    # A -> B로 가는 비용을 C라고 설정
    a, b, c = map(int, input().split())
    graph[a][b] = c

# 점화식에 따라 플로이드 워셜 알고리즘을 수행
for k in range(1, n + 1):
    for a in range(1, n + 1):
        for b in range(1, n + 1):
            graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])

# 수행된 결과를 출력
for a in range(1, n + 1):
    for b in range(1, n + 1):
        if graph[a][b] == INF:
            print('INFINITY', end=' ')
        else:
            print(graph[a][b], end=' ')
    print()
```

# 다익스트라 vs 벨만 포드 vs 플로이드 워셜
## 📌다익스트라
- 시간 복잡도는 $O(ElogE)$
- 하나의 정점에서 모든 정점으로 가는 최단거리를 구함.
- 우선순위 큐 사용
   1. 시작 노드 결정 0으로 초기화 후 우선순위 큐에 담음
   2. 나머지 노드 무한대로 초기화
   3. 우선순위 큐에서 pop한 후 그 노드에서 갈 수 있는 노드를 확인
   4. 더 빠르다면 갱신하고 우선순위 큐에 넣는다.
   5. 방문했거나, 더 느리다면 continue
   6. 우선순위 큐가 빌 때까지 3-5번을 반복한다.

## 📌벨만 포드
- 시간 복잡도는 $O(V*E) \~= O(V^3)$
- 하나의 정점에서 모든 정점으로 가는 최단거리를 구함.
- 가중치가 음수인 경우도 적용 가능
- 가중치가 사이클을 이루는 경우 체크 가능
   1. 시작 노드 결정 0으로 초기화
   2. 나머지 노드 무한대로 초기화
   3. 나머지 노드 방문하며 주변 노드에 방문하는 최단거리 갱신 (v-1 번 반복)
   4. 한 번 더 방문하면 업데이트 되는지 확인 (사이클 확인, 사이클이 있다면 false)

## 📌플로이드 워셜
- 시간 복잡도는 $O(V^3)$
- 모든 정점에서 모든 정점으로 가는 최단거리를 구함.
- 그러므로 그래프는 2차원 배열
- 가중치가 음수인 경우도 적용 가능
   1. 인접행렬을 저장할 2차원 배열을 만들고 무한대로 초기화
   2. 간선정보저장, 제자리 0으로 초기화
   3. 경유지를 기준으로, 해당 경우지를 거쳐가는게 빠르다면 갱신
     (i 가 경유지라면, A[j][k] = min(A[j][k],A[j][i]+A[i][k]) )
   4. 모든 정점을 경유지로 선정해 3번 반복