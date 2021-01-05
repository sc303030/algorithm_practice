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

- 굳이 배열을 만들지 않아도 됐었다.

1. 우선 사용자로부터 행,열을 만들 개수를 받아온다.
2. x와 y좌료를 (1,1)로 설정한다.
3. 움직일 방향의 문자를 받아온다.
4. x좌표로 움직일 리스트와 y좌표로 움직일 리스트를 만든다.
5. 해당 리스트 인덱스와 일치하도록 움직일 방향 문자를 리스트로 만든다.
6. 사용자가 입력한 움직이는 방향 리스트에서 문자를 하나씩 꺼내온다.
   1. 그 안에서 기존에 설정한 방향과 비교한다.
   2. 문자가 일치하면 해당 인덱스에 있는 값을 더한다.
   3. 만약 값이 좌표를 벗어나면 x와 y에 다시 반영하는 것 없이 다시 루프를 돈다.
7. 최종으로 프린트한다.



# 시각

**내가 작성한 코드**

```python
num = int(input())

sec = 0
min = 0
hour= 0

cnt = 0


for idx in range(num):
  hour += 1
  if str(hour)[0] == '3':
    cnt +=1
  if str(hour)[1] == '3':
    cnt += 1
  while min < 60:
    min += 1
    if str(min)[0] == '3':
      cnt +=1
    elif str(min)[1] =='3':
      cnt += 1
    while sec < 60:
      sec +=1
      if str(sec)[0] == '3':
        cnt +=1
      elif str(sec)[1] == '3':
        cnt +=1
```

- 시간 , 분, 초를 1씩 증가시켜서 인덱스마다 3과 일치하면 담으려고 했다.
  - 인덱스가 범위를 벗어났다며 오류를 냈다.
  - 시간 초과로 풀지 못하였다.

---

**다른 답안**

- 모든 시각의 경우를 하나씩 모두 세면 된다.
- 단순히 시각을 1씩 증가시키면서 3이 하나라도 포함되면 카운트한다.
- 시간, 분,초는 24 * 60 * 60루프를 돌면 된다.
- 이러한 유형은 완전 탐색유형으로  분리되기도 한다.

```python
h = int(input())

cnt = 0
for i in range(h + 1):
  for j in range(60):
    for k in range(60):
      if '3' in str(i) + str(j) + str(k):
        cnt +=1

print(count)
```

1. 시간을 받아온다.
2. 맨 처음에 시간의 루프를 돌린다
3. 분의 루프를 돌린다
4. 초의 루프를 돌린다
   1. 여기서 만약 문자열로 바꾼 시간, 분, 초를에 3이 있으면 카운트 한다.
   2. 내가 위에서 생각했던 것은 꼭 3과 일치 해야한다는 생각이었는데 문자열이니 3이라는 문자가 있으면 되는 것이었다.



# 왕실의 나이트

**내가 작성한 코드**

```python
col, row = input()
row = int(row)
num_list = [-2,2]
cnt = 0
col_list = {'a' : 1, 'b' : 2 ,'c' : 3, 'd' : 4, 'e': 5 ,'f' : 6, 'g' : 7 ,'h' : 8}

for i in range(8):
    if ((row + 2 ) <=8 or (row - 2 ) >= 1)  and ((col_list[col] + 2 ) <= 8 or(col_list[col] -2 ) >= 1):
      cnt +=1
    
print(cnt)
```

1. 사용자에게서 열과 행을 받아와서 따로 따로 저장한다.
2. 행은 다시 숫자로 바꿔준다.
3. 딕셔너리로 열 알파벳에 숫자를 부여해서 하려고 하였다.
4. 행에 +2,-2 그리고 열에 +2, -2를 하여 이것이 범위를 넘어가지 않으면 `cnt +=1` 을 하려고 하였다.
5. 끝내 풀지 못하고 시간 초과하였다.

---

**다른 답안**

- 위 `상하좌우` 문제랑 비슷하다.
- 규칙에 의해 총 8가지의 경우가 나온다.
  - `(-2, -1),(-1,-2),(1,-2),(2,-1),(2,1),(1,2),(-1,2),(-2,1)`  로 움직일 수 있다.
- 사용자에게서 받은 열과 행에 더해주고 하나씩 확인한다.

```
input_data = input()
row = int(input_data[1])
column = int(ord(input_data[0])) - int(ord('a')) + 1

steps = [(-2, -1),(-1,-2),(1,-2),(2,-1),(2,1),(1,2),(-1,2),(-2,1)]

cnt = 0
for step in steps:
  next_row = row + step[0]
  next_col = column + step[1]

  if next_row >= 1 and next_row <= 8 and  next_col >= 1 and  next_col <= 8:
    cnt +=1

print(cnt)
>
c2
6
```

