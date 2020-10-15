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