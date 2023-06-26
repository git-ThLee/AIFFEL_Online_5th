# 제너레이터(Generator)

제너레이터(Generator)는 파이썬의 이터레이터(Iterator)를 생성하는 함수입니다. 일반적인 함수와 달리, 제너레이터는 값을 반환한 후에도 실행 상태를 유지하고, 필요할 때마다 값을 생성하여 반환합니다. 이를 통해 큰 데이터 집합을 한 번에 메모리에 저장하지 않고, 필요한 만큼의 값을 생성하여 처리할 수 있습니다.

제너레이터 함수는 yield 문을 사용하여 값을 반환하고 실행 상태를 유지합니다. yield 문은 값을 반환하면서 현재 상태를 기억하고 다음 호출에서 실행을 재개합니다. 이러한 특성으로 인해 제너레이터는 이터레이터로 사용할 수 있습니다.

제너레이터 함수를 정의할 때는 일반 함수와 동일한 방법으로 정의합니다. 다만, 함수 내에서 yield 문을 사용하여 값을 반환하고, 필요에 따라 반복적으로 호출될 수 있는 함수로 만들어야 합니다.

```python
def my_generator():
    yield 1
    yield 2
    yield 3

# 제너레이터 호출 및 값 출력
gen = my_generator()
print(next(gen))  # 1
print(next(gen))  # 2
print(next(gen))  # 3

```

## for문과 비교해보기

```python
import sys

my_list = ['a','b','c','d']

# 인자로 받은 리스트를 가공해서 만든 데이터셋 리스트를 리턴하는 함수
def get_dataset_list(my_list):
    result_list = []
    for i in range(2):
        for j in my_list:
            result_list.append((i, j))
    print('>>  {} data loaded..'.format(len(result_list)))
    return result_list

for X, y in get_dataset_list(my_list):
    print(X, y)
print(f'메모리사용량 : {sys.getsizeof(get_dataset_list)}') # sys.getsizeof(메모리 사용량 확인하는 메소드)
```

- 위 코드에서의 문제점 

> 이중 for 문이 다 돌아가는 걸 기다린 후, 반환된 result_list 값에 대해 또 for 문을 돌려야 한다는 것입니다. 뭔가 중복되는 느낌도 들고, 확실히 느리겠죠? 지금은 my_list 에 데이터 4개밖에 없지만 만약 1억 개가 담겨 있다면 또 어떤 문제가 있을까요? 바로, get_dataset_list(my_list) 를 위해 엄청난 양의 데이터를 전부 메모리에 올려놔야 한다는 것입니다.

```python
my_list = ['a','b','c','d']

# 인자로 받은 리스트로부터 데이터를 하나씩 가져오는 제너레이터를 리턴하는 함수
def get_dataset_generator(my_list):
    for i in range(2):
        for j in my_list:
            yield (i, j)   # 이 줄이 이전의 append 코드를 대체했습니다
            print('>>  1 data loaded..')

dataset_generator = get_dataset_generator(my_list)
for X, y in dataset_generator:
    print(X, y)

print(f'메모리 사용량 : {sys.getsizeof(dataset_generator)}')
```

영어로 "Yield"라는 단어는 "양보하다"라는 뜻을 갖고 있죠. 파이썬에서도 마찬가지로 yield는 코드 실행의 순서를 밖으로 "양보"합니다. 즉, dataset_generator = get_dataset_generator(my_list) 을 실행해도 "generator object" 만 반환할 뿐, 저희가 원하는 값을 바로 반환하고 있지 않습니다. 실질적으로 데이터를 반환하는 건 for 문에서 값을 하나씩 불러올 때죠.

위 코드 블록의 실행 결과를 보면 값을 한 번 반환 후 "1 data loaded.." 를 출력하는 걸 반복합니다.

그렇기 때문에 yield는 메모리 사용을 효율적으로 만들 수 있습니다.

실제 메모리 사용량을 확인해보면 yield를 사용한 반복문이 사용하지 않은 반복문보다 메모리 사용량이 적은걸 확인할 수 있습니다.

이처럼 제너레이터가 없다면 우리는 길이 1억짜리 리스트를 리턴 받아 메모리에 전부 올려놓고 처리를 시작해야 합니다. 그러나 제너레이터를 활용할 때는 1억 개의 데이터를 전부 메모리에 올려놓을 필요가 없이 현재 처리해야 할 데이터를 1개씩 로드해서 사용할 수 있게 됩니다. 이것은 빅데이터를 처리해야 할 머신러닝 상황에서 매우 요긴합니다.