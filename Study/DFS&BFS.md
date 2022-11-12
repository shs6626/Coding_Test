# DFS/BFS

### 그래프 탐색하기 위한 대표적인 두 가지 알고리즘

탐색 (Search) 란 많은 양의 데이터 중에서 원하는 데이터를 찾는 과정을 의미한다

DFS와 BFS를 정확히 알기 위해선 기본 자료구조인 **스택과 큐**에 대한 이해가 필요하다.

(자료구조 : 데이터를 표현하고 관리하고 처리하기 위한 구조)

오버플로 : 특정한 자료구조가 수용할 수 있는 데이터의 크기를 이미 가득 찬 상태에서 삽입 연산을 수행할 때 발생한다.

언드플로 : 특정한 자료구조에 데이터가 전혀 들어 있지 않은 상태에서 삭제 연산을 수행하면 데이터가 전혀 없는 상태

### 스택 (Stack)

박스(택) 쌓기라고 생각하면 쉽다

**FILO**

### 큐 (Queue)

대기 줄

**FIFO**

```python
from collections import deque

queue = deque()

queue.append(5)
queue.append(2)
queue.popleft()
queue.popleft()
```

deque는 스택과 큐의 장점을 모두 채택한 것인데 데이터를 넣고 빼는 속도가 리스트 자료형에 비해 효율적이며 queue 라이브러리를 이용하는 것보다 더 간단하다.

### 재귀함수 (Recursive Function)

자기 자신을 다시 호출하는 함수

컴퓨터 내부에서 재귀 함수의 수행은 스택 자료구조를 이용한다. 즉, 스택 자료구조를 활용해야 하는 상당수 알고리즘은 재귀함수를 이용해서 간편하게 구현될 수 있다. (ex. DFS)

---

## DFS

**Depth-First-Search 깊이 우선 탐색**

그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘

그래프는 node(vertex)와 edge로 표현된다. 

프로그래밍에서 그래프는 크게 2가지로 표현된다.

1. 인접 행렬 (Adjacency Matrix) : 2차원 배열로 그래프의 연결 관계를 표현하는 방식
    1. 메모리 불필요하게 낭비
2. 인접 리스트 (Adjacency List) : 리스트로 그래프의 연결 관계를 표현하는 방식
    1. 메모리 효율적
    2. 정보를 얻는 속도가 느리

```python
#인접 행렬

INF = 9999999

graph = [
    [0,7,5],
    [7,0,INF],
    [5,INF,0]
]

```

```python
#인접 리스트

graph = [[] for _ in range(3)]

print(graph)

graph[0].append((1,7))
graph[0].append((2,5))

print(graph)

graph[1].append((0,7))
graph[2].append((0,5))

print(graph)

# [[], [], []]
# [[(1, 7), (2, 5)], [], []]
# [[(1, 7), (2, 5)], [(0, 7)], [(0, 5)]]
```

DFS 스택 자료 구조

1. 탐색 시작 노드를 스택에 삽입하고 방문 처리를 한다
2. 스택의 최상단 노드에 방문하지 않은 인접 노드가 있으면 그 인접 노드를 스택에 넣고 방문처리를 한다. 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼낸다
3. 2번의 과정을 더 이상 수행할 수 없을 때 까지 반복한다

![Untitled](DFS%20BFS%20aac80c228ccf4037aa6f324d303411dc/Untitled.png)

```python
#DFS 메서드 정의

def dfs(graph, v, visited):
    visited[v] = True
    print(v, end = ' ')

    for i in graph[v]:
        if not visited[i]:
            dfs(graph, i, visited)

    # graph = [
    #     []
    #     [2,3,8],
    #     [1,7],
    #     .....
    # ]
    
    visited = [False]*9
    
    dfs(graph, 1, visited)

```

## BFS

Breadth First Search ‘너비 우선 탐색’ 

가까운 노드부터 탐색하는 알고리즘

큐 자료구조에 기초한다는 점에서 구현이 간단하며, 일반적인 경우 실제 시간은 DFS보다 좋은 편이다.

1. 탐색 시작 노드를 큐에 삽입하고 방문 처리를 한다
2. 큐에서 노드를 꺼내 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리를 한다
3. 2번의 과정을 더 이상 수행할 수 없을 때까지 반복한다

```python
form collections import deque

def bfs(graph, start, visited):
    queue = deque([start])

    visited[start]=True

    whiile queue:
    v=queue.popleft()
    print(v,end=' ')

    for i in graph[v]:
        if not visited[i]:
            queue.append(i)
            visited[i] = True

   
graph = [
    [],
    [2,3,8],
    [1,7],
    ....
]

visited = [False]*9

bfs(graph, 1, visited)
```

![Untitled](DFS%20BFS%20aac80c228ccf4037aa6f324d303411dc/Untitled%201.png)