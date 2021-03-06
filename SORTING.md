# 정렬

### 위에서 아래로

**내가 작성한 코드**

```python
n = int(input())

num_list = []

for i in range(n):
  num_list.append(int(input()))

num_list.sort(reverse=True)

for i in num_list:
  print(i, end=' ')
>
3 
15
27
12
27 15 12 
```

1. 몇 번 데이터를 저장할 지 받아온다.
2. 루프로 데이터를 리스트에 저장한다.
3. 데이터를 내림차순으로 정렬한다.
4. 공백을 기준으로 데이터를 print 한다.

---

**다른 답안**

```python
n = int(input())

array =[]
for i in range(n):
  array.append(int(input()))

array = sorted(array, reverse=True)

for i in array:
  print(i, end=' ')
>
3
15
27
12
27 15 12 
```

1. 몇 번 데이터를 저장할 지 받아온다.
2. 루프로 데이터를 리스트에 저장한다.
3. 리스트를 내림차순으로 정렬한다.
4. 공백으로 데이터를 print 한다.

### 성적이 낮은 순서로 학생 출력하기

**내가 작성한 코드**

```python
n = int(input())

name_list= []
score_list = []

for i in range(n):
  name, score = input().split()
  name_list.append(name)
  score_list.append(int(score))

sort_list = sorted(score_list)

for i in range(len(sort_list)):
  for j in range(len(score_list)):
    if score_list[j] == sort_list[i]:
      print(name_list[j], end=' ')
>
2
홍길동 95
이순신 77
이순신 홍길동 
```

1. 리스트의 개수를 받아온다.
2. 이름과 점수를 담을 리스트를 만든다.
3. 루프로 n번만큼 리스트에 이름과 점수를 저장한다.
4. 그 리스트를 정렬한 다음 새로운 변수에 저장한다.
5. 2중 루프를 돌려 정렬한 리스트랑 비교하여 이름을 출력한다.

- 여기서 O(NlogN)을 보장하거나 O(N)을 보장하는 프로그램을 짜야 했었는데 제곱의 시간을 써버렸다. 그래서 안 좋다.

---

**다른 답안**

```python
n = int(input())

array = []
for i in range(n):
  input_data = input().split()
  array.append((input_data[0], int(input_data[1])))

array = sorted(array, key=lambda student : student[1])

for student in array:
  print(student[0], end=' ')
>
2
홍길동 95
이순신 77
이순신 홍길동 
```

1. 학생의 수를 받아온다.
2. 리스트를 하나만 만든다
3. 학생의 수만큼 루프를 돌리는데 이름과 점수를 같이 저장한다.
   1. (''홍길동'', 95) 이러한 식으로 리스트에 튜플로 저장한다.
4. 키를 점수로 하고 정렬한다.
5. 순서대로 이름을 출력하면 된다.
6. 이중 루프 구문이 없고 깔끔하다.

### 두 배열의 원소 교체

**내가 작성한 답안**

```python
n, k = map(int,input().split())
a_list = sorted(list(map(int, input().split())))
b_list = sorted(list(map(int, input().split())),reverse=True)

for i in range(k):
    a_list[i] , b_list[i] = b_list[i], a_list[i]

result = 0
for i in a_list:
    result += i
    
print(result)
>
5 3
1 2 5 4 3
5 5 6 6 5
26
```

1. n과 k를 받아온다.
2. a와 b 리스트를 받아서 바로 정렬한다.
   1. b는 내림차순으로 정렬한다.
3. k만큼 루프를 돌려서 인덱스에 해당하는 값을 바꾼다.
4. 합을 구해서 출력한다.

---

**다른 답안**

```python
# 다른 답안
n, k = map(int,input().split())
a = list(map(int, input().split()))
b = list(map(int, input().split()))

a.sort()
b.sort(reverse=True)

for i in range(k):
    if a[i] < b[i]:
        a[i], b[i] = b[i], a[i]
    else:
        break
print(sum(a))
```

1. n과 k를 받아온다.
2. a와 b리스트를 만든다.
3. a와 b리스트를 정렬한다.
   1. b는 내림차순으로 정렬한다.

4. k만큼 돌리는데 a의 값이 b보다 작아야 바꾸고 그렇지 않으면 루프를 탈출한다.
5. sum으로 합을 구한다.