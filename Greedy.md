출처 : 이것이 취업을 위한 코딩 테스트다 with 파이썬 - 저자: 나동빈

### 큰 수의 법칙

배열 : `2,4,5,4,6` 

횟수 : 8번

최대 더 할수 있는 횟수 : 3번

배열의 크기 : 5

결과 : 6+6+6+5+6+6+6+5 = 46

---

배열 : `3,4,3,4,3` 

횟수 : 7번

최대 더 할수 있는 횟수 : 2번

배열의 크기 : 5

결과 : 4+4+4+4+4+4+4 = 28

---

**입력조건**

- 첫째 줄에 N(2 <= N <= 1,000), M(1 <= M <= 10,000), K(1<= K <= 10,000)의 자연수가 주어지며, 각 자연수는 공백으로 구분한다.
- 둘째 줄에 N개의 자연수가 주어진다. 각 자연수는 공백으로 구분한다. 단, 각각의 자연수는 1이상 10,000 이하의 수로 주어진다.
- 입력으로 주어지는 K는 항상 M보다 작거나 같다.

**출력조건**

- 첫째 줄에 동빈이의 큰 수의 법칙에 따라 더해진 답을 출력한다.

**입력예시**

```
5 8 3
2 4 5 4 6
```

**출력 예시**

```
46
```

---

**내가 작성한 코드**

```python
import numpy as np
li = [2,4,5,4,6]
li.sort(reverse=True)
array1 = np.array(li)
sum = 0
N = 5
M = 8
K = 3
count = K
for i in range(M):
  if count > 0 :
    sum += array1[0]
    count -= 1
  elif count == 0:
    sum += array1[1]
    count = K
print(sum)
```

1. 배열이라고 해서 배열로 만들었다.
2. 사용자의 값을 입력 받은게 아니라 내가 먼저 코드에 값을 주었다.
3. 숫자를 큰 순서대로 정렬해서 맨 처음 값과 두 번째 값만 사용하기로 하였다.
4. N, M, K에 예시에 있는 값을 부여하였다.
5. 그 다음에 count에 K를 복사하였다.
6. M만큼 더하는 for 루프를 작성하였다.
7. count가 0보다 크면 계속 배열의 첫 번째 값을 더한다. 그 다음에 count를 1씩 뺀다.
8. 만약에 count가 0이면 두 번째 값을 더한다. 그 다음에 다시 count를 K로 지정한다.
9. 이 과정이 끝나고 sum을 출력한다. 

값은 정확하게 나왔지만 어설프다. 

---

**다른 답안 01**

```python
n, m, k = map(int, input().split())
data = list(map(int, input().split()))

data.sort()
first = data[n - 1]
second = data[n - 2]

final = 0

while True:
  for i in range(k):
    if m == 0:
      break
    final += first
    m -= 1
  if m == 0:
    break
  final += second
  m -= 1

print(final)
```

1. input으로 숫자를 입력받아서 그 값을 n, m, k에 숫자로 저장한다.
2. data도 마찬가지로 입력받아서 저장한다.
3. data를 오름차순으로 정렬한다.
4. 배열의 길이 -1 을 하면 가장 큰 값의 인덱스랑 일치한다. 
5. 배열의 길이 -2 을 하면 가장 두 번째 큰 값의 인덱스랑 일치한다. 
6. 최대 더할 수 있는 횟수만큼 for루프를 돌린다. 
   1. 횟수가 0이되면 while을 빠져나간다.
   2. 0이 아니라면 k만큼 final에 최댓값을 더한다.
7. k만큼 더했으면 그 다음에 두 번째 큰 값을 더한다. 
8. 그 다음에 다시 또 최댓값을 더한다.
9. m을 계속 1식 빼면서 m이 0이되면 while을 빠져나간다.

m의 크기가 100억이 넘어가면 조건인 1초를 넘어버린다. 그러면 어떻게 해야 할까?

6+6+6+5 / 6+6+6+5 를 보면 반복되는 수열임을 알 수 있다.  수열의 길이가 (1 + k) 임을 알 수 있다. 

m을 (1 + k) 로 나누면 수열의 반복되는 횟수가 나온다. 여기에 k를 곱하면 가장 큰 수가 등장하는 횟수가 된다. 

