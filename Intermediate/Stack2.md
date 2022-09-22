# Stack2  

### 중위, 후위 표기법 (ex)계산기)  

- 중위 표기법(infix notation)  
: 연산자를 피연산자의 가운데 표기하는 방법  
  ex) A + B  
  

- 후위 표기법(postfix notation)  
: 연산자를 피연산자 뒤에 표기하는 방법  
  ex) AB+  
  
  
- 중위 표기법 -> 후위 표기법  
  1) 피연산자는 바로 출력
  2) 연산자인 경우, top 연산자의 우선순위가 자신보다 작을때까지 pop한 후에, push  
  3) ')'일 경우, '('가 top으로 올때까지 pop하고, '('와 만난경우 pop하지만, 출력하지 않고 넘어간다.  
  4) 토큰이 남아있지 않다면, stack에 남아있는 연산자 전부 pop하고, 출력한다.  
    

- 후위 표기법 -> 계산  
  1) 피연산자를 만나면 Stack에 push
  2) 연산자 □ 를 만나면 b = pop(), a = pop() -> push(a□b) 
  3) 수식이 끝나면, Stack pop하여 출력  
    

---  
### BackTracking  
: 해를 찾는 도중에 '막히면' (해가 아니면) 되돌아가서 다시 해를 찾아 가는 기법이다.  
이는 최적화(optimization) 문제와 결정(decision) 문제를 해결하는데 사용한다.  

#### 결정 문제  
: 문제의 조건을 만족하는 해가 존재하는지의 여부를 'yes' 또는 'no'로 답하는 문제.  

- 백트래킹(Backtracking)과 깊이우선탐색(depth first search)과의 차이  
: 가지치기(Prunning) - 해결책으로 이어질 것 같지 않으면 더 이상 그 경로를 따라가지 않음으로써 시도의 횟수를 줄임.  
  가지치기의 핵심은 depth를 줄이는 것.  
####ex)
```python
# 기본적인 멱집합 구하는 알고리즘

def par(k): # dfs
    if k == N:
        print(result)
        # return
    else:
        result[k] = 0
        par(k+1)

        result[k] = 1
        par(k+1)
        # for i in range(2):
        #     result[k] = i
        #     par(k+1)
        #



lst = [10, 30, 40]
result = [-1] * N
N = 3
par(0)
```
```python
# Stack2 p.56 연습문제 2번
def par(k):
    if k == N: # 다 돌았다. dfs
        # print(result)
        sumV = 0
        for i in range(N):
            if result[i] == 1:
                sumV += lst[i]
        if sumV == 10:
            for i in range(N):
                if result[i] == 1:
                    print(lst[i], end=' ')
            print()
    else:
        result[k] = 0
        par(k+1)

        result[k] = 1
        par(k+1)

lst = [x for x in range(1,11)]
N = 10
result = [-1]*N
par(0)
```
```python
# 백트래킹
def par(k, curSum):
    if curSum > 10:
        # print('이상',k, result) # k 는 depth를 의미.
        return

    if k == N: # 다 돌았다. dfs
        # sumV = 0
        # for i in range(N):
        #     if result[i] == 1:
        #         sumV += lst[i]
        if curSum == 10:
            for i in range(N):
                if result[i] == 1:
                    print(lst[i], end='')
            print()
    else:
        result[k] = 0
        par(k+1, curSum)

        result[k] = 1
        par(k+1, curSum+lst[k])


lst = [x for x in range(1,11)]
N = 10
result = [-1]*N
par(0, 0)
```
```python
# 순열
def per(k):
    if k == N:
        print(result)
        for i in range(N):
            print(lst[result[i]], end=' ')
        print()
        return

    for i in range(N):
        if not visited[i]:
            visited[i] = True
            result[k] = i
            per(k + 1)
            visited[i] = False  # 저장한 값이 다른 경우에 지장이 가면 안되므로, 복구

lst = [10, 20, 30]
N = 3
result = [-1] * N
visited = [False] * N
per(0)
```
```python
# 수업시간에 진행한 순열 알고리즘.

def f(i, N):
      if i == N:  # 순열 완성.
          print(P)
      else:
          for j in range(i, N):   # P[i]에 들어갈 숫자 P[j] 결정.
              P[i], P[j] = P[j], P[i]
              f(i+1, N)
              P[i], P[j] = P[j], P[i]

P = [1,2,3]
f(0, 3)
```
Swea 4881 : perputation + Backtracking
