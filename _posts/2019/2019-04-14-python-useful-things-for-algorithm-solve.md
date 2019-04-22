---
title: "[PYTHON] 코딩 테스트에서 쓸만한 기능들 모음"
last_modified_at: 2019-04-22T00:00:00
category: record
tag: 
    - PYTHON
    - algorithm
---

파이썬 기본 함수나 모듈 중 코딩 테스트를 풀 때 쓸만했던 것들을 생각나는 대로 적는 중 입니다.
{: .notice--info}

## Built-in Functions
---
### divmod
나누기의 몫과 나머지를 한 번에 리턴.  
결과적으론 `divmod(n,d)`는 `n//d`, `n%d`와 같은데, 성능 차이가 좀 있다고 한다.  
작은 수의 경우는 연산자를 쓰는게 더 빠르고, 매우 큰 수는 `divmod`가 빠르다고 한다. [관련글](https://stackoverflow.com/questions/30079879/is-divmod-faster-than-using-the-and-operators)  
그렇지만 코딩 테스트 수준에서 저게 크게 영향 미칠 것 같진 않고... 편한대로 쓰면 될 듯.  
```python
q, r = divmod(10,3)  # q = 3, r = 1
q, r = 10//3, 10%3
```

---
### zip
주어진 iterable 객체들의 각 요소가 하나씩 들어간 tuple의 iterator를 리턴.  
즉, i번째 tuple에는 각 객체에서의 i번째 원소가 들어있다.  
반환되는 tuple의 갯수는 원소의 갯수가 가장 적은쪽에 맞춰진다. 가장 긴 쪽에 맞추고 싶다면 `itertools.zip_longest`를 쓴다.  
```python
list(zip('ABCD', 'xy'))  # 원소의 갯수가 적은 'xy'에 맞게 tuple이 2개만 생성
# [('A', 'x'), ('B', 'y')]
```
<br>
## set
---
```python
# set 생성
s = set()
```

set은 hashable한 값들만 받는다. 때문에 list 타입 등은 set의 원소로 넣을 수 없음. 대신 tuple로 변환하면 넣을 수 있다.   
```python
>>> set([1, 2, 3])  # [1, 2, 3]의 각 원소는 int 타입이므로 set에 넣을 수 있음.
{1, 2, 3}

>>> set([[1, 2, 3]])  # [[1, 2, 3]]의 원소는 [1,2,3]이라는 list 타입 변수이므로 에러 발생.
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
```
---
#### union, intersection, difference
두 집합의 합집합, 교집합, 차집합을 구하는 함수.  
각각 `|`, `&`, `-` 연산자와 같은 결과가 나온다.  
```python
# 아래 두 결과가 동일
set([1,2,3]) & set([2,3,4])  # {2, 3}
set([1,2,3]).intersection(set([2,3,4]))
```

---
#### issubset & issuperset, isdisjoint
issubset, issuperset: 집합이 다른 집합에 속하는 지 여부를 리턴  
isdisjoint: 두 집합 간 교집합이 없으면 True 리턴  
```python
>>> set([1,2]).issubset(set([1,2,3]))  # 집합 (1,2)는 (1,2,3)의 부분집합
True
>>> set([1,2,3]).issuperset(set([1,2]))
True
>>> set([1,2,3]).isdisjoint(set([4,5]))
True
```

<br>
## itertools
---
```python
import itertools
```

---
### combinations
주어진 iterable 객체에서 주어진 길이에 대한 모든 조합을 리턴.  
중복 가능한 조합을 구하고 싶으면 `combinations_with_replacement`가 있다.
```python
for c in itertools.combinations(['A','B','C'], 2):  # A,B,C 세 개의 원소 중 두 개를 뽑는 경우의 수 = 3가지
  print(c)  # ('A','B') / ('A','C') / ('B','C')

for cr in itertools.combinations_with_replacement(['A','B','C'], 2):
  print(c)    # 중복 가능이므로 ('A','A') 등도 포함.
```

---
### permutations
주어진 iterable 객체에서 주어진 길이에 대한 모든 순열을 리턴.  
```python
for p in itertools.permutations(['A','B','C'], 2):  # A,B,C 세 개의 원소 중 두 개로 만들 수 있는 순열의 수 = 6가지
  print(p)  # ('A','B') / ('A','C') / ('B','A') / ('B','C') / ('C','A') / ('C','B')
```

---
### product
주어진 iterable 객체들에 대한 모든 Cartesian product(곱 집합)를 리턴.  
이를 이용하면 이중 이상의 for문을 한 줄의 for문으로 대체할 수 있으니 인덴테이션도 줄어들어 보기에 좋다.  
```python
list_1, list_2 = [1,2,3,4], ['a','b','c']

# 이중 for문으로 리스트들의 각 원소에 대한 모든 조합 구하기
for i in list_1:
  for k in list_2:
    print(i,k)

# product를 이용해 모든 조합 구하기. 위의 방식보다 간결하다.
for i,k in itertools.product(list_1, list_2):
  print(i,k)

# generator도 쓸 수 있다. 다차원 배열을 순환할 때 써먹을 수 있다.
for y,x in itertools.product(range(2), range(3)):
  print(x,y)

# 000 ~ 111 까지 1씩 증가하는 2진수 구하기
for i in itertools.product(range(2), repeat=3):
  print(i)
```

---
### compress
주어진 iterable 객체의 원소들 중 `selectors`에서 같은 인덱스의 원소가 참인 것만 뽑아 만든 iterator 리턴.  
여기서 참은 `True` 뿐 아니라 `True`로 평가되는 것이면 됨. (ex. 0은 False, 1은 True)  
```python
list(itertools.compress('ABCDEF', [1,0,1,0,1,1]))  # 두 번째 매개변수가 selectors 다.
#  ['A', 'C', 'E', 'F']
list(itertools.compress('ABCDEF', [1,0,1,0]))  #  첫 매개변수의 길이가 더 길면, 남는 원소들은 알아서 필터링에서 걸러지는 듯.
#  ['A', 'C']
```

---
### zip_longeset
기본 내장함수인 `zip`과 다르게 원소의 갯수가 가장 큰 객체에 맞게 tuple이 생성되며, 빈 값은 `fillvalue`로 매꿔진다.  
```python
list(itertools.zip_longest('ABCD', 'xy', fillvalue='-'))
# [('A', 'x'), ('B', 'y'), ('C', '-'), ('D', '-')]
```
<br>
## sys
---
```python
import sys
```

---
### 재귀횟수 제한 설정 
재귀로 문제를 풀었는데 몇 테스트케이스에서만 런타임 에러가 난다? 최대 재귀 스택 제한에 걸린 것일 수 있으니 제한을 늘려본다.  
참고로 기본 제한은 1000번 이다.(플랫폼마다 다를 수도) 무한 재귀를 막기 위해 설정된 것.  
그렇다고 무작정 높이지는 말자. 크래시 날 수도 있으니까...  
```python
sys.setrecursionlimit(10**4)
```