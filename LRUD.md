# 상하좌우

**내가 작성한 코드**

```python
import numpy as np

cnt = int(input())
move = input().split()
cnt = int(input())
move = input().split()

cnt_list = [list(range(1,cnt + 1))] * 5 

ary = np.array(cnt_list)

aryIdx = []

artdic = {}

for i in range(len(move)):
    if move[i] == 'R':
      artdic['R'] += 1
      aryidx[1] = +1
    elif move[i] == 'L':
      artdic['L'] += 1
      print('L {}번째 '.format(i,start))
    elif move[i] == 'U':
      artdic['U'] += 1
      print('U {}번째 '.format(i,start))
    elif move[i] == 'D':
      artdic['D'] += 1
      print('D {}번째 '.format(i,start))
cnt_list = [list(range(1,cnt + 1))] * 5 

ary = np.array(cnt_list)
```

- 이렇게 적다가 더 이상 안되서 해설을 보았다.

1. 내가 생각한 건 배열을 만들어야 겠다고 생각했다. 
2. 그래서 사용자가 입력한 수만큼 정배열을 만들었다.
3. 여기서 L,R,U,D의 숫자를 카운트해서 최종으로 행,열 방향을 입력하려고 했다. 
4. 뜻대로 안 됐다.

---

**다른 답안**

```python
cnt = int(input())
x, y = 1,1
moves = input().split()

movex = [0,0,-1,1]
movey = [-1,1,0,0]
move_type = ['L','R','U','D']

for move in moves:

  for i in range(len(move_type)):
    if move == move_type[i]:
      cntx = x + movex[i]
      cnty = y + movey[i]
  if cntx <1 or cnty < 1 or cntx > cnt or cnty > cnt    :
    continue

  x,y = cntx, cnty
print(x, y)
>
5
R R R U D D
3 4
```

