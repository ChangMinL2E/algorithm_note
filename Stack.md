# STACK(스택)

### 스택(stack)
: 물건을 쌓아 올리듯 자료를 쌓아 올린 형태의 자료구조

- 스택에 저장된 자료는 선형 구조를 가진다.  
- 스택에 자료를 삽입하거나 스택에서 자료를 꺼낼 수 있다.  
- 후입선출(Last-In-First-Out) 구조  

top : 스택에서 마지막 삽입된 원소의 위치  

### 스택의 연산    
  
&nbsp; push(삽입) : 저장소에 자료 저장  
&nbsp; pop(삭제) : 저장소에서 자료를 꺼낸다.   
&nbsp; isEmpty : 스택이 공백인지 아닌지 확인하는 연산.  
&nbsp; peek : top에 있는 item(원소)를 반환하는 연산.
---
### 재귀호출      
: 자기 자신을 호출하여 순환 수행되는 것  
``ex) factorial, Fibonacci``  
---
### Memoization  
: 컴퓨터 프로그램을 실행할 때 이전에 계산한 값을 메모리에 저장해서 매번 다시 계산하지 않도록 하여 전체적인 실행속도를 빠르게 하는 기술이다.  
동적 계획법(DP)의 핵심이 되는 기술!

factorial 과 fibonacci와 같은 재귀함수에서 계산된 값을 저장하는 방식으로 사용된다.  
=> 이는 계산 되었던 값들이 다시 계산 되서 나오는 수행을 막아준다.  

```python
# Fibonacci 구현 예시

def fibo():
    global memo
    if n >= 2 and len(memo) <= n:
        memo.append(fibo(n-1) + fibo(n-2))
    return memo[n]

memo = []
```
---

### DP(Dynamic Programming)
: 그리디 알고리즘과 같이 최적화 문제를 해결하는 알고리즘이다.  
입력 크기가 작은 부분 문제들을 모두 해결, 그 해들을 이용하여 더 큰 문제 해결  
최종적으로 원래 주어진 입력의 문제를 해결하는 알고리즘이다.  

---
### DFS(깊이우선탐색)

- 비선형구조의 그래프 구조는 표현된 모든 자료를 빠짐없이 검색하는 것이 중요하다.

1. 깊이 우선 탐색(Depth First Search, DFS)
2. 너비 우선탐색(Breath First Search, BFS)

Stack에서는 DFS에 대해서 알아보자.

- DFS(Depth First Search, 깊이 우선 탐색) 

: 시작 정점의 한 방향 -> 갈 수 있는 곳 깊이 탐색  
-> 다시 갈림길로 돌아와 깊이 탐색. -> 모든 정점 방문하는 순회방법.  

- 구현 방법

스택의 현재 위치를 넣을 리스트 : stack = [ ]  
스택이 방문했던 여부를 넣을 리스트 : visited = [ ]

```python
# dfs 구현 함수.
def dfs(v):
    s = [] # stack -> s
    s.append(v)
    visited[v] = True
    while:
        v = s.pop(-1)
        # print(v, end= "")
        for w in G[v]:
            if not visited[w]:
                s.append(w)
                visited[w] = True
```

```python
# dfs 구현 재귀 함수.
def dfsr(v):
  visited[v] = True
  # print(v, end=' ')
  for w in G[v]:
    if not visited[w]:
        dfsr(w)

```

```python
# bfs 구현 함수.
def bfs(v):
    q = []
    q.append(v)
    visited[v] = True
    while q:
        v = q.pop(0) # 선입선출과 선입후출 차이이다.
        print(v, end='')
        for w in G[v]:
            if not visited[w]:
                q.append(w)
                visited[w] = True
```