# 4. 분할정복(Divided and Conquer)  

---  
### 01 분할 정복 기법  

- 예제 : 가짜 동전 찾기  
> n 개의 동전들 중에 가짜 동전이 하나 포함 되어 있다. (무게가 다름)  
> 양팔 저울을 최소로 사용해서 가짜 동전을 찾는 방법은 무엇일까..?  

- 분할 정복 알고리즘의 설계 전략  
    - 분할(Divide)  
    : 해결할 문제를 여러 개의 작은 부분 문제들로 분할  
      
    - 정복(Conquer)  
    : 나눈 작은 문제를 각각 해결  
      
    - 통합(Combine)  
    : 필요 시 해결된 해답을 모음  
  
    
- 반복(Iterative) 알고리즘 : O(n)  
: C의 거듭제곱 = 1에 거듭제곱 만큼 C를 곱하는 방법  
  ```python
    def Iterative_Power(C,n):
        result = 1
        for _ in range(n):
            result *= C
        return result
  ```

- 분할 정복 기반의 알고리즘 : O(logn)  
$C^n$  
  &Rightarrow; $C^{n/2}$*$C^{n/2}$ , n is even   
    &Rightarrow; $C^{{(n-1)}/2)$*$C^{{(n-1)}/2}$*C , n is odd  

```python
def Recursive_Power(C,n):
    if n == 1:
        return C
    if n%2 == 0: # even  
        y = Recursive_Power(C,n/2)
        return y*y  
    else: # odd  
        y = Recursive_Power(C,(n-1)/2)
        return y*y*C
```

반복 알고리즘 O(n) > 분할 정복 기반 알고리즘 O(logn)  
&Rightarrow; 시간 복잡도를 줄일 수 있다.  

---  
### 02 병합 정렬  
>: 여러 개의 정렬된 자료의 집합을 병합하여 한 개의 정렬된 집합으로 만드는 방식  
>분할 정복 알고리즘 활용  
>- Top-down 방식  
>: 자료를 최소 단위의 문제까지 나눈 후, 차례대로 정렬해서 최종 결과  
>
> 시간 복잡도 : O(nlogn)

- 병합 정렬 과정  
    - 분할 단계  
    : 자료의 개수가 하나(최소크기)인 부분 집합이 될 때까지 분할
    
    - 병합 단계  
    : 2개의 부분집합을 정렬하면서 하나의 집합으로 병합  
      
```python
# 알고리즘 : 분할  
def merge_sort(m):
    if len(m) <= 1: # 사이즈가 0이거나 1인 경우, 바로 리턴  
        return m  

    # 1. Divide
    mid = len(m)//2  
    left = m[:mid]
    right = m[mid:] 

    # 리스트의 크기가 1이 될 때까지 merge_sort 재귀 호출  
    left = merge_sort(left)
    right = merge_sort(right)  

    # 2. Conquer   
    return merge(left,right)
```
```python
# 알고리즘 : 병합  

def merge(left, right):
    result = [] # 두 개의 분할된 리스트를 병합하여 result를 만든다.  

    while len(left) > 0 and len(right) > 0: # l,r 에 원소가 남은 경우
        # left는 left끼리, right는 right끼리 정렬 되어 있는 상태
        # left와 right끼리 정렬하기.
        if left[0] <= right[0]:  
            result.append(left.pop(0))
        else:
            result.append(right.pop(0))
    if len(left) > 0:
        result.extend(left)
    if len(right) > 0:
        result.extend(right)
    return  result
```
---  
### 03 퀵 정렬  

- 퀵정렬  
: 주어진 리스트를 두 개로 분할하고, 각각을 정렬
    - 병합 정렬과 퀵 정렬의 차이점  
    : 두 부분으로 나누고 후처리로 병합 과정을 하는 병합 정렬  
      분할 시, 부분 정렬을 하며 분할하는 퀵 정렬  
      &Rightarrow;  퀵 정렬은 후처리 병합을 안해줘도 된다.  
      
