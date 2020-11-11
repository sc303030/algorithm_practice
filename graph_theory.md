# 그래프_이론

### 팀 결성

**내가 작성한 코드**

```python
n,m = map(int, input().split())
num_list = [[] for _ in range(m+1)]

for i in range(m):
    zo,a,b = map(int,input().split())
    if zo == 0:
        num_list[a].append(b)
        num_list[b].append(a)
    if zo == 1:
        if b in num_list[a]:
            print('YES')
        else:
            print('NO')
```

1. 우선 n,m을 받아온다.
2. 저장할 리스트를 만든다.
3. 0이면 서로의 리스트 인덱스에 값을 넣는다.
4. 1이면 b가 a인덱스 리스트에 있는지 확인하고 해당되는 값을 출력한다.

---

**다른 답안**

```python
#특정 원소가 속한 집합을 찾기
def find_parent(parent , x):
    # 루트 노드가 아니라면, 루트 노드를 찾을 때까지 재귀적으로 호출
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]

# 두 원소가 속한 집합을 합치기
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b :
        parent[b] = a
    else:
        parent[a] = b
        
    
n, m = map(int, input().split())
parent = [0] * (n+1) # 부모 테이블 초기화

# 부모 테이블상에서, 부모를 자기 자신으로 초기화
for i in range(0, n+1):
    parent[i]  = i
    
# 각 연산을 하나씩 확인

for i in range(m):
    oper, a, b = map(int, input().split())
    # 합집합(union) 연산인 경우
    if oper == 0:
        union_parent(parent, a, b)
    # 찾기(find) 연산인 경우
    elif oper == 1:
        if find_parent(parent, a) == find_parent(parent, b):
            print('YES')
        else:
            print('NO')
```

### 도시 분할 계획

**다른 답안**

```python
# 특정 원소가 속한 집합을 찾기
def find_parent(parent, x):
    # 루트 노드가 아니라면, 루트 노드를 찾을 때까지 재귀적으로 호출
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]


# 두 원소가 속한 집합을 합치기
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b
        
# 노드의 개수와 간선(union 연산) 의 개수 입력받기
v, e = map(int,input().split())
parent = [0] * (v + 1) #부모 테이블 초기화

# 모든 간선을 담을 리스트와 최종 비용을 담을 변수
edges = []
result = 0

# 부모 테이블상에서, 부모를 자기 자신으로 초기화
for i in range(1, v + 1):
    parent[i] = i
    
# 모든 간선에 대한 정보를 입력받기
for _ in range(e):
    a, b, cost = map(int,input().split())
    # 비용순으로 정렬하기 위해서 튜플의 첫 번째 원소를 비용으로 설정
    edges.append((cost, a, b))
    
# 간선을 비용순으로 정렬
edges.sort()
last = 0 # 최소 신장 트리에 포함되는 간선 중에서 가장 비용이 큰 간선

# 간선을 하나씩 확인하며
for edge in edges:
    cost, a, b = edge
    # 사이클이 발생하지 않는 경우에만 집합에 포함
    if find_parent(parent,a) != find_parent(parent, b):
        union_parent(parent, a, b)
        result += cost
        last = cost
        
print(result - last)
>
7 12
1 2 3
1 3 2
3 2 1
2 5 2
3 4 4
7 3 6
5 1 5
1 6 2
6 4 1
6 5 3
4 5 3
6 7 4
8
```

