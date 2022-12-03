# [프로그래머스] N-Queen 파이썬

> ### 문제 설명

가로, 세로 길이가 n인 정사각형으로된 체스판이 있습니다. 체스판 위의 n개의 퀸이 서로를 공격할 수 없도록 배치하고 싶습니다.

예를 들어서 n이 4인경우 다음과 같이 퀸을 배치하면 n개의 퀸은 서로를 한번에 공격 할 수 없습니다.

![Imgur](https://i.imgur.com/lt2zdK6.png)
![Imgur](https://i.imgur.com/5c5EUrq.png)

체스판의 가로 세로의 세로의 길이 n이 매개변수로 주어질 때, n개의 퀸이 조건에 만족 하도록 배치할 수 있는 방법의 수를 return하는 solution함수를 완성해주세요.

##### 제한사항

- 퀸(Queen)은 가로, 세로, 대각선으로 이동할 수 있습니다.
- n은 12이하의 자연수 입니다.

------

##### 입출력 예

| n    | result |
| ---- | ------ |
| 4    | 2      |

##### 입출력 예 설명

입출력 예 #1
문제의 예시와 같습니다.

> ### 제출 답안

- 전형적인 백트랙킹 문제이다.
- 자세한 설명은 여기서 볼 수 있다. 
  - https://www.fun-coding.org/Chapter21-backtracking-live.html
- 설명할 부분이 많아 코드 안에 주석으로 설명을 대신한다.

```python
def is_available(candidate, current_col):
    current_row = len(candidate) # 지금까지의 Q의 개수를 파악하면 row를 알 수 있다.
    for q_row in range(current_row): # row만큼 for loop를 해야 직선, 대각선 파악이 가능하다.   
        if candidate[q_row] == current_col or abs(candidate[q_row] - current_col) == current_row - q_row:
            # candidate = [1, 2] 일 때, candidate[q_row] = 2이고 current_col = 2이면 직선이기에 놓을 수 없고
            # 대각선인 경우 (x,x)가 동일하기에 current_row=2, q_row=2면 대각선으로 겹쳐서 Q를 놓을 수 없다.
            return False
    return True


def DFS(N, current_row, current_candidate, final_result):
    if current_row == N:
        # current_row가 N이랑 같으면 Q 놓는것이 끝났다는 뜻이여서 final_result에 담는다.
        final_result.append(current_candidate[:])
        return
    
    for candidate_col in range(N):
        if is_available(current_candidate, candidate_col):
            current_candidate.append(candidate_col)
            DFS(N, current_row + 1, current_candidate, final_result)
            current_candidate.pop()


def solution(N):
    final_result = []
    DFS(N, 0, [], final_result)
    return len(final_result)
```

