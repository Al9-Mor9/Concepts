# Search Algorithm
## 1. Linear Search (선형 검색)
![Linear-Search](https://user-images.githubusercontent.com/108309396/214469677-92944d5b-be6b-4c36-a6bd-d16a8b369108.png)
- 순차적으로 검색하여 Sequential search라고도 함
- array, linked list 등의 처음부터 끝까지 하나씩 비교해가며 원하는 값을 찾아내는 알고리즘
- 장점: 단순하여 구현이 쉽고 정렬되지 않은 리스트에서도 사용 가능
- 단점: 데이터의 양이 많아지면 검색에 소요되는 시간도 길어져 비효율적임

### > Time Complexity
- Best case: $O(n) = 1$
-  Worst case: $O(n) = n$
- Average case: $O(n) = (\frac{n}{2}\times\frac{1}{2})+(n\times\frac{1}{2}) = \frac{3}{4}n$  
&rarr; 원하는 대상이 있을 경우와 없을 경우 각각 확률 $\frac{1}{2}$  
&rarr; $O(n)= n$

### > Implementation(using Python)
```python
def LinearSearch(arr, size, target):
    for i in range(size)
        if arr[i] == target # arr이라는 배열에서 target을 찾는다.
            return i # 찾으면 해당 index를 return
    return -1 # 못 찾으면 -1을 return
```


## 2. Binary Search (이진 검색)
![BinarySearch](https://user-images.githubusercontent.com/108309396/214477517-ad8be845-eb14-443b-b505-eabc081f5bd0.png)
- 반으로 나누어 검색
- linear search의 경우 처음부터 끝까지 탐색해야 하지만 binary search는 중간값부터 탐색함
- linear search는 linked list에서, binary search는 tree에서 많이 쓰임
- 계속 반으로 나누면서 연산하기 때문에 처리속도가 매우 빠름
- 대신 반드시 정렬되어야 함

### > Time Complexity
전체 데이터 수를 N이라고 할 때
1) 첫 번째 탐색 후 $\frac{N}{2}$
2) 두 번째 탐색 후 $\frac{N}{2}\times\frac{1}{2}$
3) 세 번쨰 탐색 후 $\frac{N}{2}\times\frac{1}{2}\times\frac{1}{2}$
4) ...k번째 탐색 후 남은 데이터 수 $N\times(\frac{1}{2})^k$  
&rarr; In worst case, $N\times(\frac{1}{2})^k$ = 1  
&rarr; $k = log_2N$  
&rarr; $O(logN)$  

