# Queue  

### 큐(Queue)  
: 스택과 마찬가지로 삽입과 삭제의 위치가 제한적인 자료구조로써, 선입선출형식의 자료구조.

- 선입선출 (First In First Out)  
: 큐에 삽입한 순서대로 원소가 저장되어, 가장 먼저 삽입된 원소가 가장 먼저 삭제된다.  
    
---
### 스택의 연산    

&nbsp; enQueue(item) : 큐의 뒤쪽(rear 다음)에 원소를 삽입하는 연산  
&nbsp; deQueue() : 큐의 앞쪽(front)에서 원소를 삭제하고 반환하는 연산  
&nbsp; createQueue() : 공백 상태의 큐를 생성하는 연산  
&nbsp; isEmpty() : 큐가 공백상태인지를 확인하는 연산  
&nbsp; isFull() : 큐가 포화상태인지를 확인하는 연산  
&nbsp; Qpeek() : 큐의 앞쪽(front)에서 원소를 삭제없이 반환하는 연산 

---
### 큐(Queue)의 종류  
: 선형큐, 원형큐, 우선순위 큐  

---
### 선형큐  
: 1차원 배열을 이용한 큐

- 상태  
1) 초기 상태  
: front == rear == -1
2) 공백 상태  
: front == rear
3) 포화 상태  
: rear == n-1 (n: 배열의 크기, n-1: 배열의 마지막 인덱스)  
   
##### 문제점

- 잘못된 포화상태 인식  
: 선형 큐를 이용하여 원소의 삽입과 삭제를 계속할 경우, 배열의 앞부분에 활용할 수 있는 공간이 있음에도 불구하고, rear=n-1인 상태  
  포화상태로 인식하여 더 이상의 삽입의 수행하지 않게 됨  
  - 해결 방안  
    1) 연산시 배열의 앞부분으로 이동 -> 원소 이동에 많은 시간이 소요되어 효율성 떨어짐  
    2) 1차원 배열이되, 처음과 끝이 연결되어 원형 형태의 큐를 이룬다고 가정하고 사용 -> 원형 큐의 논리적 구조.

---    
### 원형큐  

- 초기 공백 상태  
: front = rear = 0  
  

- Index의 순환  
: front, rear의 위치가 n-1 이후, 처음 인덱스인 0으로 이동해야 한다. -> mod 사용  
  

- 연산
    - isEmpty 와 isFull 의 구별  
    : 선형큐에서 front=rear일때, 포화상태이다.  
      원형큐에서 front=rear일때 공백상태이므로, 이를 구별하기 위해 원형큐의 실질적인 저장공간은 `n-1`개 이다.  
      즉, `index(rear+1) == index(front)`인 경우, 포화상태이다.  
      isFull() => (rear+1) % n == front  
  
    - 삽입(enQueue(item))  
    : rear = (rear + 1) % n  
      
    - 삭제(deQueue(), delete())  
    : isEmpty 일때 예외처리하고, front = (front + 1) % n 에 원소 대입  
      
---  
### 큐의 활용 : 버퍼(Buffer)  
: 데이터를 한 곳에서 다른 한 곳으로 전송하는 동안 일시적으로 그 데이터를 보관하는 메모리의 영역  
- 버퍼링  
: 버퍼를 활용하는 방식 또는 버퍼를 채우는 동작  
  

---  
### BFS(Breadth First Search)  
- 너비 우선 탐색  
: 탐색 시작점의 인접한 정점들을 먼저 모두 차례로 방문한 후에, 방문했던 정점을 시작점으로 하여 다시 인접한 정점들을 차례로 방문하는 방식  
  기존의 dfs는 한 점에서 갈 수 있는 경로를 쭉 갔다가 되돌아오는(pop) 방식  
  bfs는 갈 수 있는 점들중 가장 먼저 오는 점을 빼고(pop(0)), 갈 수 있는 경로를 뒤로 넣어주는 방식  
  ※ 전 경로를 들려야 함 -> DFS, 어느 구간을 가기 위한 횟수 -> BFS  
```python
# BFS 구현

def BFS(G,v): # 그래프 G, 탐색 시작점 v
    visited = [0]*(n+1) # 정점의 개수 n
    queue = []
    queue.append(v)
    while queue:
        t = queue.pop(0)
        if not visited[t]:
            visited[t] = True
            visit(t)
            for i in G[t]:
                if not visited[i]:
                queue.append(i)
```

```python
# BFS 구현2

def BFS(G,v,n): # 그래프 G, 탐색 시작점 v
    visited = [0]*(n+1) # 정점의 개수 n
    queue = []
    queue.append(v)
    visited[v] = 1
    while queue:
        t = queue.pop(0)
        visit(t)
        for i in G[t]:
            if not visited[i]:
            queue.append(i)
            visited[i] = visited[t] + 1
```












