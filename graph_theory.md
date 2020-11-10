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