### > Implementation(using Python)
```python
def BinarySearch(arr, size, target):
    first = 0
    last = n - 1
    while first <= last:
        mid = (first + last) // 2
        if target == arr[mid]:
            return mid
        elif target < arr[mid]:
            last = mid - 1
        else 
            first = mid + 1
    return -1
```
## 3. Hash Search
### > Hash Basic
![ComponentsofHashing (1)](https://user-images.githubusercontent.com/108309396/214489817-9ce48fa8-79e7-453d-8261-76f1d1f72624.png)
- Hash Table이란 Key-value쌍으로 데이터를 저장하는 자료구조
- Space-Time trade off의 대표적인 알고리즘
- key, Hash function, Hash, value, bucket, slot으로 이루어져 있음
  - key: 고유한 값으로 해시 함수의 input이 된다.
  - Hash function: key를 hash로 바꿔주는 역할을 함. 다양한 길이를 가지고 있는 key를 일정한 길이를 가지는 hash로 변환하여 저장소를 효율적으로 운용할 수 있도록 도와줌.
  - Hash: 해시 함수의 결과물로 저장소(bucket, slot)에서 value와 매칭되어 저장됨
  - value: 저장소에 최종적으로 저장되는 값으로 key와 매칭되어 저장, 삭제, 검색, 접근이 가능


### > Hash Search Algorithm
![hash3](https://user-images.githubusercontent.com/108309396/214490361-23260cab-87c4-4d72-ae07-50abe17348f8.png)
- Hash search를 위해서는 총 두 개의 알고리즘이 필요
  - 데이터를 저장하는 알고리즘
  - 데이터를 검색하는 알고리즘
- 해시함수로는 나누기 연산, 나머지 연산 등 다양한 연산을 이용할 수 있다.
1. 데이터를 저장하는 알고리즘
   - 배열 2개를 준비한다
    - 주어진 값들을 해시함수를 이용하여 별도의 배열에 다시 저장하기 때문
    - 다른 탐색 알고리즘에서는 배열 크기를 데이터 수 만큼만 준비하면 충분하지만, 해시 탐색법은 데이터 수의 1.5~2배의 크기의 배열을 준비해야 한다.
    - ex) 데이터가 10개이면, 데이터를 15으로 나눈 나머지를 해시값으로 설정한다.

   - 만약, 같은 해시값을 가진 데이터가 있다면 (충돌이 일어난다면) 비어있는 옆 칸에 보관한다.

2. 데이터를 검색하는 알고리즘
   - 저장할 때 사용한 것과 같은 해시 함수를 사용
   - 원하는 데이터가 존재하지 않을 경우에 어떻게 처리할 것인지 정해야 한다
- 장점
  - 데이터를 저장하거나, 탐색하고자 하는 위치를 즉시 참조할 수 있기 때문에 빠른 속도로 처리가 가능
- 단점
  - Hash collision 발생 시 탐색이 시간 복잡도 $O(n)$에 점점 수렴함
  - 정렬이나 순차적인 메모리 저장이 필요한 경우 적합하지 않음
  - 해시 함수의 성능에 따라 해시 테이블 전체 성능이 크게 영향을 받는다.

### Hash Collision
(1) 충돌이 일어난 인덱스를 뛰어넘어서, 빈 공간이 있는지 탐색 후 삽입 → 개방주소법 (Open addressing)

(2) 충돌이 일어난 지점을 사용하되, 연결 리스트로 묶는 방법 → 체이닝 (Chaning)

개방주소법의 경우, 인덱스만 증가시켜주면 되므로 안정적인 방법입니다.

체이닝의 경우, 정해진 해시테이블 이외의 주소를 추가로 할당해서

확장해서 사용할 수 있다는 장점이 있습니다.
### > Time Complexity
- Best case: $O(1)$
- Worst case: $O(n)$
- Hash Table에서 해당하는 데이터를 찾아 바로 return 하기 때문에 $O(1)$

### > Implementation
1. **python의 경우, hash table을 별도로 구현할 필요없음! &rarr; dictionary 사용**
2. C++
```c++
#include <iostream>

#define MAX_TABLE	8191
#define MAX_KEY		64

typedef long long ll;

using namespace std;

typedef struct Hash {
	char key[MAX_KEY + 1];
	int data;
} Hash;
Hash table[MAX_TABLE];

ll hashGen(char key[]) {
	ll h = 5381;
	while (*key != '\0')
		h = (((h << 5) + h) + *key++) % MAX_TABLE;
	return h;
}

int m_strcmp(const char* str1, const char* str2) {
	while (*str1 != '\0' || *str2 != '\0') {
		if (*str1 != *str2) return *str1 - *str2;
		str1++; str2++;
	}
	return 0;
}

void m_strcpy(char dsc[], char src[]) {
	while (*src != '\0')
		*(dsc++) = *(src++);
}

int hashDelete(char key[]) {
	ll h = hashGen(key);
	int cnt = MAX_TABLE;

	while (table[h].key[0] != 0 && cnt--) {
		if (!m_strcmp(table[h].key, key)) {
			table[h].key[0] = 0;
			table[h].data = 0;
			return 1;
		}
		h = (h + 1) % MAX_TABLE;
	}
	return 0;
}

int hashAdd(char key[], int data) {
	ll h = hashGen(key);
	int cnt = MAX_TABLE;

	while (table[h].key[0] != 0 && cnt--) {
		if (!m_strcmp(table[h].key, key)) {
			table[h].data = data;
			return 1;
		}
		else cout << "[충돌 발생]\n";
		h = (h + 1) % MAX_TABLE;
	}

	if (cnt == -1) return 0;
	m_strcpy(table[h].key, key);
	table[h].data = data;
	return 1;
}

int hashFind(char key[], int* data) {
	ll h = hashGen(key);
	int cnt = MAX_TABLE;

	while (table[h].key[0] != 0 && cnt--) {
		if (!m_strcmp(table[h].key, key)) {
			*data = table[h].data;
			return 1;
		}
		h = (h + 1) % MAX_TABLE;
	}
	return 0;
}

int main(void) {
	while (true) {
		char key[64];
		int data;
		char c;
		cout << "[명령]\n1. 삽입\n2. 찾기\n3. 삭제\n4. 테이블 조회\n5. 종료\n→ ";
		cin >> c;

		switch (c) {
		case '1':
			cout << "[Key, Data 입력] ";
			cin >> key >> data;
			if (hashAdd(key, data)) cout << "[성공] 입력 완료\n";
			else cout << "[실패] 해시가 가득 찼습니다.\n";
			cout << "-----------------------------\n";
			break;
		case '2':
			cout << "[Key 입력] ";
			cin >> key;
			if (hashFind(key, &data)) cout << "[성공] " << data << '\n';
			else cout << "[실패] 존재하지 않는 데이터입니다.\n";
			cout << "-----------------------------\n";
			break;
		case '3':
			cout << "[Key 입력] ";
			cin >> key;
			if (hashDelete(key)) cout << "[성공] 삭제되었습니다.\n";
			else cout << "[실패] 존재하지 않는 데이터입니다.\n";
			cout << "-----------------------------\n";
			break;
		case '4':
			for (int i = 0; i < MAX_TABLE; i++)
				cout << "[" << i << "] " << table[i].key << ", " << table[i].data << '\n';
			cout << "-----------------------------\n";
			break;
		case '5':
			return 0;
		default:
			cout << "잘못 입력하였습니다.\n";
			cout << "-----------------------------\n";
			continue;
		}
	}

	return 0;
}
```
