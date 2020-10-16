# DFS/BFS

### 음료수 얼려 먹기

**내가 작성한 코드**

```python
n, m = map(int, input().split())

ice_list = []

stack = []
cnt=0
for i in range(n):
  ice_list.append(list(map(str,input())))
  for idx in range(m):
    if '0' == ice_list[i][idx]:
      stack.append(idx)
  if len(ice_list) >1 :
    if stack[i-1] !=  stack[i]:
          cnt +=1
          print(cnt)
```

1. 사용자로부터 세로, 가로를 받아온다.
2. 리스트에 리스트로 담아서 확인하려고 했다.
3. 만약에 만들어진 리스트에 0이 있으면 해당 인덱스 번호를 받아와서 다음 리스트 인덱스랑 비교해보려교 했다.
4. 시간초과로 실패

---

**다른 답안**

![dfs01](C:\Users\gh\algorithm_practice\DFS_BFS.assets\dfs01.PNG)

특정한 지점의 주변 상,하,좌,우를 살펴보고 0이면서 방문하지 않았으면 방문한다.

다시 반복한다.

```python
n, m = map(int, input().split())

graph = []
for i in range(n):
  graph.append(list(map(int,input())))

def dfs(x,y):
  if x <= -1 or x >= n or y <= -1 or y >= m:
    return False
  if graph[x][y] == 0:
    graph[x][y] = 1
    dfs(x - 1, y)
    dfs(x,y - 1)
    dfs(x + 1,y)
    dfs(x , y + 1)
    return True
  return False

result = 0
for i in range(n):
  for j in range(m):
    if dfs(i,j) == True:
      res(ult += 1
print(result)
```

1. 값을 받아온다.
2. 2차원의 리스트로 값을 받아온다.
3. 범위를 벗어나면 종료하고 아니면 계속 한다.
4. 노드를 방문하고 값이 0이라면 주변을 살피기 위해 재귀적으로 함수를 다시 호출한다.
5. 방문했으면 False를 리턴하고 True면 결과에 1을 추가한다.

### 미로 탈출

**내가 작성한 코드**

```python
n, m = map(int,input().split())

move_list = [(-1,0),(1,0),(0,-1),(0,1)]

miro_list=[]
for i in range(n):
  miro_list.append(list(map(int,input())))

def bfs(x,y):
  if x <= -1 or x >= n or y <= -1 or y >= m:
    return False
  if x == 0 and y == 0:
    continue
  if miro_list[x][y] == 1:
    miro_list[x][y] + = 1
    bfs(x-1,y)
    bfs(x,y-1)
    bfs(x + 1,y)
    bfs(x,y + 1)
```

1. 사용자한테 값을 받아온다.
2. 움직일 리스트를 만들었다.
3. 행의 개수만큼 2중 리스트를 만든다.
4. 만약에 좌료가 범위를 벗어나면 계속 bfs함수를 실행하게 했다.
   1. 1이면 실행하는데까지만 생각하고 시간초과

---

**다른 답안**

```python
from collections import deque

n, m = map(int,input().split())

miro_list=[]
for i in range(n):
  miro_list.append(list(map(int,input())))

dx = [-1,1,0,0]
dy = [0,0,-1,1]

def bfs(x,y):
  queue = deque()
  queue.append((x,y))
  while queue:
    x,y = queue.popleft()
    
    for i in range(4):
      nx = x + dx[i]
      ny = y + dy[i]

      if nx < 0 or ny < 0 or nx >= n  or ny >=m:
        continue
      if miro_list[nx][ny] == 0:
        continue
      if miro_list[nx][ny] == 1:
        miro_list[nx][ny] = miro_list[x][y] + 1
        queue.append((nx,ny))
  return   miro_list[n - 1][m - 1]

print(bfs(0,0))
>
5 6
101010
111111
000001
111111
111111
10
```

1. deque를 사용하기 위해 import한다.
2. 사용자에게서 n,m값을 받아온다.
3. 2중 리스트를 만들어서 해당 인덱스에 값을 저장한다.
4. 이동한 상,하,좌,우를 정의한다.
5. deque를 이용하여 인접한 열에 방문했다는 표시를 한다.
6. queue가 빌때까지 계속 while을 돌린다.
   1. 우선 처음 들어온 값을 꺼내서 상,하,좌,우 방문한다.
   2. 미로를 벗어나거나 벽이면 무시한다.
   3. 처음 방문하는 곳이면 해당 노드에 이전 노드에 +1을 한다.
   4. 그 다음에 해당 인덱스를 다시 queue에 넣고 인전하지 않은 열이 있는지 없는지 처리한 후 빠져나온다.
7. 가장 오른쪽 아래에 해당하는 인덱스를 주어서 값을 리턴한다.



