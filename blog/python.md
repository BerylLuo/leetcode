# python 刷题常用tools

- {}, [], set()

- list的sort和sorted，里面的key参数可以指定比较的方法

- heapq 模块里面的heappush, heappop, heappushpop，比如

```
q = []
heappush(q, (2, 'second'))
heappush(q, (1, 'first'))
heappush(q, (3, 'third'))
while len(q):
    print(heappop(q)[1])
"""
first
second
third
"""
```

- collections.deque 使用append和pop来充当stack；使用append和popleft来充当队列

- collections.Counter 统计频率，主要keys, values, items, subtract, +, -, &和|方法

- bisect 模块里面的bisect和bisect_left用来做二分查找

- itertools.permutations 用来遍历一个iterable的全部permutation
 
- collections.defaultdict 可以设置默认值的字典，比如

    - defaultdict(list)
    - defaultdict(int)
    - defaultdict(str)
    - defaultdict(deque)
    - defaultdict(lambda: 3)