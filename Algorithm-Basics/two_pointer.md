## 투포인터
- 리스트에 순차적으로 접근해야 할 경우, 두 개의 점(포인터)의 위치를 기록하면서 처리하는 알고리즘
- 말 그대로 두 가지 포인터를 사용하여 문자열이나 배열에서 원하는 값을 찾거나 반복문을 써야 할 때 쓰기 좋은 방식
![1](https://user-images.githubusercontent.com/78436899/215311381-88dcfbc1-2eff-4888-8f6b-58c4d4bfaf74.png)

## 투포인터의 대표 예제
### < 특정한 합을 가지는 부분 연속 수열 찾기 >
**<예시 문제>**

- **아래 리스트에서 연속되는 값들을 더해 그 합이 5가 되는 경우의 수는 몇가지인가**
    
(숫자 리스트가 주어질 때, 리스트의 연속 수열의 합이 특정 값을 가지는 것을 확인하는 문제)
![2](https://user-images.githubusercontent.com/78436899/215311400-afd59136-41fc-4866-858f-fcca214ebad3.png)
<결과>
![3](https://user-images.githubusercontent.com/78436899/215311415-c26e3e2d-8b9f-4494-a3ff-ec8680fb77bf.png)
- N 개의 자연수로 구성된 수열이 있다.
- 합이 M인 부분 연속 수열의 개수를 구해라

N = 5

M = 5

결과 : 5개의 데이터가 있을 때, 부분 합이  5인 부분 연속 수열은 3가지 경우가 존재


**특정한 합의 부분 연속 수열의 개수를 구하고 싶을 때, 어떠한 방법을 사용할까 ?**



- **<완전 탐색>**
    
    ⇒ 완전탐색을 진행하면 n**2 만큼의 시간이 걸린다
    
- **<투포인터>**
    
    ⇒ 그래서 우리는 투포인터를 이용해 문제를 해결할 것이다
    
    
<풀이 과정>
![4](https://user-images.githubusercontent.com/78436899/215311430-a401a9af-e354-443d-a0f4-b5c801593100.jpg)
위의 과정을 반복하면, 아래의 결과을 도출 할 수 있다
![5](https://user-images.githubusercontent.com/78436899/215311440-5fc7b4d5-bc6f-4799-b5ea-a733feb1ceec.png)


<문제 코드>
특정 합을 가지는 부분 연속 수열 찾기 코드


```python
n = 5
m = 5
data = [1,2,3,2,5]

count = 0
interval_sum = 0
end = 0

# start를 차례대로 증가시키며 반복
for start in range(n):
	# end를 가능한 만큼 이동시키기
	while interval_sum < m and end < n :
		interval_sum += data[end]
		end += 1
	# 부분합이 m일 때 카운트 증가
	if interval_sum == m:
		count += 1
	interval_sum -= data[start]

print(count)
```

### [관련강의](https://www.youtube.com/watch?v=ttLRltNDiCo)
