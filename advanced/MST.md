# 최소 신장 트리  

- 그래프에서 최소 비용 문제  
    - 모든 정점을 연결하는 간선들의 가중치의 합이 최소가 되는 트리  
    - 두 정점 사이의 최소 비용의 경로 찾기  
    

- 신장 트리  
: n개의 정점, n-1개의 간선으로 이루어진 무방향 그래프  
  

- 최소 신장 트리 (Minimum Spanning Tree)  
: 무방향 가중치 그래프에서 신장 트리를 구성하는 간선들의 가중치의 합이 최소인 신장 트리  
    

---  
### Prim Algorithm  

- 하나의 정점에서 연결된 간선들 중에 하나씩 선택하면서 MST를 만들어 가는 방식  
    1. 임의 정점 선택  
    2. 선택 정점과 인접하는 정점들 중 최소 가중치 간선 정점 선택  
    3. 모든 정점이 선택될때 까지 반복  
    &Rightarrow; 어느 부분이 사이클이 되지 않도록 조심  

       
- 알고리즘 구현
```python
def prim():
    U = []
    D = [10000]*(N+1) # infinite 대신 10000을 적어줬다.
    P = [10000]*(N+1)
    D[0] = 0
    while len(U) < N+1:
        # D에서 최소를 구한다.(단, U에 포함되지 않은 것을 대상으로
        minV = 10000
        for i in range(N+1):
            if i in U: continue
            if minV > D[i]:
                minV = D[i]
                curV = i

        U.append(curV)
        # i와 연결된 정점들의 D를 수정
        for i in range(N+1):
            if i in U: continue
            if G[curV][i] and D[i] > G[curV][i]:
                D[i] = G[curV][i]
                P[i] = curV
    print(U,D,P)

N, E = map(int,input().split())
G = [[0]* (N+1) for _ in range(N+1)] # 인접행렬

for i in range(E):
    n1, n2, w = map(int,input().split())
    G[n1][n2] = w
    G[n2][n1] = w
# print(G)
prim()

```

#### 알고리즘 해석 및 idea  
: 노드를 하나씩 연결된 간선을 보되, 제일 가중치가 적은 간선을 key값으로 저장한다.

- U,D,P 생성  
> U: 확인한 노드들 집합 (진행한 순서)  
> D: 각 노드별 key 값 (가중치)  
> P: 각 노드별 부모 노드  
> D[0] = 0 : 초기 노드 선택을 위한 설정 (아래 코드 일반화를 위한 초기 작업)  

- 모든 노드들을 확인할때까지 진행 (While len(U)<N+1:)  
```python
While len(U)<N+1:
    minV = infinite # key 값이 제일 적은 노드를 보겠다.  
     for i in range(Node):  
       if not i in U:  # 봤던 노드들은 안보겠다.
           if minV > D[i]:  # 제일 적은 key를 가진 노드의 인덱스를 curV
               minV = D[i]
               curV = i
    U.append(curV) # 이제 가야지!
``` 
```python
for i in range(Node):
    if not i in U:  # 이미 봤던 간선들은 그만 보고 싶어요.
        if G[curV][i] and D[i] > G[curV][i]:  # 고른 노드와 인접하고, key값이 적으면 저장해줄껀데,
            D[i] = G[curV][i] # 그 노드의 key값을 바꿔주고,
            P[i] = curV # 부모노드를 저장해주세요.
```

&Rightarrow; 노드 선정을 다음과 같이 변경할 수 있다.  
```python
def prim(G):
    U = [False] * N # uppend를 빼고, 방문 여부의 visit를 만들어줬다.
    D = [1e10] * N
    D[0] =0
 
    for _ in range(N):
        # curV=U에 D중 가장 작은 값을 가진 정점 선택
        minV = 1e10
        for i in range(Node):
            if U[i]:
                continue
            if minV > D[i]:
                minV = D[i]
                curV = i
   
        U[curV] = True
        # curV하고 연결된 정점들의 D값을 최선으로 바꿔준다
        for i in range(N):
            if U[i]:
                continue
            if D[i] > G[curV][i]:
                D[i] = G[curV][i]
          
```

---  
### Dijkstra  





