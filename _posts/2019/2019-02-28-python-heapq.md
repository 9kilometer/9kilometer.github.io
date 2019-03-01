---
title: "[Python] 파이썬 기본 모듈 - heapq"
# excerpt: ""
# header: 
#     overlay_image: /assets/resources/post_header.jpg
last_modified_at: 2019-02-28T23:00:00
category: PYTHON
tag: 
    - python
    - heap
---

파이썬의 `heapq` 모듈은 최소 힙 자료구조를 구현하기 위한 기능들을 제공한다.  

여기서 힙은 모든 노드가 자식 노드보다 작거나 같은 이진 트리다. 이를 0부터 시작하는 배열로 보면, `heap[k] <= heap[2*k + 1]` 이며, `heap[k] <= heap[2*k +2]` 이다. 또한 트리의 루트인 `heap[0]` 이 배열에서 가장 작은 값이 된다.  


### 모듈 사용하기
내장 모듈이기 때문에 별도의 설치 없이 import 후 사용하면 된다.
```python
import heapq
```

### 힙 생성하기
`heapq` 모듈은 파이썬의 리스트를 최소 힙처럼 다룰 수 있게 해줄 뿐이다. 따로 최소 힙을 구현한 클래스가 있는건 아니다.  
빈 리스트도, 채워진 리스트도 힙처럼 쓸 수 있다. 비어있는 힙을 만들고 싶으면, 그냥 빈 리스트를 준비하면 된다.    
이미 채워진 리스트에 `heapify()` 함수를 쓰면 힙 정렬된 리스트로 바뀐다.  
```python
# 빈 힙을 만들고 싶으면 그냥 빈 리스트를 준비!
heap = []
# 채워진 리스트를 힙으로 사용하고 싶다면
heap_2 = [4, 2, 5, 1]
heapq.heapify(heap_2)
print(heap_2)  # 출력 : [1, 2, 5, 4]
```

### 값 추가
`heappush()` 함수로 값을 추가할 수 있다. 첫 번째 인자에 리스트를, 두 번째 인자에 추가할 값을 넘긴다.
```python
heapq.heappush(heap, 4)
heapq.heappush(heap, 2)
heapq.heappush(heap, 5)
heapq.heappush(heap, 1)
print(heap) # 출력 : [1, 2, 5, 4]
```

### 최소 값 제거
`heappop()` 함수는 힙에서 최소값을 제거하고 반환한다. (제거하고 남은 값들로 다시 힙 트리를 만든다.)  
최소값을 제거하지 않고 보고만 싶은거면, `heap[0]`을 쓰면 된다. 그냥 리스트니까!
```python
print(heapq.heappop(heap)) # 출력 : 1
print(heap) # 출력 : [2, 4, 5]
```

### 그 외의 함수들
그 외에 값을 push하고 pop하는 `heappushpop()`, pop하고 값을 push하는 `heapreplace()` 라던가,(push와 pop의 순서가 다르다)  
리스트에서 n번째 큰/작은 값을 반환하는 `nlargest()`, `nsmallest()` 등이 있다. 자세한 정보는 참조의 문서 등을 확인하자.  

---
### 참조
- https://docs.python.org/3.6/library/heapq.html