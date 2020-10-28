# Dynamic_Programming

### 1로 만들기

**내가 작성한 코드**

```python
n = input()

while n != 1:
    if n > 3:
        a,b = divmod(n,5)
    
```

1. n을 받아서 큰 수인 5부터 나눠서 하려고 했지만 실패했다.

---

**다른 답안**

```python
n = int(input())

d = [0] * 30001

for i in range(2,n + 1):
    d[i] = d[i - 1] + 1
    if i % 2 == 0:
        d[i] = min(d[i],d[i // 2]+1) 
    if i % 3 == 0:
        d[i] = min(d[i],d[i // 3]+1) 
    if i % 5 == 0:
        d[i] = min(d[i],d[i // 5]+1) 
print(d[n])
>
26
3
```

1. n을 받는다.
2. 방문했다는 메모이제이션을 만든다.
3. 2부터 n+1까지 돌린다.
   1. 1부터 i를 2,3,4로 나눈 값중에서 작은 값을 택한다.
   2. +1은 계산 횟수를 넣어야 하기 때문에 추가한다.
   3. i = 2일때 d[2] = d[1] (0) + 1 = 1, 2는 2로 나누어 지니깐 d[2] (1) 과 d[1] + 1 = 1중에 작은 값이면 1이다.
   4. i = 3일때 d[3] = d[2] (1)+ 1 = 2, 3은 3으로 나누어 지니깐 d[3] (2) 와 d[1] (0) + 1 = 1중에 작은 1이 선택된다.
4. 이렇게 n+1까지 해나간다.

### 개미전사

```python
n = int(input())
food_list = list(map(int,input().split()))

food_asc = sorted(food_list)
food_desc = sorted(food_list,reverse=True)

result = []

for i in range(n):
    result.append(food_asc[i])
    if len(result) < n:
        result.append(food_desc[i])
    if len(result) == n:
        break
result = result[1::2]
print(sum(result))
>
4
1 3 1 5
8
```

1. 식량창고의 개수를 받아온다.
2. 오름차순과 내림차순의 리스트를 만든다.
3. 서로 번갈아가며 리스트에 삽입되게 한다.
4. 완성된 리스트의 맨 처음은 최소값이니 1부터 2번째 떨어트려 값을 구해 더한다.

---

**다른 답안**

```python
n = int(input())
food_list = list(map(int,input().split()))

d = [0] * 100

d[0] = food_list[0]
d[1] = max(food_list[0], food_list[1])

for i in range(2,n):
    d[i] = max(d[i-1], d[i-2] + food_list[i])
    
print(d[n - 1])
```

1. 식량창고의 개수를 받아온다.
2. 식량 정보를 받는다.
3. DP테이블 초기화 한다.
4. 맨 처음 식량을 가져 갈지, 2번째 식량을 가져 갈지 max로 구한다. 
   1. 그러면 다음부터 어디를 털 지 정해진다.
5. 2부터 시작해서 앞에 있는 식량이 더 큰지, 현재 인덱스값과 앞앞칸을 더한게 큰지 비교한다.

6. 인덱스는 n-1을해줘야 그 자리값이다.