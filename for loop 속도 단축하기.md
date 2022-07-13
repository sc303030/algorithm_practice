# for loop 속도 단축하기

- for loop 안에서 연산을 수행할 때 과연 어떤 방법으로 해야 시간을 단축할 수 있을까?
- 여러 가지 방법을 시도해 보았다. 
- 시간 날 때 하나씩 하나씩 채워가려고 한다.
- 우선 그 연산이 for loop내에서 무조건 실행되어야 하는지 혹은 for loop 후에 실행해도 되는지에 따라 다르다.

#### 조건문을 만족하는 경우가 적을 경우

- 접했던 상황은 다음과 같다.
  - 비교할 값은 정해져 있었다.
    - 그러나 이 값보다 큰 경우가 거의 없다.
  - 데이터의 `i-1` 값과 `i` 값의 차가 비교할 값보다 크면 조건이 충족된다.

- 대소 비교를 하는데 조건에 만족하는 경우가 적을 때 for loop안에서 연산을 수행하는 것이 좋을지, for loop 밖에서 연산을 수행하는 것이 좋을지 비교를 해보았다.
- 아래의 경우에는 거의 for loop의 마지막에 가서 조건이 충족되기에 for loop를 다 돌고 밖에서 비교하는 것이 더 유리하다.

> for loop 내에서 대소 비교

```python
import time


def compare_max_number(target_number, max_range):
    start = time.process_time()
    max_number = 0
    for i in range(1, max_range):
        temp = i - (i-1)
        if target_number <= max_number:
            end = time.process_time()
            print(end - start)
            return True
        max_number = max(max_number, temp)
    return False

compare_max_number(1000002, 1000001)
>
0.234375
```

> for loop 밖에서 대소 비교

```python
import time


def compare_max_number(target_number, max_range):
    start = time.process_time()
    max_number = 0
    for i in range(1, max_range):
        temp = i - (i-1)
        max_number = max(max_number, temp)
    if target_number <= max_number:
        end = time.process_time()
        print(end - start)
        return True
    return False

compare_max_number(1000000, 1000001)
>
0.171875
```



- 제너레이터와 numba 등은 추후에 다시 정리하려고 한다.