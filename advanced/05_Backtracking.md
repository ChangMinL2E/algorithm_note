# 05 백트래킹(Backtracking)  

---  
### 01 백트래킹  

- 백트래킹(Backtracking)  
>    - 해를 찾는 도중에 막히면 되돌아가서 다시 해를 찾아가는 기법  
>    - 최적화(Optimization) 문제와 결정(Decision) 문제를 해결 가능  
>    - 결정 문제: 해 존재 여부 &rightarrow; `yes` or `no`  
>  - ex) 미로 찾기  
>    - 입구 &rightarrow; 출구 경로 존재 여부  
>    - 조건 만족하는 부분 집합 존재 여부  
>    - 미로 찾기 최단 경로 문제  
> 
>  : 초기 상태에서 목표 상태로 가는 경로를 탐색하는 기법  
>    - 여러 가지 선택지중 하나 선택 &rightarrow; 새로운 선택지 집합 생성 &rightarrow; 반복 후 최종 상태  
  
- 트리의 루트 &rightarrow; 당첨(단말 노드) 가는 경로 찾기  
> dfs와 같은 방법 

- 상태 공간 트리  
> 해를 찾기 위한 선택의 과정을 트리로 표현한 것

- Backtracking 과 DFS의 차이  
    - Prunning (가지치기)
    : 불필요한 경로 조기에 차단  
      
- 예시 : 8-Queens  
> 퀸 8개를 8 X 8 크기의 체스판 안에 서로 공격할 수 없도록 배치하는 모든 경우를 구하는 문제  
> 루트의 높이가 0 일때, 노드의 높이는 말의 번호와 같다.  
> &rightarrow; 이와 같은 문제는 dfs로 하면 비효율  
>
> 상태 공간 트리로 볼때 방문하는 노드가 유망하지 않으면 탐색 중지  

---
### 02 부분 집합  

- 멱집합(Power set)  
: 어떤 집합의 공집합과 자기 자신을 포함한 모든 부분집합  
  원소 개수 n이면 부분집합의 개수 $2^n$

- Power set 생성 dfs 알고리즘
```python
# bit_lst: 집합에 대한 비트 표현 저장  
# k : 노드의 높이, n: 트리의 높이  

def subset(bit_lst, k, n):
    if k == n:
        process_solution(bit_lst, n) # bit를 list로 만들어주는 함수  
    else:
        bit_lst[k] = 0 # k번째 원소는 미 포함
        subset(bit_lst, k+1, n)
        bit_lst[k] = 1 # k번째 원소는 포함
        subset(bit_lst, k+1, n)
```

---  
### 03 순열(Permutation)  

- 모든 순열 생성 알고리즘  
```python
# order[] : 순열의 순서를 저장하는 리스트
def permutation(order,k,n):
    if k == n:
        print_order_array(order,n)
    else:
        check = [False]*n
        for i in range(k):
            check[order[i]] = True
            
        for i in range(n):
            if check[i] == False: # 체크되지 않은 원소 추가
                order[k] = i
                permutation(order,k+1,n)

```
---  

### 04 예시 1 : 동전 거스름돈 문제  

```python
# coin[] : 동전의 금액, choice: 선택한 동전들 집합  
# best : 거스름돈에 대한 최소 동전 개수
def CoinChange(choice, N, money):
    global best
    if best <= N: # 이미 넘어서버리면
        return
    elif money == 0:
        best = N
    else:
        for i in range(len(coin)):
            if money-coin[i] >= 0:
                choice[N] = coin[i]
                CoinChange(choice, N+1, money-coin[i])

```
