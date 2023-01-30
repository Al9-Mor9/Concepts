## Bubble sort

- 개념 요약
    - 서로 인접한 두 원소를 검사하여 정렬하는 알고리즘
        - 인접한 2개의 레코드를 비교하여 크기가 순서대로 되어 있지 않으면 서로 교환
- 구체적인 개념
    - 첫 번째 ↔ 두 번째, 두 번째 ↔ 세 번째, … , (마지막-1)번째와 마지막 자료를 비교하여 교환 → 1회전을 수행하면 가장 큰 자료가 맨 뒤로 이동
    - 2회전 수행 시 끝에서 두 번째 자료까지는 정렬에서 제외
- 예제
    
    ![Untitled](https://user-images.githubusercontent.com/90077061/214869782-56ce7ec1-efa8-4221-852e-572a559ca428.png)
    
- 코드
    
    ```python
    def bubble_sort(arr):
        for i in range(len(arr) - 1, 0, -1):
            *for j in range(i):*
                if arr[j] > arr[j + 1]:
                    arr[j], arr[j + 1] = arr[j + 1], arr[j]
    ```
    
- 특징
    - 구현이 매우 간단
    - 순서에 맞지 않은 요소를 인접한 요소와 교환한다
    - 하나의 요소가 가장 왼쪽에서 가장 오른쪽까지 이동하기 위해서 배열의 다른 모든 요소와 교환 되어야 함
    - 단순하지만 거의 쓰이지 않음
- 시간복잡도
    
    $T(n) = O(n^2)$
    

## Selection sort

- 개념 요약
    - 입력 배열 이외에 다른 추가 메모리를 요구하지 않는 정렬방법
    - 해당 순서에 원소를 넣을 위치는 이미 정해져 있고, 어떤 원소를 넣을지 선택하는 알고리즘
    - 과정 설명
    1. 주어진 배열 중에서 최솟값을 찾는다
    2. 그 값을 맨 앞에 위치한 값과 교체한다
    3. 맨 처음 위치를 뺀 나머지 리스트를 같은 방법으로 교체한다
    4. 하나의 원소만 남을 때까지 위의 과정을 반복한다
- 구체적인 개념
    - 가장 작은 값을 찾아 첫 번째에 놓고, 두번째부터 마지막까지 가장 작은 값을 찾아 두번째에 넣고 …
    - 1회전을 하고 나면 가장 작은 값의 자료가 맨 앞으로 오게 되므로 그 다음 회전에서 두 번째 자료를 가지고 비교한다
- 예제
    
    ![Untitled (1)](https://user-images.githubusercontent.com/90077061/214871369-b8882a63-c15c-4752-abe3-3b696a863194.png)
    
- 코드
    
    ```python
    def selection_sort(arr):
        for i in range(len(arr) - 1):
            min_idx = i
            for j in range(i + 1, len(arr)):
                if arr[j] < arr[min_idx]:
                    min_idx = j
            arr[i], arr[min_idx] = arr[min_idx], arr[i]
    ```
    
- 특징
    - 자료 이동 횟수가 미리 결정 된다
    - 안정성이 부족
        
        = 값이 같은 레코드가 있는 경우 상대적 위치가 변경될 수 있다
        
- 시간복잡도
    
    $T(n) = O(n^2)$
    

## Insertion sort

- 개념 요약
    - 손안의 카드를 정렬하는 방법과 유사
    - 모든 요소를 앞에서부터 차례대로 이미 정렬된 배열 부분과 비교
- 구체적인 개념
    - 두 번째 자료부터 시작하여 그 앞의 자료들과 비교하여 삽입할 위치를 지정한 후 자료를 뒤로 옮기고 직정한 자리에 자료를 삽입하여 정렬하는 알고리즘
- 예제
    
    ![Untitled (2)](https://user-images.githubusercontent.com/90077061/214871483-9690673b-6ce9-409e-a719-7ad6fb4d6358.png)
    
- 코드
    
    ```python
    def insertion_sort(arr):
        for end in range(1, len(arr)):
            for i in range(end, 0, -1):
                if arr[i - 1] > arr[i]:
                    arr[i - 1], arr[i] = arr[i], arr[i - 1]
    ```
    
- 특징
    - 안정한 정렬 방법
    - 레코드의 수가 적을 경우 알고리즘 자체가 매우 간단하므로 다른 정렬 법보다 유리
    - 비교적 많은 레코드들의 이동을 포함
    - 레코드 수가 많고 레코드 크기가 클 경우 적합하지 않음
- 시간복잡도
    - $Worst : T(n) = O(n^2)$