딱 나눠 떨어지지 않는 경우에는 m * (1 + K) 의 나머지만큼 최댓값을 더해준다. 

**식이 만들어 진다**

```
int(m / (1 + k)) * k + m % (1 + k)
```

 **다른 답안 02**

```python
n, m, k = map(int, input().split())
data = list(map(int, input().split()))

data.sort()
first = data[n - 1]
second = data[n - 2]

count = int( m / (k + 1)) * k
count += m % (k + 1)

final = 0
final += (count) * first
final += (m - count) * second

print(final)
```

1. count에 나누어 떨어지는 경우를 저장한다.
2. 그 다음에 나머지 만큼 최댓값을 더해주는 경우를 저장한다.
3. final에 최댓값을 먼저 곱해서 저장한다.
4. 그 다음에 최댓값을 더하고 남은 횟수에 두 번째로 큰 값을 곱해서 저장한다. 



### 숫자 카드 게임

> 여러 개의 숫자 카드 중에서 가장 높은 숫자가 쓰인 카드 한 장을 뽑는 게임이다. 
>
> > 행을 선택하면 그 행에서 가장 작은 수를 선택한다. 어떤 행을 선택해야 행에서는 가장 작으면서 배열에서는 가장 큰 수일까?

```
3 1 2
4 1 4
2 2 2
```

- 카드를 고를 행을 선택한다. 예제에서 1행과 2행을 선택한다면 `1` 을 선택해야한다.
- 하지만 3행을 선택하면 `2` 를 선택할 수 있다. 
- 따라서 3행을 선택해 `2` 를 선택하는것이 정답이다. 

---

**입력 조건**

- 첫째 줄에 숫자 카드들이 놓인 행의 개수 N과 열의 개수 M이 공백을 기준으로 하여 각각 자연수로 주어진다. (1 <=N, M<=100)
- 둘째 줄부터 N개의 줄에 걸쳐 각 카드에 적힌 숫자가 주어진다. 각 숫자는 1이상 10,000이하의 자연수이다.

**출력 조건**

- 첫째 줄에 게임의 룰에 맞게 선택한 카드에 적힌 숫자를 출력한다. 

**입력 예시1**

```
3 3
3 1 2 
4 1 4
2 2 2
```

**출력 예시 1**

```
2
```

**입력 예시2**

```
2 4
7 3 1 8
3 3 3 4
```

**출력 예시2**

```
3
```

---

**내가 작성한 코드**

```python
n,m = map(int, input().split())
data = [ sorted(list(map(int, input().split()))) for i in range(n) ]
min_data = [ data[i2][0] for i2 in range(n)]
result = max(min_data)

print(result)
```

1. 우선 `input` 으로 행과 열을 받아온다.
2. 행의 개수만큼 값을 받아온다. 리스트안에 for루프들 돌려서 바로 저장했다. 
   1. 리스트 안에 리스트를 저장하는 형식이다.
   2. 그 값을 바로 오름차순 해버린다. 
   3. 그러면 맨 앞에 있는 값들만 비교하면 된다.

3. 만들어진 리스트안에 리스트들의 값을 비교한다. 
   1. 행의 개수만큼 [0]번째 값을 찾으면 된다.
4. 최솟값만 모인 리스트에서 최댓값을 찾는다.

---

**다른 답안 1 **

```python
n,m = map(int, input().split())

final = 0
for i in range(n):
  data = list(map(int, input().split()))
  min_data = min(data)
  final = max(final, min_data)
print(final)
```

1. 행과 열을 받아온다.
2. 행의 개수만큼 for루프를 돈다.
   1. 데이터를 리스트로 받아온다.
   2. 받아왔을 때 바로 최솟값을 찾는다.
   3. 그 다음에 `final` 과 최솟값을 비교해서 최댓값을 `final` 에 담는다.

**다른 답안2**

```python
n,m = map(int, input().split())

final = 0
for i in range(n):
  data = list(map(int, input().split()))
  min_data = 10001
  for a in data:
    min_data = min(min_data, a)
  final = max(final, min_data)

print(final)
```

