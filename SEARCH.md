# 탐색

### 부품 찾기

**내가 작성한 답안**

```python
ori_n = int(input())
ori_m = list(map(int,input().split()))

costomer_n = int(input())
costomer_m = list(map(int,input().split()))

while costomer_n > 0:
    for i in costomer_m:
        if i in ori_m:
            print('yes', end=' ')
        else:
            print('no',end=' ')
        costomer_n -=1
>
5
8 3 7 9 2
3
5 7 9
no yes yes 
```

1. 가게 부품의 개수와 고유한 번호를 받아온다.
2. 소비자 부품 개수와 고유한 번호를 받는다.
3. while을 돌려 소비자가 입력한 고유한 번호를 가게의 기존 부품 번호와 비교한다.
4. 있으면 yes, 없으면 no를 출력한다.

---

**다른 답안01 **

```python
def binary_search(array, target, start, end):
    while start <= end:
        mid = (start + end) // 2
        if array[mid] == target:
            return mid
        elif array[mid] > target:
            end = mid - 1
        else:
            start = mid + 1
        return None
n = int(input())
array = list(map(int,input().split()))
array.sort()

m = int(input())
x = list(map(int,input().split()))

for i in x:
    result = binary_search(array,i,0,n-1)
    if result != None:
        print('yes',end=' ')
    else:
        print('no',end=' ')
>
5
8 3 7 9 2
3
5 7 9
no yes no 
```

1. 가게의 부품 고유 번호를 오름차순으로 정리한다.
2. 소비자가 입력한 번호와 비교해본다.
   1. 가게 부품 고유 번호 가운데와 비교해서 소비자가 입력한 번호가 똑같으면 가운데 번호를
   2. 가게 부품 고유 번호가 크면 왼쪽을, 아니면 오르쪽을 다시 비교한다.
   3. 없으면 None를 리턴한다.
3. 소비가자 입력한 부품 번호 개수만큼 루프를 돌려서 계산한다.
4. 여기서 왜 마지막이 no인지 다시 확인해볼 필요가 있다.

**다른 답안 02**

```python
n = int(input())
array = [0] * 1000001

for i in input().split():
    array[int(i)] = 1

m = int(input())
x =list(map(int,input().split()))

for i in x :
    if array[i] == 1:
        print('yes',end=' ')
    else:
        print('no', end=' ')
>
5
8 3 7 9 2
3
5 7 9
no yes yes 
```

1. 문제에서 주어준 범위까지 배열을 0으로 채운다.
2. 가게 부품 번호에 해당하는 인덱스를 1로 채운다.
3. 사용자가 입력한 부품 번호와 비교해서 그 부품 번호가 1이면 yes를 0이면 no을 리턴한다.

**다른 답안 03**

```python
n = int(input())
array = set(map(int,input().split()))

m = int(input())
x = list(map(int,input().split()))

for i in x :
    if i in array:
        print('yes', end=' ')
    else:
        print('no',end=' ')
>
5
8 3 7 9 2
3
5 7 9
no yes yes 
```

1. 가게 부품 번호를 받아서 중복없이 저장한다.
2. 소비자가 입력한 부품 번호를 받는다.
3. 하나씩 루프를 돌려서 가게 부품 번호와 확인한다.