```python
# Quick Sort
# A: list, l: start index, r: end index

def quickSort(A,l,r):
  if l < r:
    s = partition(A,l,r) # pivot index가 return 값으로 나온다.
    quickSort(A,l,s-1)
    quickSort(A,s+1,r)
```
- Hoare-Partition algorithm  
  - idea  
  : pivot &rightarrow; start  
    p | p>요소들 | p<요소들  
    처럼 정렬 후 pivot을 가운데에 둔다.  
    pivot은 다음 정렬에서 제외.

```python
def partition(A,l,r):
    p = A[l]
    i = l + 1
    j = r
    while i <= j:
      while(i<=j and A[i]<=p): i += 1
      while(i<=j and A[i]>=p): j -= 1
      if i <= j
        A[i],A[j] = A[j],A[i]
    A[l],A[j] = A[j],A[l] # 정렬 끝나면, 현재 j는 pivot보다 작은 집단 가장 오른쪽 원소  
    return j
```
pivot 선택 &rightarrow; 왼쪽 끝, 오른쪽 끝, 임의의 세 개 중 중간 값  

- Lomuto-Partition algorithm  
  - idea  
  : i,j 모두 증가 하면서 작업 수행  
    
```python
def partiton(A,l,r):
    x = A[r] # pivot은 제일 오른쪽 값이 된다.
    i = l-1 # i는 pivot보다 작은 마지막 값이 된다.
    for j in ragne(l,r):  
        if A[j] <= x: # A[j]가 pivot 보다 작으면
            i += 1
            A[i],A[j] = A[j],A[i]
    A[i+1],A[r] = A[r],A[i+1]
    return i+1 # 작은 마지막 인덱스 다음 자리에 pivot을 둔다.
```
---  
### 04 이진 검색    

- 이진 검색  
: 자료의 가운데에 있는 항목의 키 값과 비교하여 다음 검색 위치 결정, 진행하는 방법  
  정렬 되어 있는 상태여야 함.  
  - 검색 과정  
    1) 자료의 중앙에 있는 원소 선택  
    2) 중앙 원소의 값과 찾고자 하는 목표 값 비교  
    3) 목표 값과 중앙 원소 값 관계  
        - 목표 값 < 중앙 원소 값  
        : 왼쪽 반에서 새로 검색 수행  
        - 목표 값 > 중앙 원소 값  
        : 오른쪽 반에서 새로 검색 수행  
          
    4) 찾을 때까지 반복  
  
- 알고리즘 : 반복구조  
```python
# a : 검색할 리스트  
# key : 검색하고자 하는 값  

def binarySearch(a, key):
    st = 0
    ed = len(a)-1  
    while st <= ed:
        middle = st + (ed-st)//2 # 중간 위치  
        if key == a[middle]:
            return middle # 찾으면 index 반환
        elif key < a[middle]:
            ed = middle-1       
        else: # key > a[middle]
            st = middle-1
    return -1 # 검색 실패
```

- 알고리즘 : 재귀구조  
```python
# a : 검색할 리스트  
# key : 검색하고자 하는 값  

def binarySearch2(a, low,high, key): # 재귀 구조
    if low>high:
      return -1 # 검색 실패
    else:
      middle = (low+high)//2
      if key == a[middle]:
          return middle # 찾으면 index 반환
      elif key < a[middle]:
          return binarySearch2(a,low,middle-1,key)       
      else: # key > a[middle]
          return binarySearch2(a,middle+1,high,key)
```
---  
### 05 분할 정복 사례  

- 병합 정렬  
: 외부 정렬의 기본이 되는 정렬 알고리즘  
  
- 퀵 정렬  
: 매우 큰 입력 데이터에 대해서 좋은 성능을 보이는 알고리즘  
  
- 최근접 점의 쌍 문제  
: 2차원 평면상의 n개의 점이 입력으로 주어질 때, 거리가 가장 가까운 한 쌍의 점을 찾는 문제  
  