1. 행과 열을 받아온다.
2. 행의 개수만큼 for루프를 돈다.
   1. 데이터를 리스트로 받아온다.
   2. 최솟값을 우리가 조건에 걸었던 숫자보다 1크게 지정한다.
   3. 다시 `data` 를 for루프 돌린다. 
      1. 여기서 `data` 의 값 하나씩과 최솟값을 비교한다.
   4. `data` 의 루프가 끝나면 최솟값이 나온다.
3. 그 값과 `final` 의 최댓값을 담는다.



### 1이 될 때까지

> 어떠한 수 N이 1이 될 때까지 두가지 과정 중 하나를 선택하여 수행한다.

1. N에서 1을 뺀다.
2. N을 K로 나눈다. 단, N이 K로 나누어떨어질 때만 선택할 수 있다.

예를 들어 N=17, K=4이면 

1. 17-1 = 16
2. 16 / 4 = 4
3. 4 / 4 = 1

총 3번의 과정을 수행한다. 최소 횟수를 구하는 프로그램을 작성하자.

---

**입력 조건**

- 첫째 줄에 N(2<= N <= 100,000)과 K(2 <= K <= 100,000)가 공백으로 구분되며 각각 자연수로 주어진다. 이때 입력으로 주어지는 N은 항상 K보다 크거나 같다.

**출력 조건**

- 첫째 줄에 N이 1이 될 때까지 1번 혹은 2번의 과정을 수행해야 하는 횟수의 최솟값을 출력한다.

**입력 예시**

\> **출력 예시**

```
25 5
> 2
```

---

**내가 작성한 코드**

```python
n,k = map(int, input().split())
cnt= 0
while n > 1:
  if n % k != 0:
    n -=1
    cnt += 1
  else:
    n = n / k
    cnt += 1

print(cnt)
>
25 5
2
```

1. 우선 n과 k 에 값을 받아온다. 
2. cnt에 횟수를 담는다.
3. 만약 n이 1보다 크다면 계속 진행하라.
   1. n을 k로 나누었을 때 0이 아니면 1을 빼고 1이면 n을 k로 나눈다.
4. 최종 결과를 출력한다.

---

**다른 답안 1**

1을 빼는 것보다 2이상의 수로 나누는 것이 더 효율적이다. 

그러니 N을 K로 최대한 나눌 수 있도록 하는 것이 최적의 해를 보장한다.

```python
n, k = map(int,input().split())
cnt = 0

while n >= k:
  while n % k != 0:
    n -= 1
    cnt += 1
  n //= k
  cnt += 1

while n > 1:
  n -= 1
  cnt += 1
print(cnt)
>
25 5
2
```

1. 우선 n과 k 에 값을 받아온다. 
2. cnt에 횟수를 담는다.
3. n이 k보다 크면 반복한다.
   1. n을 k로 나누었을 때 나머지가 0이 아니면 -1을 하고 0이면 k로 나눠서 정수 몫만 가져온다. 
4. 그 후에 n에서 1씩 뺀다. 최대한 나누고 마지막에 1씩 빼는게 더 효율적이다.
5. 최종 횟수를 출력한다. 

**다른 답안 2**

```python
n, k = map(int, input().split())
cnt = 0

while True:
  n2 = (n // k) * k
  cnt += (n - n2)
  n = n2

  if n < k:
    break
  cnt += 1
  n //= k
cnt += (n - 1)
print(cnt)
```

1. 우선 n과 k 에 값을 받아온다. 
2. cnt에 횟수를 담는다.
3. n이 k보다 작아지면 나가도록 작성한다.
   1. n에 계속 작아지는 값을 담는다.
      1. (25 // 5 = 5) * 5 = 25
      2. 25 - 25 = 0
      3. 25 = 25
      4. 25 // 5 = 5
   2. (5 // 5 = 1) * 5 = 5
      1. 5 - 5 = 0
      2. 5 = 5
      3. 5 // 5 = 1
   3. (1 // 5 = 0) * 5 = 0
      1. 1 - 0 = 1
      2. 0 = 0
4. n이 k보다 작아졌기에 while을 나간다.
5. 마지막으로 3-1 = 2를 하고 값을 출력한다.
