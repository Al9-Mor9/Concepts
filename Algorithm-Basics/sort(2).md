# Merge Sort
## 개념 요약
- **안정 정렬** 에 속하며, **분할 정복 알고리즘**의 하나이다.
  - 분할 정복(divide and conquer) 방법
    - 문제를 작은 2개의 문제로 분리하고 각각을 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 전략이다.
    - 분할 정복 방법은 대개 순환 호출을 이용하여 구현한다.
- 과정
  1. 리스트의 길이가 0 또는 1이면 이미 정렬된 것으로 본다. 
  2. 그렇지 않은 경우에는 정렬되지 않은 리스트를 절반으로 잘라 비슷한 크기의 두 부분 리스트로 나눈다.
  3. 각 부분 리스트를 재귀적으로 합병 정렬을 이용해 정렬한다.
  4. 두 부분 리스트를 다시 하나의 정렬된 리스트로 합병한다.

- P) **안정정렬이란?**   
  배열을 정렬했을 때, 동일한 값의 원소 사이의 위치 관계가 변하지 않는 정렬입니다.   
  (예 [4, 3, 2_1, 1, 2_2] 를 정렬했을 때, 안정정렬인 경우 [1, 2_1, 2_2, 3, 4]로 2의 값을 가지는 두 원소 사이의 위치 관계가 유지되지만, 불안정정렬인 경우에는 [1, 2_2, 2_1, 3, 4]와 같이 나올 수도 있음.)

## 개념
- 하나의 리스트를 두 개의 균등한 크기로 **분할**하고, 분할된 부분 리스트를 **정렬**한 다음, 두 개의 정렬된 부분 리스트를 **합하여** 전체가 정렬된 리스트가 되게 하는 방법이다.
- 단계
  - 분할(Divide): 입력 배열을 같은 크기의 2개의 부분 배열로 분할한다.
  - 정복(Conquer): 부분 배열을 정렬한다. 부분 배열의 크기가 충분히 작지 않으면 **순환 호출**을 이용하여 다시 분할 정복 방법을 적용한다.
  - 결합(Combine): 정렬된 부분 배열들을 하나의 배열에 합병한다.
- 과정
  - 추가적인 리스트가 필요하다.
  - 각 부분 배열을 정렬할 때도 합병 정렬을 순환적으로 호출하여 적용한다.
  - 합병 정렬에서 실제로 정렬이 이루어지는 시점은 2개의 리스트를 합병(merge)하는 단계 이다.  
