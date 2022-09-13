# 06 그래프의 기본과 탐색  

---
### 01 그래프 기본  

- 그래프  
    - 객체(사물 또는 추상적 개념)들과 객체들 사이의 연결 관계 표현  
    - 정점(Vertex)들의 집합과 정점을 연결하는 간선(Edge)들의 집합으로 구성된 자료 구조  
    : G = (V,E), V: 정점들의 집합, E: 간선들의 집합  
      |V|:정점 개수, |E|: 간선 개수  
      
    - 선형이나 트리 자료구조로 표현하기 어려운 N:N 관계를 가지는 원소들을 표현하기에 용이  
    
- 그래프 종류  
    - 무향 그래프(Undirected Graph)  
    : 서로 대칭적인 관계를 연결해서 나타낸 그래프  
      
    - 유향 그래프(Directed Graph)  
    : 간선을 화살표로 표현하고 방향성의 개념 포함  
      
    - 가중치 그래프(Weighted Graph)  
    : 간선(이동할때)에 가중치를 부여한 그래프  
  
    
- 추가 정의
    - 인접  
    : 두 개의 정점에 간선이 존재  
      
    - 부분 그래프  
    : 운래 그래프에서 일부의 정점이나 간선을 제외한 그래프  
  
    - 경로  
    : 간선들을 순서대로 나열한 것   
      
    - 단순경로  
    : 경로 중 한 정점을 최대한 한 번만 지나는 경로  
      
    - 사이클(Cycle)  
    : 시작한 정점에서 끝나는 경로  
      - 사이클 없는 유향 그래프 : Directed Acyclic Graph  
    
##### 컴퓨터에서의 그래프 표현  

- 인접 행렬(Adjacent matrix)  
: |V|X|V| 크기의 2차원 리스트를 이용해서 간선 정보 저장  
  두 정점을 연결하는 간선의 유무 표현  
  인접 : 1, 인접하지 않다 : 0
  
  - 간선의 갯수  
    무향 그래프는 (i,i) 대각 원소기준 상 혹은 하  
    유향 그래프는 임의의 행,렬의 합

- 인전 리스트(Adjacent List)  
: 각 정점마다 인접 정점으로 나가는 간선의 정보 저장  
  
---  
### 02 그래프 탐색  

- 그래프 순회  
: 비선형구조인 그래프로 표현된 모든 자료(정점)를 빠짐없이 탐색  
  - dfs(depth first search)  
    > 시작 정점에서 갈 수 있는 한 방향 선택해서 이동  
    > 이 과정 반복  
    > 갈 곳이 없으면, 최근 갈림길까지 돌아와서 다른 방향 이동  
    
    Stack(후입선출) 사용  
    
    ```python
    # 재귀  
    
    # G: 그래프, v: 시작 정점  
    # visited: 정점의 방문 정보, False로 초기화  
    # G[v]: 그래프 G에서 v의 인접 정점 리스트  
    
    def DFS_Recursive(G,v):
        visited[v] = True
        visit(v)
        for w in G[v]:
            if not visited[w]:
            DFS_Recursive(G,w)
    ```
    ```python
    # 알고리즘  
    # S: 스택  
    # 다른 변수는 위와 동일
    
    def DFS_Iterative(S,v):  
        S = [v] 
        while stack:  
            v = S.pop() 
            if v not in visited:
                visited.append(v)
                visit()
                S.extend(G[v] - set(visited))
        return visited
    ```

  - bfs(breadth first search)  
    > 탐색 시작점의 인접한 정점들을 먼저 모두 방문  
    > 방문했던 정점들을 다시 시작점으로 하여 반복  
    
    Queue(선입선출) 사용  
    
    ```python
    # 알고리즘  
    # Q: 스택  
    # 다른 변수는 위와 동일
    
    def BFS(Q,v):  
        Q.append(v) 
        visited[v] = True
        visit(v)
        while Q:  
            v = Q.pop(0)
            for w in G[v]: 
                if not in visited[w]:
                    Q.append(w)
                    visited[w] = True   
                    visit(w)
    ```   
    
---  
### 03 상호배타 집합들  

- 서로소(상호배타 집합들)  
  - 서로 중복 포함된 원소가 없는 집합들, 교집합 X  
  - 집합에 속한 하나의 특정 원소를 통해 각 집합들을 구분  
    - 특정 원소 : 대표자(Representative)  
  - 상호배타 집합을 표현할때 연결 리스트, 트리 이용  
  - 집합 연산  
    - Make-Set(x)  
      : x만 존재하는 집합 생성  
    - Find-Set(x)  
      : x가 존재하는 집합을 찾는다  
    - Union(x,y)   
      : x가 속한, y가 속한 집합을 합친다.  
      
    효율적으로 표기하기 위해, 트리를 이용  
    대표자를 루트 노드로 놓는다.  
    원소, rank를 같이 저장  
    
    










