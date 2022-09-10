# 02 완전 검색  

---
### 01 완전 검색 기법  

- Baby-Gin Game  
> :0~9사이의 숫자 카드에서 6장 뽑는다.  
> 런(RUN) : 3장의 카드가 연속적인 번호를 갖는 경우  
> 트리플릿(Triplete) : 3장의 카드가 동일한 번호는 갖는 경우  
> &Rightarrow; 6장의 카드가 런과 트리플릿으로만 이루어져있는 경우 Baby-Gin  

- 완전 검색  
> - 문제의 해(Solution)를 얻기 위해 가능한 모든 경우들을 나열해 보고 확인하는 기법  
> 고지식한 방법(Brute-force), 생성 및 테스트(Generate and test)  
> Brute-force의 force : 사람(지능)보다는 컴퓨터의 힘(계산능력)을 의미한다.  
> 
> - 문제를 해결하기 위한 간단하고 쉬운 접근법(상대적으로 빠른 시간에 문제 해결 가능)  
> - 요소, 인스턴스의 크기가 작을 경우 유용  

- 고지식한 검색(순차 검색, Sequential Search)  
: 자료들의 리스트에서 키 값을 찾기 위해 첫 번째 자료부터 비교하면서 진행  
  결과 &rightarrow; 탐색 성공 or 실패  
  
```python
def sequentialSearch(a,n,key):
    i = 0
    while i < n and a[i] != key:
        i = i + 1
    if i < n:   # 성공
        return i
    else:       # 실패
        return -1
```

  
> - 정리  
> 완전 검색이란?  
> 문재 해결을 위한 가장 단순한 방법이지만, 크기가 커지면 시간 복잡도가 매우 크게 증가한다.  
> 입력 크기를 작게 해서 빠르게 답을 구하는 알고리즘 설계  
> 완전 검색으로 접근 &rightarrow; 해답 도출 후 다른 알고리즘도 사용 &rightarrow; 해답 확인  

- ex) Baby-Gin  
`{2, 3, 5, 7, 7, 7}`을 입력 받았을 시, Power set 생성 후, 앞의 세 자리, 뒤의 세 자리를 잘라서 Run, Triplete 여부 테스트  
  &Rightarrow; Baby-Gin 판단

---  
### 02 조합적 문제  

많은 종류의 문제들이 특정 조건을 만족하는 경우나 요소를 찾는 검색  
Permutation, Combination, Subset과 같은 Combinatorial Problems과 관련되어 있다.  
조합적 문제에 대한 고지식한 방법(Brute-force)  

- 순열  
: 서로 다른 것들 중 몇 개를 뽑아서 한 줄로 나열하는 것  
    `nPr` : 서로 다른 n개중 r개를 택하는 순열 표현  
  순서가 있는 나열과 같은 느낌이다.  
  

- 순열 생성 방법  
> 1. 사전식 순서(Lexicographic-Order)  
> 요소들이 오름차순으로 나열된 형태가 시작하는 하나의 순열  
> `{1,2,3}`  
> &rightarrow; `[1,2,3], [1,3,2], [2,1,3], [3,2,1], [3,1,2], [3,2,1]`  
> 
> 2. 최소 변경을 통한 방법(Minimum-exchange requirement)  
> 각각의 순열들은 이전의 상태에서 단지 두 개의 요소들 교환을 통해 생성  
> &rightarrow; Johnson-Trotter 알고리즘  

-  두 원소의 교환을 통해 생성  
: 순열이 생성되는 모든 과정은 트리 구조를 가진다.  
   
```python
# a[] : 데이터가 저장된 리스트  
# n : 원소의 개수
# k : 현재까지 선택된 원소의 수  
def perm(n,k):
    if k == n: # 하나의 순열이 생성됨.
        print(a) # 원하는 작업 수행
    else:
        for i in range(k,n): 
            a[k], a[i] = a[i], a[k] # 교환을 통한 선택 
            perm(n,k+1) # 재귀호출
            a[k], a[i] = a[i], a[k] # 이전 상태로 복귀
```
- 파이썬 라이브러리로 만든 순열  
```python
import itertools  
lst = [1,2,3]
result = itertools.permutations(lst) # (lst,3) r 생략시 기본값 len(lst)

print(list(result))
```

- 파이썬 라이브러리로 만든 중복 순열  
```python
import itertools  
lst = [1,2,3]
result = itertools.product(lst, repeat=3) 

print(list(result))
```

---
- 부분 집합(Subset)  
: 집합에 포함된 원소들을 선택하는 것  
  다수의 중요 알고리즘들이 원소들의 그룹에서 최적의 부분 집합을 찾는 것  
  N개의 원소를 포함한 집합 &Rightarrow; $2^n$개
  
```python
# Power set 단순하게 생성하는 방법  
arr = [2,3,4,5]
bit = [0]*len(arr)
for i in range(2):
    bit[0] = i
    for j in range(2):
      bit[1] = j
        for k in range(2):
            bit[2] = k
            for l in range(2):
                bit[3] = l
                print(arr[x] for x in range(len(bit)) if bit[x]) # 생성된 부분집합 출력
```

- 바이너리 카운팅(Binary Counting)  
: 원소 수에 해당하는 N개의 비트 열을 이용  
  i번째 비트 값이 1이면 i번째 원소가 포함되었음.  
  
```python
# Binary Counting
arr = [2,3,4,5]
n = len(arr) # n: 원소의 개수  

for i in range(1<<n): # 1 << n : 부분집합의 개수 
    for j in range(n): # 원소의 수만큼 비트를 비교함
        if i & (1<<j): # i의 j번째 비트가 1이면 j번째 원소 출
            print(arr[j],end=",")
    print()
```
```python
arr = [2,3,4,5]
for i in range(1<<len(arr)): # 1<<n : 부분집합의 개수
    print([arr[j] for j in range(len(arr)) if i & (1<<j)])
```
---
- 조합(Combination)  
: 서로 다른 n개의 원소 중 r개를 순서 없이 골라낸 것  
  
`nCr = n-1Cr-1 + n-1Cr`  
&rightarrow; `nCr`은 n개중에 r개를 선택하는데, `n-1Cr-1 + n-1Cr`는 한 개의 원소가 포함된 상태에서 r-1개를 뽑는 것 + 포함 되지 않은 상태에서 r개를 뽑는 것의 합과 같다.  

```python
# 조합 
def comb(n,r):
    if r == 0:
        print(tr)
    elif n < r:
        return
    else:
        tr[r-1] = an[n-1]
        comb(n-1, r-1)
        comb(n-1, r)
```
```python
# 파이썬 라이브러리를 활용한 조합
import itertools
lst = [1,2,3]
result = itertools.combinations(lst, r=2) # r 생략 불가
print(list(result))
```
```python
# 파이썬 라이브러리를 활용한 중복조합
import itertools
lst = [1,2,3]
result = itertools.combinations_with_replacement(lst, r=2) # r 생략 불가
print(list(result))
```


