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

### 떡볶이 떡 만들기

**내가 작성한 답안**

```python
n,m = map(int,input().split())
dd_list = list(map(int,input().split()))

dd_list.sort(reverse=True)
result= []
a = 1
while True :
    for i in dd_list:
        b = i - dd_list[-a]
        if b < 0:
            result.append(0)
        else:
            result.append(b)
    if sum(result) == m:
        break;
    a += 1
    result = []
print(dd_list[a])
>
4 6
19 15 10 17
15
```

1. 떡의 개수와 길이를 받는다.
2. 떡의 개별 높이를 받아서 내림차순으로 정렬한다.

3. 높은 떡의 길이부터 낮은 떡의 길이를 뺀다.
   1. 이 길이가 -면 0을 +면 그 값을 result에 담는다.
   2. 이 값이 m이랑 일치하면 while를 빠져나간다.

4. 떡의 길이 리스트에 a를 넣어서 최댓값을 구한다.
5. 이건 하나 하나 구하지 않아서 안 될 것 같다.

---

**다른 답안**

```python
n,m = map(int,input().split())
array = list(map(int,input().split()))

start = 0
end = max(array)

result = 0
while(start <= end):
    total = 0
    mid = (start + end) // 2
    for x in array:
        if x > mid:
            total += x - mid
    if total < m:
        end = mid - 1
    else:
        result = mid
        start = mid + 1
print(result)
>
4 6
19 15 10 17
15
```

1. 떡의 개수와 길이를 받는다.
2. 떡의 개별 높이를 받는다.
3. start와 end를 지정한다.
   1. end는 개별 떡의 최댓값으로 설정한다.
4. 시작지점이 끝 지점보다 커질때까지 계속 반복한다.
   1. 중간지점과 x를 비교해서 x가 크면 떡을 자르고, 이 값을 total에 저장한다.
   2. 만약에 total이 m보다 작으면 끝점을 감소시킨다.
   3. 중간점을 계속 옮기면서 남은 떡의 길이를 계산한다.
   4. 결과가 중간점과 일치하면 result를 담고, start가 end보다 커질 것이다. 그러면 빠져나온다
5. 최종 결과를 출력한다.

