# Python 刷题模版

```
from itertools import permutations, count, chain
from collections import defaultdict, Counter, deque
from heapq import heappush, heappushpop, heappop
from bisect import bisect, bisect_left

INF = float('inf')

def dijkstra_array(adj, N, s):
    visited = [False] * N
    d = [INF] * N

    d[s] = 0

    u = s
    while True:
        visited[u] = True
        for v, w in adj[u]:
            d[v] = min(d[v], d[u] + w)

        m = INF
        for i, v in enumerate(d):
            if not visited[i] and v < m:
                m, u = v, i
        if m == INF:
            return d

def dijkstra(adj, N, s):
    d = [INF] * N
    q = []
    heappush(q, [0, s])
    while len(q):
        w, u = heappop(q)
        if d[u] > w:
            d[u] = w
            for v, w in adj[u]:
                heappush(q, [d[u] + w, v])
    return d

def bellman_ford(adj, N, s):
    d = [INF] * N
    d[s] = 0
    for _ in range(N - 1):
        for u in adj:
            for v, w in adj[u]:
                d[v] = min(d[v], d[u] + w)
    return d

def spfa(adj, N, s):
    d = [INF] * N
    d[s] = 0

    q = deque()
    q.append(s)

    while len(q):
        u = q.popleft()
        for v, w in adj[u]:
            if d[u] + w < d[v]:
                d[v] = d[u] + w
                q.append(v)
    return d

def floyd(adj, N, s):
    mat = [[INF] * N for _ in range(N)]
    for i in range(N):
        mat[i][i] = 0
    for u in adj:
        for v, w in adj[u]:
            mat[u][v] = w

    for k in range(N):
        for i in range(N):
            for j in range(N):
                mat[i][j] = min(mat[i][j], mat[i][k] + mat[k][j])

    return mat[s]
    
class STNode:
    def __init__(self, lo, hi, val=0, left=None, right=None):
        self.lo, self.hi, self.val = lo, hi, val
        self.left, self.right = left, right

class SegmentTree:
    def __init__(self, nums, lo, hi):
        self.validate(lo, hi)
        self.root = self.build(nums, lo, hi)

    def build(self, nums, lo, hi):
        if lo == hi:
            return STNode(lo, hi, nums[lo])
        else:
            mid = lo + (hi - lo) // 2
            left = self.build(nums, lo, mid)
            right = self.build(nums, mid+1, hi)
            return STNode(lo, hi, left.val + right.val, left, right)

    def add(self, val, lo, hi):
        self.validate(lo, hi)
        self._add(self.root, val, lo, hi)

    def query(self, lo, hi):
        self.validate(lo, hi)
        return self._query(self.root, lo, hi)

    def _add(self, root, val, lo, hi):
        if root.lo == root.hi:
            root.val += val
        else:
            mid = root.lo + (root.hi - root.lo) // 2
            if lo > mid:
                self._add(root.right, val, lo, hi)
            elif hi <= mid:
                self._add(root.left, val, lo, hi)
            else:
                self._add(root.left, val, lo, mid)
                self._add(root.right, val, mid+1, hi)
            root.val = root.left.val + root.right.val

    def _query(self, root, lo, hi):
        if root.lo == lo and root.hi == hi:
            return root.val
        else:
            mid = root.lo + (root.hi - root.lo) // 2
            if lo > mid:
                return self._query(root.right, lo, hi)
            elif hi <= mid:
                return self._query(root.left, lo, hi)
            else:
                return self._query(root.left, lo, mid) + self._query(root.right, mid+1, hi)

    def validate(self, lo, hi):
        if lo > hi:
            raise ValueError('lo > hi is not allowed!!!')
```

建立相邻表,需要保持节点的索引以0开始
```
adj = defaultdict(list)
for u, v, w in arr:
    adj[u].append([v, w])
```