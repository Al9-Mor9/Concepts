# Binary Tree

- 개념 요약
    - 각각의 노드가 최대 두 개의 자식 노드를 가지는 트리(그림을 뒤집었을 때 트리모양) 자료구조
- 트리(Tree) 개념 상세
    
    ![Untitled](https://user-images.githubusercontent.com/90077061/216817120-6fcbc56b-1756-43a8-8765-6d26f6b5549e.png)
    
    - 검정색 동그라미 : 노드(node), 여기에 데이터가 담김.
    - 노드와 노드 사이를 이어주는 선을 엣지(edge)라고 함.
    - 경로(path)란 엣지로 연결된, 즉 인접한 노드들로 이뤄진 시퀀스(sequence)를 가리킴.
    - 트리의 높이(height)는 루트노드에서 말단노드에 이르는 가장 긴 경로의 엣지 수
    - 잎새노드(leaf node) 또는 말단노드 : 자식노드가 없는 노드
    - internal node : 잎새노드를 제외한 노드
    - root node : 부모노드가 없는 노드
- 특성
    - 임의의 노드에서 다른 노드로 가는 경로는 유일하다
    - 회로가 존재하지 않는다
    - 모든 노드는 서로 연결되어있다
    - 엣지를 하나 자르면 트리가 두 개로 분리된다
    - 엣지의 수는 노드의 수에서 1을 뺀 것과 같다
- 종류
    - 정 이진트리(Full Binary Tree)
        - 모든 노드가 0개, 혹은 2개의 자식노드를 가지는 트리.   
        ![image](https://user-images.githubusercontent.com/74289372/218609676-0d0809a2-7b74-40cd-9742-4ca193280927.png)




    - 포화 이진트리(Perfect Binary Tree)
        - 모든 레벨에서 노드들이 꽉 채워진(잎새노드를 제외한 모든 노드가 2개의 자식노드를 가짐) 트리
        
        ![Untitled 1](https://user-images.githubusercontent.com/90077061/216817131-7a1b5452-38f2-46b9-9136-d0ab2cc47ca1.png)
        
        - 레벨(k)에 따른 노드의 숫자 : $2^k$
    - 완전 이진트리(Complete Binary Tree)
        - 마지막 레벨을 제외한 모든 레벨이서 노드들이 꽉 채워진 이진트리
        
        ![Untitled 2](https://user-images.githubusercontent.com/90077061/216817140-0525c485-004d-4a20-ab78-e8773cbf9876.png)
        
    정이진트리와 완전이진트리는 다음처럼 1차원 배열(array)로도 표현이 가능
    
    ![Untitled 3](https://user-images.githubusercontent.com/90077061/216817144-8a767e99-3e82-419a-97ec-7ec7174cd874.png)
    
    ```python
    left_index = index * 2 + 1
    right_index = index * 2 + 1
    ```
    
- 트리 순회
    - 트리의 각 노드를 체계적인 방법으로 방문하는 과정
    
    ![Untitled 4](https://user-images.githubusercontent.com/90077061/216817167-07bb6990-9aa3-4d82-b7c4-caab1755a2bc.png)
    
    - 전위 순회(preorder)
        - 1, 2, 4, 5, 3
    - 중위 순회(inorder)
        - 4, 2, 5, 1, 3
    - 후위 순회(postorder)
        - 4, 5, 2, 3, 1

# Heap

- 개념 요약
    - 완전 이진트리의 일종으로, 우선순위 큐를 위하여 만들어진 자료
    - 여러 개의 값들 중에서 최댓값이나 최솟값을 빠르게 찾아내도록 만들어진 자료구조
    - 힙은 일종의 반정렬 상태를 유지
        - 큰 값이 상위 레벨에 있고, 작은 값이 하위 레벨에 있다는 정도
        - 간단히 말하면 **부모 노드의 키 값이 자식 노드의 키 값보다 항상 큰(작은) 이진 트리**
    - 힙 트리에서는 중복값 허용(이진 탐색 트리에서는 중복값 허용X
- 힙의 종류
    
    ![Untitled 5](https://user-images.githubusercontent.com/90077061/216817179-f1ee37bb-2653-4272-8e0f-500d916d65ea.png)

    - 최대 힙(Max Heap)
        - 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리
    - 최소 힙(Min Heap)
        - 부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진 트리
- 구현
    - 힙을 저장하는 표준적인 자료구조는 **배열**
    - 배열의 첫 번째 인덱스인 0은 사용 X
    - 특정 위치의 노드 번호는 새로운 노드가 추가되어도 변하지 않음
        - (루트 노드의 오른쪽 노드의 번호는 항상 3)
    - 힙에서의 부모 노드와 자식 노드의 관계
        - 왼쪽 자식의 인덱스 = (부모 인덱스) * 2
        - 오른쪽 자식의 인덱스 = (부모 인덱스) * 2 + 1
        - 부모 인덱스 = (자식 인덱스) / 2
    
    ```python
    import heapq
    
    heap = []
    
    heapq.heappush(heap, 10)
    heapq.heappush(heap, 6)
    heapq.heappush(heap, 13)
    heapq.heappush(heap, 5)
    
    print(heap) # [5, 6, 10, 13]
    
    print(heapq.heappop(heap))  # 5
    print(heap) # [6, 10, 13]
    
    # heapify
    x = [4, 3, 1, 2, 5, 6]
    print(x) # [4, 3, 1, 2, 5, 6]
    heapq.heapify(x)
    print(x) # [1, 2, 4, 3, 5, 6]
    ```
    
- 저장 과정
    
    ![Untitled 6](https://user-images.githubusercontent.com/90077061/216817184-dc810d77-1d03-46eb-8df9-aec7f777b7b2.png)
    
- 삭제 과정(heapify)
    
    ![Untitled 7](https://user-images.githubusercontent.com/90077061/216817198-575a16ef-b7cd-491f-8c6d-d448e0f42671.png)
    
# Priority Queue

- 개념 요약
    - 우선순위의 개념을 큐에 도입한 자료 구조
    - 데이터들이 우선순위를 가지고 있고, 우선순위가 높은 데이터가 먼저 나간다
        
        
        | 자료구조 | 삭제되는 요소 |
        | --- | --- |
        | 스택(Stack) | 가장 최근에 들어온 데이터 |
        | 큐(Queue) | 가장 먼저 들어온 데이터 |
        | 우선순위 큐(Priority Queue) | 가장 우선순위가 높은 데이터 |
- 연산(python)
    - put : 맨 끝 위치에 값을 저장
        - 부모 노드와 비교하며, 조건을 만족하는지 확인
            - 만족하지 않는다면, 서로 위치를 변경(Heap - 저장 과정 참조)
    - pop : 가장 우선순위가 높은 값을 삭제
        - 맨 끝의 노드를 비어있는 루트 노드로 끌어옴
        - 루트 노드의 자식 노드들과 값을 비교, 위치 변경
            - 위치를 만족할 때 까지 자식 노드와 위치를 변경하며 올바른 위치까지 이동
- 구현
    - 일반적으로 배열 사용 - 완전 이진 트리 이므로 중간에 비어있는 요소가 없기 때문
    
    ```python
    from queue import PriorityQueue
    
    q = PriorityQueue()
    q1 = PriorityQueue(maxsize=10)  # maxsize를 활용하여 크기 제한 가능
    
    # put
    q.put(3)
    q.put(4)
    q.put(1)
    
    q1.put((1, 'apple'))    # (우선순위, 값)의 형태로 저장 할 수도 있음
    
    # get
    print(q.get())  # 1
    
    # (우선순위, 값)의 형태에서 값 반환
    print(q1.get()[1]) # apple
    ```
    

# Indexed Tree

- 개념 요약
    - 포화 이진 트리 형태의 자료구조
    - 잎새 노드(리프 노드)는 배열에 적혀 있는 수를 의미
    - 내부 노드는 왼쪽 자식과 오른쪽 자식의 합을 이야기한다
- 사용 용도
    - 부분합(또는 구간 Max값)을 계속해서 구해야 할 때
    - 특정 인덱스의 변경 또한 계속 일어날 수 있을 때
- 예제
    - [8, 3, 26, 1, 7, 2, 4, 10] 이라는 숫자들 중 3-5인덱스의 합을 구하려는 상황
        
        ![Untitled 8](https://user-images.githubusercontent.com/90077061/216817210-5fe57469-a928-4af1-9ed5-4da57205203d.png)
        
    - 필요한 구간 노드까지만 탐색해서 최종합을 반환
- 코드 구현

# Segment Tree

- 개념 요약
    - 여러 개의 데이터가 존재할 때 특정 구간의 합(최솟값, 최댓값, 곱 등)을 구하는데 사용하는 자료구조
    - 트리 종류 중 하나로 이진 트리의 형태, 특정 구간의 합을 가장 빠르게 구할 수 있음
- 예제
    - [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]의 구간 합 구하기
    
    ```python
    arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    
    # arr 크기보다 큰 가장 가까운 N의 제곱수를 구하고, 그 값의 2배에 해당하는 값을 크기로 선언
    # N이 10으로 가장 가까운 제곱수는 4^2=16으로 16*2=32개의 크기가 필요
    tree = [0] * (len(arr) * 4)
    ```
    
    - 트리 초기화
    
    ![Untitled 9](https://user-images.githubusercontent.com/90077061/216817220-e751bc0d-633f-462c-ab21-e8d90dc3dfeb.png)
    
    `보통 리스트의 인덱스는 0번부터 시작하는데, 세그먼트 트리는 1번부터 시작하는지 의문이 생길 수 있다. 세그먼트 트리의 인덱스가 1번부터 시작하는 이유는 재귀적으로 편하게 세그먼트 트리를 생성하기 위해서이다. 1부터 시작하게 되면 2를 곱했을 때는 왼쪽 자식 노드를 가리키고, 2를 곱하고 1을 더하면 오른쪽 자식 노드를 가리키게 되어 효과적임`
    
    ```python
    # <세그먼트 트리를 배열의 각 구간 합으로 채워주기>
    # start : 배열의 시작 인덱스, end : 배열의 마지막 인덱스
    # index : 세그먼트 트리의 인덱스 (무조건 1부터 시작)
    def init(start, end, index):
        # 가장 끝에 도달했으면 arr 삽입
        if start == end:
            tree[index] = arr[start]
            return tree[index]
        mid = (start + end) // 2
        # 좌측 노드와 우측 노드를 채워주면서 부모 노드의 값도 채워준다.
        tree[index] = init(start, mid, index * 2) + init(mid + 1, end, index * 2 + 1)
        return tree[index]
    
    init(0, 9, 1)
    
    print(tree)
    # [0, 55, 15, 40, 6, 9, 21, 19, 3, 3, 4, 5, 13, 8, 9, 10, 1, 2, 0, 0, 0, 0, 0, 0, 6, 7, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
    ```
    
    - 트리 구간 합 구하기
    
    ![Untitled 10](https://user-images.githubusercontent.com/90077061/216817240-f6471dc5-83b7-42be-be48-7f82cf803b3c.png)
    
    `6-9 범위의 구간합을 구한다고 가정 시 그림처럼 3개의 빨간색 노드의 합만 구해주면 된다.`
    
    ```python
    # <구간 합을 구하는 함수>
    # start : 시작 인덱스, end : 마지막 인덱스
    # left, right : 구간 합을 구하고자 하는 범위
    def interval_sum(start, end, index, left, right):
        # 범위 밖에 있는 경우
        if left > end or right < start:
            return 0
        # 범위 안에 있는 경우
        if left <= start and right >= end:
            return tree[index]
        # 그렇지 않다면 두 부분으로 나누어 합을 구하기
        mid = (start + end) // 2
        # start와 end가 변하면서 구간 합인 부분을 더해준다고 생각하면 된다.
        return interval_sum(start, mid, index * 2, left, right) + interval_sum(mid + 1, end, index * 2 + 1, left, right)
    
    print(interval_sum(0, 9, 1, 6, 9))
    # 34
    ```
    
    - 원소 값 수정
    
    ![Untitled 11](https://user-images.githubusercontent.com/90077061/216817251-410979a7-2676-4835-a576-b2579c3c23ab.png)
    
    `특정 원소의 값을 수정할 때는 **해당 원소를 포함하고 있는 모든 구간 합 노드들을 갱신**
    해주면 됨. 즉, 세그먼트 트리의 모든 노드를 변경하는 것이 아닌 해당 원소를 포함하고 있는 부분적인 노드들만 바꿔주면 되는 것`
    
    `예를들어 인덱스 6의 arr값을 수정한다고 가정 시 5개의 구간 합 노드를 모두 수정`
    
    ```python
    # <특정 원소의 값을 수정하는 함수>
    # start : 시작 인덱스, end : 마지막 인덱스
    # what : 구간 합을 수정하고자 하는 노드
    # value : 수정할 값
    def update(start, end, index, what, value):
        # 범위 밖에 있는 경우
        if what < start or what > end:
            return
        # 범위 안에 있으면 내려가면서 다른 원소도 갱신
        tree[index] += value
        if start == end:
            return
        mid = (start + end) // 2
        update(start, mid, index * 2, what, value)
        update(mid + 1, end, index * 2 + 1, what, value)
    
    print(tree)
    # [0, 55, 15, 40, 6, 9, 21, 19, 3, 3, 4, 5, 13, 8, 9, 10, 1, 2, 0, 0, 0, 0, 0, 0, 6, 7, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
    update(0, 9, 1, 6, 10)
    print(tree)
    # [0, 65, 15, 50, 6, 9, 31, 19, 3, 3, 4, 5, 23, 8, 9, 10, 1, 2, 0, 0, 0, 0, 0, 0, 6, 17, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
    ```
    

## Segment Tree와 Indexed Tree 차이점

- Segment Tree
    - 세그먼트 트리는 어떤 배열이 주어졌을 때, 각 구간의 대푯값을 빠르게 구할 수 있는 자료구조
    - 배열의 크기가 N일 때, 임의의 구간에 대한 쿼리를 O(logN)에 수행 가능
    - 필요한 리프노드만 채움, 불완전 트리라서 특정 인덱스(node)로 지정 탐색이 어려움.
    - 업데이트도 지정 업데이트가 불가능(루트노드부터 업데이트 필요)
- Indexed Tree
    - 팬윅 트리라고도 하며, 세그먼트 트리처럼 각 구간의 대푯값을 따르게 구할 수 있다
    - 세그먼트 트리보다 구현이 간단하고 속도가 빠르다
    - 리프노드를 모두 채워서 만듦,  특정 인덱스(node)로 지정 탐색이 가능.
    - 업데이트도 지정 업데이트 가능(리프노드부터 업데이트 가능)
    
    **⇒ 문제에서 인덱스가 주어지는 경우 인덱스 트리를 사용하는 것이 용이**
    
    **⇒ 구간 업데이트가 빈번한 경우 세그먼트 트리를 사용하는 것이 용이**
