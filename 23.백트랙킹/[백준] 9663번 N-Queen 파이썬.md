# [백준] 9663번 N-Queen 파이썬

> ### 문제

N-Queen 문제는 크기가 N × N인 체스판 위에 퀸 N개를 서로 공격할 수 없게 놓는 문제이다.

N이 주어졌을 때, 퀸을 놓는 방법의 수를 구하는 프로그램을 작성하시오.

##### 입력

첫째 줄에 N이 주어진다. (1 ≤ N < 15)

##### 출력

첫째 줄에 퀸 N개를 서로 공격할 수 없게 놓는 경우의 수를 출력한다.

##### 예제 입력 1

```
8
```

##### 예제 출력 1

```
92
```

> ### 제출 답안

```python

'''
1. 아이디어
- 처음에 퀸을 놓는다.
- 그 다음 행에 퀸을 놓았을 때 같은 행이 아닌지, 대각선에 겹치지 않는지 확인한다.
2. 시간 복잡도
- N!
3. 변수
- result []
- candidate []
'''

import sys
input = sys.stdin.readline

def is_avaliable(row):
    for q_row in range(row):
        if candidate[row] == candidate[q_row] or abs(candidate[row] - candidate[q_row]) == row - q_row:
            return False
    return True

def dfs(row):
    global result
    if row == n:
        result += 1
        return
    for col in range(n):
        candidate[row] = col
        if is_avaliable(row):
            dfs(row+1)

n = int(input())
result = 0
candidate = [0] * n
dfs(0)

print(result)
```