1. 사용자에게서 데이터를 받아온다.
2. 인덱싱을 통해 `[1]` 에 있는 문자를 숫자로 바꿔준다. 행이 될 것이니깐
3. 인덱싱을 통해 `[0]` 에 있는 문자를 다음과 같이 처리한다.
   1. **`ord`** : 문자의 아스키 코드값을 돌려주는 함수이다.
   2. 그래서 사용자가 입력한 열의 문자에서  `a` 의 아스키  코드를 빼고 `+1` 을 하면 해당 열이 몇 번째인지 알수 있다.
4. `steps` 에 8가지의 움직일 수 있는 경우의 수를 부여한다.
5. `for` 루프를 돌린다
   1. `step` 에 있는 값들을 행과 열에 더한다.
   2. 열과 행이 1보다 크고 8보다 작으면 `cnt +=1` 을 한다.
6. 최종 프린트한다.



# 게임 개발

**내가 작성한 코드**

```python
n, m = map(int,input().split())
x, y , start = map(int,input().split())
location = []
loc = []

foot = 0

steps = [(-1,0),(0,1),(1,0),(0,-1)]

for i in range(n):
  a = list(map(int, input().split()))
  for i in a:
    loc.append(i)
  location.append(loc)
  loc = []

if start == 0:
  foor = 2
  dx, dy = x,y
  dx, dy = steps[0]
  if location[dx][dy] == 1:
    location[dx][dy] = location[x][y]
    start = 3
>
4 4
1 1 0
1 1 1 1
1 0 0 1
1 1 0 1
1 1 1 1
```

1. 사용자에게서 행과 열을 받아온다.
2. 캐릭터의 좌표와 시작방향을 받아온다.
3. 행을 끊어서 리스트 안에 리스트로 담는다.
4. 움직인 것을 구하기 위해 foot을 만들었다.
5. 동서남북을 생각해서 steps을 만들었다.
6. 그 다음에 행 만큼 루프를 돌려서 좌표를 바다와 육지를 받는다.
7. 받아온 후에 움직이는 루프를 만들었지만 시간을 초과하였다....
   1. 우선 동,서,남,북 다 만드려고 했었다.
   2. 그 다음에 내가 만든 리스트의 인덱스에 해당하는 행에서 열을 빼오는 형식으로 만들었다.

---

**다른 답안**

- 전형적인 시뮬레이션 문제이다.
- 별도의 알고리즘 보다는 요구하는 내용을 오류없이 성실하게 구현하면 할 수 있다.
- 별도의 dx, dy좌표를 리스트로 만들어 방향을 정하면 효과적이다.
- 리스트 컴프리헨션으로 2차원 리스트를 초기화 하였는데 파이썬에서 2차원 리스트를 선언할 때는 컴프리헨션을 사용하는 것이 효과적이다.

```python
n, m = map(int,input().split())

d = [[0] * m for _ in range(n)]

x, y , start = map(int,input().split())
d[x][y] = 1

array = []
for i in range(n):
  array.append(list(map(int, input().split())))

dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]

def turn_left():
  global start
  start -= 1
  if start == -1:
    start = 3

cnt = 1
turn_time = 0
while True:
  turn_left()
  nx = x + dx[start]
  ny = y + dy[start]

  if d[nx][ny] == 0 and array[nx][ny] == 0:
    d[nx][ny] = 1
    x = nx
    y = ny
    cnt +=1
    turn_time = 0
    continue
  else:
    turn_time += 1
  if turn_time == 4:
    nx = x - dx[start]
    ny = y - dy[start]
    if array[nx][ny] == 0 :
      x = nx
      y = ny
    else:
      break
    turn_time = 0
print(cnt)
>
4 4 
1 1 0
1 1 1 1
1 0 0 1
1 1 0 1
1 1 1 1
3
```

1. 사용자에게서 행과 열을 받아온다. 
2. 그 다음에 전체 행과 열을 0으로 만들어 버린다.
3. 좌표와 시작 지점을 받아온다.
4. 북,동,남,서 방향으로 움직이는 리스트를 만든다.
5. 왼쪽으로 도니깐 왼쪽으로 도는 함수 하나를 생성한다.
   1. global을 사용하여 전역변수로 만든다.
   2. 그러면 다른 곳에서도 `start` 를 쓸 수 있다.
6. 맨 처음에 왼쪽으로 돈 다음 해당 시작 지점을 더한다.
7. 만약에 움직였는데 처음가는 곳이면 움직인다. 동시에 움직인 횟수를 추가한다.
8. 만약에 돌았는데 갔던 곳이나 바다면 다시 돈다.
9. 4번 다 돌았으면 뒤로 한 칸간다. 여기서 뒤가 바다면 while을 끝낸다.
10. 최종 횟수를 출력한다.