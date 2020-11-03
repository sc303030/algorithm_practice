# 미래도시

**내가 작성한 답안**

```python
INF = int(1e9)

n, m = map(int,input().split())

company_root = [[INF] * (n + 1) for _ in range(n+1)]

for a in range(1, n+1):
    for b in range(1,n + 1):
        if a == b:
            company_root[a][b] = 0
                
for i in range(m+1):
    if  i < m:
        a,b = map(int, input().split())
        company_root[a][b] = 1
        company_root[b][a] = 1
    else:
        x,k = map(int, input().split())

keys = [i for i in range(1,n+1)]
cnt = dict.fromkeys(keys,0)

for i in range(1,n + 1):
    if company_root[1][i] == 1:
        for a in range(2,n + 1):
            if i == a:
                if company_root[a][k] == 1 or company_root[a][x] == 1:
                    cnt[a] +=1
                    for b in range(2,n + 1):
                        if a == b:
                            if company_root[b][k] == 1:
                                cnt[b] +=1
                                for c in range(2,n + 1):
                                    if b == c:
                                        if company_root[c][x] == 1:
                                            cnt[c] +=1
                                            print(cnt.get(c))
```

1. n과 m을 받아서 무한대 값을 가지는 리스트를 n+1만큼 만든다.
2. 시간이 1만큼이니 대칭행렬이다. 
   1. 그래서 a,b 서로 1을 가진다.
   2. m+1값은 x,k값으로 할당한다.
3. 우선 1과 연결된 노드를 찾고 그 노드에서 다시 x와 k값을 가지는 노드를 찾고 거기서 또 k와 연결된 것을 찾고 마지막으로 x와 연결된 것을 찾았다.
4. 값은 나오는데 -1을 구하는것을 못했다.

---

**다른 답안**

```python
INF = int(1e9)

n, m = map(int,input().split())

company_root = [[INF] * (n + 1) for _ in range(n+1)]

for a in range(1, n+1):
    for b in range(1,n + 1):
        if a == b:
            company_root[a][b] = 0
for i in range(m+1):
    if  i < m:
        a,b = map(int, input().split())
        company_root[a][b] = 1
        company_root[b][a] = 1
    else:
        x,k = map(int, input().split())   
for k in range(1, n+1):
    for a in range(1, n+1):
        for b in range(1, n+1):
            company_root[a][b] = min( company_root[a][b],  company_root[a][k] +  company_root[k][b])
distance = company_root[1][k] + company_root[k][x]

if distance >= INF:
    print("-1")
else:
    print(distance)
```

1. n과 m을 받아서 무한대 값을 가지는 리스트를 n+1만큼 만든다.
2. 시간이 1만큼이니 대칭행렬이다. 
   1. 그래서 a,b 서로 1을 가진다.
   2. m+1값은 x,k값으로 할당한다.
3. 목적지까지 도달하는데 어떻게 건너건너 가면 거기로 도착할수 있는지 플로이드 워셜을 사용해서 구한다.
   1. 5번으로 가려면 4번을 거치거나 3번을 거쳐야 한다. 그래서 이 거리를 더하면 된다.
   2. 4에 도달하기까지 이렇게 하면 된다.
4. k다음에 x에 가야하니 `company_root[1][k] + company_root[k][x]` 이렇게 구한다.
5. 만약에 겹치는게 없었으면 무한대 값을 가지고 있을데니 -1일 출력하고 값이 있으면 해당 값을 출력한다.