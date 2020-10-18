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