![merge-sort-concepts](https://user-images.githubusercontent.com/108309396/216827345-734ad9ef-51c8-4a6a-a023-623ae21cc795.png)
- 2개의 정렬된 리스트를 합병(merge)하는 과정
  1. 2개의 리스트의 값들을 처음부터 하나씩 비교하여 두 개의 리스트의 값 중에서 더 작은 값을 새로운 리스트(sorted)로 옮긴다.
  2. 둘 중에서 하나가 끝날 때까지 이 과정을 되풀이한다.
  3. 만약 둘 중에서 하나의 리스트가 먼저 끝나게 되면 나머지 리스트의 값들을 전부 새로운 리스트(sorted)로 복사한다.
  4. 새로운 리스트(sorted)를 원래의 리스트(list)로 옮긴다.  
![merge-sort2](https://user-images.githubusercontent.com/108309396/216827349-e593474b-92f1-4ba3-87e1-b560c3fba430.png)

## 합병 정렬(merge sort) 알고리즘의 특징
- 단점
  - 만약 레코드를 **배열(Array)** 로 구성하면, 임시 배열이 필요하다.
    - 제자리 정렬(in-place sorting)이 아니다.
  - 레코드의 크기가 큰 경우에는 이동 횟수가 많으므로 매우 큰 시간적 낭비를 초래한다.
- 장점
  - 안정적인 정렬 방법
    - 데이터의 분포에 영향을 덜 받는다. 즉, 입력 데이터가 무엇이든 간에 정렬되는 시간은 동일하다. ($O(nlogn)$로 동일)
  - 만약 레코드를 **연결 리스트(Linked List)** 로 구성하면, 링크 인덱스만 변경되므로 데이터의 이동은 무시할 수 있을 정도로 작아진다.
    - 제자리 정렬(in-place sorting)로 구현할 수 있다.
  - 따라서 크기가 큰 레코드를 정렬할 경우에 연결 리스트를 사용한다면, 합병 정렬은 퀵 정렬을 포함한 다른 어떤 졍렬 방법보다 효율적이다.

## 시간복잡도
1. 분할 단계
- 비교 연산과 이동 연산이 수행되지 않는다.
2. 합병 단계
- 비교 횟수  
  - ![sort-time-complexity-etc4](https://user-images.githubusercontent.com/108309396/216827667-c328b96c-5800-46e3-9e84-11cadf6bc84a.png)

  - 순환 호출의 깊이 (합병 단계의 수)
    - 레코드의 개수 n이 2의 거듭제곱이라고 가정$(n=2^k)$했을 때, $n=2^3$의 경우, $2^3$&rarr;$2^2$&rarr;$2^1$&rarr;$2^0$ 순으로 줄어들어 순환 호출의 깊이가 3임을 알 수 있다. 이것을 일반화하면 $n=2^k$의 경우, $k=log_2n$임을 알 수 있다.
    - $k=log_2n$
  - 각 합병 단계의 비교 연산
    - 크기 1인 부분 배열 2개를 합병하는 데는 최대 2번의 비교 연산이 필요하고, 부분 배열의 쌍이 4개이므로 $2\times4=8$번의 비교 연산이 필요하다. 다음 단계에서는 크기 2인 부분 배열 2개를 합병하는 데 최대 4번의 비교 연산이 필요하고, 부분 배열의 쌍이 2개이므로 $4\times2=8$번의 비교 연산이 필요하다. 마지막 단계에서는 크기 4인 부분 배열 2개를 합병하는 데는 최대 8번의 비교 연산이 필요하고, 부분 배열의 쌍이 1개이므로 $8\times1=8$번의 비교 연산이 필요하다. 이것을 일반화하면 하나의 합병 단계에서는 최대 n번의 비교 연산을 수행함을 알 수 있다.
    - 최대 n번
  - 순환 호출의 깊이 만큼의 합병 단계 * 각 합병 단계의 비교 연산 = $nlog_2n$
- 이동 횟수
  - 순환 호출의 깊이 (합병 단계의 수)
    - $k=log_2n$
  - 각 합병 단계의 이동 연산
    - 임시 배열에 복사했다가 다시 가져와야 되므로 이동 연산은 총 부분 배열에 들어 있는 요소의 개수가 n인 경우, 레코드의 이동이 2n번 발생한다.
  - 순환 호출의 깊이 만큼의 합병 단계 * 각 합병 단계의 이동 연산 = $2nlog_2n$
3. $T(n) = nlog_2n(비교) + 2nlog_2n(이동) = 3nlog_2n = O(nlogn)$

## Merge Sort C언어 구현
```C
# include <stdio.h>
# define MAX_SIZE 8
int sorted[MAX_SIZE] // 추가적인 공간이 필요

// i: 정렬된 왼쪽 리스트에 대한 인덱스
// j: 정렬된 오른쪽 리스트에 대한 인덱스
// k: 정렬될 리스트에 대한 인덱스
/* 2개의 인접한 배열 list[left...mid]와 list[mid+1...right]의 합병 과정 */
/* (실제로 숫자들이 정렬되는 과정) */
void merge(int list[], int left, int mid, int right){
  int i, j, k, l;
  i = left;
  j = mid+1;
  k = left;

  /* 분할 정렬된 list의 합병 */
  while(i<=mid && j<=right){
    if(list[i]<=list[j])
      sorted[k++] = list[i++];
    else
      sorted[k++] = list[j++];
  }

  // 남아 있는 값들을 일괄 복사
  if(i>mid){
    for(l=j; l<=right; l++)
      sorted[k++] = list[l];
  }
  // 남아 있는 값들을 일괄 복사
  else{
    for(l=i; l<=mid; l++)
      sorted[k++] = list[l];
  }

  // 배열 sorted[](임시 배열)의 리스트를 배열 list[]로 재복사
  for(l=left; l<=right; l++){
    list[l] = sorted[l];
  }
}

// 합병 정렬
void merge_sort(int list[], int left, int right){
  int mid;

  if(left<right){
    mid = (left+right)/2 // 중간 위치를 계산하여 리스트를 균등 분할 -분할(Divide)
    merge_sort(list, left, mid); // 앞쪽 부분 리스트 정렬 -정복(Conquer)
    merge_sort(list, mid+1, right); // 뒤쪽 부분 리스트 정렬 -정복(Conquer)
    merge(list, left, mid, right); // 정렬된 2개의 부분 배열을 합병하는 과정 -결합(Combine)
  }
}

void main(){
  int i;
  int n = MAX_SIZE;
  int list[n] = {21, 10, 12, 20, 25, 13, 15, 22};

  // 합병 정렬 수행(left: 배열의 시작 = 0, right: 배열의 끝 = 7)
  merge_sort(list, 0, n-1);

  // 정렬 결과 출력
  for(i=0; i<n; i++){
    printf("%d\n", list[i]);
  }
}
```  
![merge-sort-ccode3](https://user-images.githubusercontent.com/108309396/216827344-c657ca30-2cc1-4d30-9732-649945ee9ce1.png)



# Heap Sort
## 자료구조 ‘힙(heap)’
- 완전 이진 트리의 일종으로 우선순위 큐를 위하여 만들어진 자료구조
- 최댓값, 최솟값을 쉽게 추출할 수 있는 자료구조  
![1](https://user-images.githubusercontent.com/108309396/216829091-1422af71-c1c0-4407-8ff0-b158a99a67a9.png)

## 개념 요약
- 최대 힙 트리나 최소 힙 트리를 구성해 정렬을 하는 방법
- 내림차순 정렬을 위해서는 최대 힙을 구성하고, 오름차순 정렬을 위해서는 최소 힙을 구성
- 과정
  1. 정렬해야 할 n개의 요소들로 최대 힙(완전 이진 트리 형태)을 만든다.
     - 내림차순을 기준으로 정렬
  2. 그 다음으로 한 번에 하나씩 요소를 힙에서 꺼내서 배열의 뒤부터 저장하면 된다.
  3. 삭제되는 요소들(최댓값부터 삭제)은 값이 감소되는 순서로 정렬되게 된다.

## 힙 정렬(heap sort) 알고리즘의 특징
- 장점
  - 시간 복잡도가 좋은편
  - 힙 정렬이 가장 유용한 경우는 전체 자료를 정렬하는 것이 아니라 가장 큰 값 몇개만 필요할 때 이다.

## 힙 정렬(heap sort)의 시간복잡도

- 힙 트리의 전체 높이가 거의 $log_2n$(완전 이진 트리이므로)이므로 하나의 요소를 힙에 삽입하거나 삭제할 때 힙을 재정비하는 시간이 $log_2n$만큼 소요된다.
- 요소의 개수가 n개 이므로 전체적으로 $O(nlog_2n)$의 시간이 걸린다.
- $T(n) = O(nlogn)$


## 내림차순 정렬을 위한 최대 힙(max heap)의 구현
- 힙(heap)은 1차원 배열로 쉽게 구현될 수 있다.
- 정렬해야 할 n개의 요소들을 1차원 배열에 기억한 후 최대 힙 삽입을 통해 차례대로 삽입한다.
- 최대 힙으로 구성된 배열에서 최댓값부터 삭제한다.
1. 최대 힙(max heap)의 삽입
    1) 힙에 새로운 요소가 들어오면, 일단 새로운 노드를 힙의 마지막 노드에 이어서 삽입한다.
    2) 새로운 노드를 부모 노드들과 교환해서 힙의 성질을 만족시킨다.
- 아래의 최대 힙(max heap)에 새로운 요소 8을 삽입해보자.  
![2](https://user-images.githubusercontent.com/108309396/216829093-34a9e50b-f278-4f61-a2ac-145e89c26c23.png)

## C언어를 이용한 최대 힙(max heap) 삽입 연산
```c
/* 현재 요소의 개수가 heap_size인 힙 h에 item을 삽입한다. */
// 최대 힙(max heap) 삽입 함수
void insert_max_heap(HeapType *h, element item){
  int i;
  i = ++(h->heap_size); // 힙 크기를 하나 증가

  /* 트리를 거슬러 올라가면서 부모 노드와 비교하는 과정 */
  // i가 루트 노트(index: 1)이 아니고, 삽입할 item의 값이 i의 부모 노드(index: i/2)보다 크면
  while((i != 1) && (item.key > h->heap[i/2].key)){
    // i번째 노드와 부모 노드를 교환환다.
    h->heap[i] = h->heap[i/2];
    // 한 레벨 위로 올라간다.
    i /= 2;
  }
  h->heap[i] = item; // 새로운 노드를 삽입
}
```

2. 최대 힙(max heap)의 삭제
- 최대 힙에서 최댓값은 루트 노드이므로 루트 노드가 삭제된다.
- 최대 힙(max heap)에서 삭제 연산은 최댓값을 가진 요소를 삭제하는 것이다.
- 삭제된 루트 노드에는 힙의 마지막 노드를 가져온다.
- 힙을 재구성한다.
- 아래의 최대 힙(max heap)에서 최댓값을 삭제해보자.  
![3](https://user-images.githubusercontent.com/108309396/216829094-c55ed29d-dd92-40a7-8ac2-1bcbb1237c10.png)

## C언어를 이용한 최대 힙(max heap) 삭제 연산
```c
// 최대 힙(max heap) 삭제 함수
element delete_max_heap(HeapType *h){
  int parent, child;
  element item, temp;

  item = h->heap[1]; // 루트 노드 값을 반환하기 위해 item에 할당
  temp = h->heap[(h->heap_size)--]; // 마지막 노드를 temp에 할당하고 힙 크기를 하나 감소
  parent = 1;
  child = 2;

  while(child <= h->heap_size){
    // 현재 노드의 자식 노드 중 더 큰 자식 노드를 찾는다. (루트 노드의 왼쪽 자식 노드(index: 2)부터 비교 시작)
    if( (child < h->heap_size) && ((h->heap[child].key) < h->heap[child+1].key) ){
      child++;
    }
    // 더 큰 자식 노드보다 마지막 노드가 크면, while문 중지
    if( temp.key >= h->heap[child].key ){
      break;
    }

    // 더 큰 자식 노드보다 마지막 노드가 작으면, 부모 노드와 더 큰 자식 노드를 교환
    h->heap[parent] = h->heap[child];
    // 한 단계 아래로 이동
    parent = child;
    child *= 2;
  }

  // 마지막 노드를 재구성한 위치에 삽입
  h->heap[parent] = temp;
  // 최댓값(루트 노드 값)을 반환
  return item;
}
```

## 힙 정렬(heap sort) 알고리즘의 예제 및 c언어 코드
- 배열에 9, 7, 6, 5, 4, 3, 2, 2, 1, 3이 저장되어 있다고 가정하고 자료를 내림차순으로 정렬
- 위의 최대 힙(max heap)의 삽입, 삭제 c언어 코드를 참고
```c
// 우선순위 큐인 힙을 이용한 정렬
void heap_sort(element a[], int n){
  int i;
  HeapType h;

  init(&h);

  for(i=0; i<n; i++){
    insert_max_heap(&h, a[i]);
  }

  for(i=(n-1); i>=0; i--){
    a[i] = delete_max_heap(&h);
  }
}
```





# Quick Sort
## 개념 요약
- **불안정 정렬**에 속하며, 다른 원소와의 비교만으로 정렬을 수행하는 **비교 정렬**에 속한다.
- 분할 정복 알고리즘의 하나로, 평균적으로 매우 빠른 수행 속도를 자랑하는 정렬 방법
  - 합병 정렬(merge sort)과 달리 퀵 정렬은 리스트를 **비균등하게 분할**한다.
- 분할 정복(divide and conquer) 방법
  - 문제를 작은 2개의 문제로 분리하고 각각을 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 전략이다.
  - 분할 정복 방법은 대개 순환 호출을 이용하여 구현한다.
- 과정
  - 리스트 안에 있는 한 요소를 선택한다. 이렇게 고른 원소를 **피벗(pivot)** 이라고 한다.
  - 피벗을 기준으로 피벗보다 작은 요소들은 모두 피벗의 왼쪽으로 옮겨지고 피벗보다 큰 요소들은 모두 피벗의 오른쪽으로 옮겨진다.
  - 피벗을 제외한 왼쪽 리스트와 오른쪽 리스트를 다시 정렬한다.
    - 분할된 부분 리스트에 대하여 순환 호출 을 이용하여 정렬을 반복한다.
    - 부분 리스트에서도 다시 피벗을 정하고 피벗을 기준으로 2개의 부분 리스트로 나누는 과정을 반복한다.
  - 부분 리스트들이 더 이상 분할이 불가능할 때까지 반복한다.
    - 리스트의 크기가 0이나 1이 될 때까지 반복한다.  
![1](https://user-images.githubusercontent.com/108309396/216830122-5e571f0a-5b05-4683-8824-2ce9efc6581f.png)



## 개념
- 하나의 리스트를 피벗(pivot)을 기준으로 두 개의 비균등한 크기로 분할하고 분할된 부분 리스트를 정렬한 다음, 두 개의 정렬된 부분 리스트를 합하여 전체가 정렬된 리스트가 되게 하는 방법이다.
- 퀵 정렬은 다음의 단계들로 이루어진다.
  - 분할(Divide): 입력 배열을 피벗을 기준으로 비균등하게 2개의 부분 배열(피벗을 중심으로 왼쪽: 피벗보다 작은 요소들, 오른쪽: 피벗보다 큰 요소들)로 분할한다.
  - 정복(Conquer): 부분 배열을 정렬한다. 부분 배열의 크기가 충분히 작지 않으면 순환 호출 을 이용하여 다시 분할 정복 방법을 적용한다.
  - 결합(Combine): 정렬된 부분 배열들을 하나의 배열에 합병한다.
  - 순환 호출이 한번 진행될 때마다 최소한 하나의 원소(피벗)는 최종적으로 위치가 정해지므로, 이 알고리즘은 반드시 끝난다는 것을 보장할 수 있다.  
![2](https://user-images.githubusercontent.com/108309396/216830123-ab8d6730-ce5a-4b7f-88e2-695c32f6069d.png)

## 퀵 정렬(quick sort) 알고리즘의 특징
- 장점
  - 속도가 빠르다.
    - 시간 복잡도가 $O(nlog_2n)$를 가지는 다른 정렬 알고리즘과 비교했을 때도 가장 빠르다.
  - 추가 메모리 공간을 필요로 하지 않는다.
    - 퀵 정렬은 $O(log n)$만큼의 메모리를 필요로 한다.
- 단점
  - 정렬된 리스트에 대해서는 퀵 정렬의 불균형 분할에 의해 오히려 수행시간이 더 많이 걸린다.
- 퀵 정렬의 불균형 분할을 방지하기 위하여 피벗을 선택할 때 더욱 리스트를 균등하게 분할할 수 있는 데이터를 선택한다.
  - EX) 리스트 내의 몇 개의 데이터 중에서 크기순으로 중간 값(medium)을 피벗으로 선택한다.

## 퀵 정렬(quick sort)의 시간복잡도
1. 최선의 경우
- 비교 횟수
  - ![sort-time-complexity-etc4](https://user-images.githubusercontent.com/108309396/216827667-c328b96c-5800-46e3-9e84-11cadf6bc84a.png)
  - 순환 호출의 깊이
    - 레코드의 개수 n이 2의 거듭제곱이라고 가정$(n=2^k)$했을 때, $n=2^3$의 경우, $2^3$&rarr;$2^2$&rarr;$2^1$&rarr;$2^0$ 순으로 줄어들어 순환 호출의 깊이가 3임을 알 수 있다. 이것을 일반화하면 $n=2^k$의 경우, $k=log_2n$임을 알 수 있다.
    - $k=log_2n$
  - 각 순환 호출 단계의 비교 연산
    - 각 순환 호출에서는 전체 리스트의 대부분의 레코드를 비교해야 하므로 평균 n번 정도의 비교가 이루어진다.
    - 평균 n번
  - 순환 호출의 깊이 * 각 순환 호출 단계의 비교 연산 = $nlog_2n$
- 이동 횟수
  - 비교 횟수보다 적으므로 무시할 수 있다.
- 최선의 경우 $T(n) = O(nlog₂n)$

2. 최악의 경우
- 리스트가 계속 불균형하게 나누어지는 경우 (특히, 이미 정렬된 리스트에 대하여 퀵 정렬을 실행하는 경우)
  - ![sort-time-complexity-etc2](https://user-images.githubusercontent.com/108309396/216861849-405be650-09d1-4eab-9854-f4aff9734d45.png)
- 비교 횟수
  - 순환 호출의 깊이
    - 레코드의 개수 n이 2의 거듭제곱이라고 가정$(n=2^k)$했을 때, 순환 호출의 깊이는 $n$임을 알 수 있다.
    - $n$
  - 각 순환 호출 단계의 비교 연산
    - 각 순환 호출에서는 전체 리스트의 대부분의 레코드를 비교해야 하므로 평균 $n$번 정도의 비교가 이루어진다.
    - 평균 $n$번
    - 순환 호출의 깊이 * 각 순환 호출 단계의 비교 연산 = $n^2$
  - 이동 횟수
    - 비교 횟수보다 적으므로 무시할 수 있다.
- 최악의 경우 $T(n) = O(n^2)$

1. 평균
- 평균 $T(n) = O(nlog_2n)$
- 시간 복잡도가 $O(nlog_2n)$를 가지는 다른 정렬 알고리즘과 비교했을 때도 가장 빠르다.
- 퀵 정렬이 불필요한 데이터의 이동을 줄이고 먼 거리의 데이터를 교환할 뿐만 아니라, 한 번 결정된 피벗들이 추후 연산에서 제외되는 특성 때문이다.


## 퀵 정렬(quick sort) 알고리즘의 예제
- 배열에 5, 3, 8, 4, 9, 1, 6, 2, 7이 저장되어 있다고 가정하고 자료를 오름차순으로 정렬
- 퀵 정렬에서 피벗을 기준으로 두 개의 리스트로 나누는 과정(c언어 코드의 partition 함수의 내용)  
![3](https://user-images.githubusercontent.com/108309396/216830124-68a7d2bc-0031-4588-a0eb-0c7413b53582.png)

- 피벗 값을 입력 리스트의 첫 번째 데이터로 하자. (다른 임의의 값이어도 상관없다.)
- 2개의 인덱스 변수(low, high)를 이용해서 리스트를 두 개의 부분 리스트로 나눈다.
- 1회전: 피벗이 5인 경우,
  - low는 왼쪽에서 오른쪽으로 탐색해가다가 피벗보다 큰 데이터(8)을 찾으면 멈춘다.
  - high는 오른쪽에서 왼쪽으로 탐색해가다가 피벗보다 작은 데이터(2)를 찾으면 멈춘다.
  - low와 high가 가리키는 두 데이터를 서로 교환한다.
  - 이 탐색-교환 과정은 low와 high가 엇갈릴 때까지 반복한다.
- 2회전: 피벗(1회전의 왼쪽 부분리스트의 첫 번째 데이터)이 1인 경우,
  - 위와 동일한 방법으로 반복한다.
- 3회전: 피벗(1회전의 오른쪽 부분리스트의 첫 번째 데이터)이 9인 경우,
  - 위와 동일한 방법으로 반복한다.


## 퀵 정렬(quick sort) c언어 코드
```c
# include <stdio.h>
# define MAX_SIZE 9
# define SWAP(x, y, temp) ( (temp)=(x), (x)=(y), (y)=(temp) )

// 1. 피벗을 기준으로 2개의 부분 리스트로 나눈다.
// 2. 피벗보다 작은 값은 모두 왼쪽 부분 리스트로, 큰 값은 오른쪽 부분 리스트로 옮긴다.
/* 2개의 비균등 배열 list[left...pivot-1]와 list[pivot+1...right]의 합병 과정 */
/* (실제로 숫자들이 정렬되는 과정) */
int partition(int list[], int left, int right){
  int pivot, temp;
  int low, high;

  low = left;
  high = right + 1;
  pivot = list[left]; // 정렬할 리스트의 가장 왼쪽 데이터를 피벗으로 선택(임의의 값을 피벗으로 선택)

  /* low와 high가 교차할 때까지 반복(low<high) */
  do{
    /* list[low]가 피벗보다 작으면 계속 low를 증가 */
    do {
      low++; // low는 left+1 에서 시작
    } while (low<=right && list[low]<pivot);

    /* list[high]가 피벗보다 크면 계속 high를 감소 */
    do {
      high--; //high는 right 에서 시작
    } while (high>=left && list[high]>pivot);

    // 만약 low와 high가 교차하지 않았으면 list[low]를 list[high] 교환
    if(low<high){
      SWAP(list[low], list[high], temp);
    }
  } while (low<high);

  // low와 high가 교차했으면 반복문을 빠져나와 list[left]와 list[high]를 교환
  SWAP(list[left], list[high], temp);

  // 피벗의 위치인 high를 반환
  return high;
}

// 퀵 정렬
void quick_sort(int list[], int left, int right){

  /* 정렬할 범위가 2개 이상의 데이터이면(리스트의 크기가 0이나 1이 아니면) */
  if(left<right){
    // partition 함수를 호출하여 피벗을 기준으로 리스트를 비균등 분할 -분할(Divide)
    int q = partition(list, left, right); // q: 피벗의 위치

    // 피벗은 제외한 2개의 부분 리스트를 대상으로 순환 호출
    quick_sort(list, left, q-1); // (left ~ 피벗 바로 앞) 앞쪽 부분 리스트 정렬 -정복(Conquer)
    quick_sort(list, q+1, right); // (피벗 바로 뒤 ~ right) 뒤쪽 부분 리스트 정렬 -정복(Conquer)
  }

}

void main(){
  int i;
  int n = MAX_SIZE;
  int list[n] = {5, 3, 8, 4, 9, 1, 6, 2, 7};

  // 퀵 정렬 수행(left: 배열의 시작 = 0, right: 배열의 끝 = 8)
  quick_sort(list, 0, n-1);

  // 정렬 결과 출력
  for(i=0; i<n; i++){
    printf("%d\n", list[i]);
  }
}
```

# Tree Sort
## 개념
- Binary Search Tree를 만들어 정렬하는 방식.
- Heap Sort와 비슷해보이지만 정렬될 자료의 각 원소의 크기에 따라 부모노드의 왼쪽 자식이 되느냐, 오른쪽 자식이 되느냐가 다르다.
- 과정
  1. 정렬될 배열의 맨 첫 값이 루트 노드가 된다.
  2. 다음 값부터는 기존 노드 값과 비교한다. 루트 노드에서 출발해서 추가될 노드 값이 기존 노드 값보다 작은 경우는 왼쪽 자식을, 기존 노드 값보다 크거나 같을 경우는 오른쪽 자식을 찾는다. 내림차순은 반대로 기존 노드 값보다 크면 왼쪽, 작거나 같으면 오른쪽을 찾으면 된다.
  3. 위 2에서 해당 방향의 자식 노드가 없으면 그 방향의 자식 노드로 추가한다. 있으면 그 방향의 자식 노드로 가서 크기를 비교하고 위 2와 같은 방법으로 해당 방향의 자식 노드가 있으면 계속 그 방향으로 가서 조사하고 없으면 그 방향의 자식 노드로 추가한다.
  4. 모든 값이 노드로 추가되었으면 해당 트리를 **중위 순회 방식**(왼쪽자식-루트-오른쪽자식)으로 순회하여 그 순서대로 값을 정렬해 나간다.  
  ![캡처](https://user-images.githubusercontent.com/108309396/216869488-3440eb75-4ffc-4c37-bf1b-7f89f258bb82.PNG)

## Tree Sort의 특징
- 피벗을 기반으로 요소를 재귀적으로 분할한다는 점에서 퀵 정렬과 동일하지만, 퀵 정렬은 in-place 제자리 정렬이고 overhead가 적기 때문에 퀵 정렬에 비해 이점이 없다. 
- self-balancing tree를 사용하면 worst case에서의 시간복잡도가 더 낫지만 overhead는 더 크다.

## 시간복잡도
- Worst case: $O(n^2)$ (unbalanced)
- Bese case: $O(nlogn)$ (balanced)
- Average performance: $O(nlogn)$

# 정렬 알고리즘 시간복잡도 비교
- 단순(구현 간단)하지만 비효율적인 방법
  - 삽입 정렬, 선택 정렬, 버블 정렬
- 복잡하지만 효율적인 방법
  - 퀵 정렬, 힙 정렬, 합병 정렬, 기수 정렬  
![sort-time-complexity5](https://user-images.githubusercontent.com/108309396/216828072-770c8dcb-8bba-4cab-91e1-814667fd481e.png)
