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
```

建立相邻表,需要保持节点的索引以0开始
```
adj = defaultdict(list)
for u, v, w in arr:
    adj[u].append([v, w])
```