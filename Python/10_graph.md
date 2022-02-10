

## 서로소 집합 자료구조란
* 서로소 부분 집합들로 나누어진 원소들의 데이터를 처리하기 위한 자료구조이다.
* 서로소 집합 자료구조는 두 종류의 연산을 지원한다.
  * 합집합(Union): 두개의 원소가 포함된 집합을 하나의 집합으로 합치는 연산이다.
  * 찾기(Find):특정한 원소가 속한 집합이 어느 집합인지 알려주는 연산이다.
* 서로소 집합 자료구조는 합치기 찾기(Union Find) 자료구조라고 불리기도 한다.
## 서로소 집합 자료구조 방법
* 합집합연산을 확인하여,서로 연결된 두 노드 A,B를 확인한다.
  * 1) A와 B의 루트 노드 A',B'를 각각 찾는다.
  * A'를 B'의 부모 노드로 설정한다.
* 모든 합집합연산을 처리할 때까지 1번의 과정을 반복한다.
## 서로소 집합 자료구조 연결성
* 기본적인 형태의 서로소 집합 자료구조에서는 루트 노드에 즉시 접근할 수 없다.
  * 루트 노드를 찾기 위해 부모 테이블을 계속해서 거쳐나가야 하기 때문이다.

### 서로소 집합 자료구조: 기본적인 구현 방법(Python)

```python
# 특정 원소가 속한 집합 찾기
def find_parent(parent, x):
    # 루트 노드가 아니면 루트 노드를 찾을 때까지 재귀적으로 호출
    if parent[x] != x:
        return find_parent(parent, parent[x])
    return x

# 두 원소가 속한 집합 합치기
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b


# 노드와 간선의 개수 입력 받기
v, e = map(int, input().split())
parent = [0] * (v + 1) # 부모 테이블 초기화

# 부모를 자기 자신으로 초기화
for i in range(1, v + 1):
    parent[i] = i

# Union 연산을 각각 수행
for i in range(e):
    a, b = map(int, input().split())
    union_parent(parent, a, b)

# 각 원소가 속한 집합 출력
print('각 원소가 속한 집합: ', end='')
for i in range(1, v + 1):
    print(find_parent(parent, i), end=' ')

print()

# 부모 테이블 내용 출력
print('부모 테이블: ', end='')
for i in range(1, v + 1):
    print(parent[i], end=' ')
    
'''
[Input]
6 4
1 4
2 3
2 4
5 6
[Output]
4
각 원소가 속한 집합: 1 1 1 1 5 5
부모 테이블: 1 1 2 1 5 5
'''
```