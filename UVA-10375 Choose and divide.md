# [UVA-10375 Choose and divide][https://vjudge.net/problem/UVA-10375]

#### 方法一：唯一分解定理

```python
prime = []
maxNum = 10001
num = []
memo = [[] for i in range(maxNum)]


def findPrime():
    global prime
    arr = [1 for i in range(maxNum)]
    for i in range(2, maxNum):
        if arr[i]:
            prime.append(i)
        else:
            continue
        for j in range(i + i, maxNum, i):
            arr[j] = 0


def decompose(x: int, p: int):
    global memo
    if len(memo[x]) != 0 :
        for i in memo[x]:
            num[i] += p
        return
    i = 0
    index = x
    while i < len(prime) and x > 1:
        if not x % prime[i]:
            memo[index].append(i)
            x //= prime[i]
            num[i] += p
        else:
            i += 1


def factorial(x: int, p: int):
    for i in range(x + 1):
        decompose(i, p)


def addTogether() -> float:
    re = 1
    for i in range(len(prime)):
        re *= prime[i] ** num[i]
    return re


findPrime()
import sys
for line in sys.stdin:
    num = [0 for i in range(maxNum)]
    p, q, r, s = [int(i) for i in line.split()]
    factorial(p, 1)
    factorial(r - s, 1)
    factorial(s, 1)
    factorial(p - q, -1)
    factorial(q, -1)
    factorial(r, -1)
    print('{0:.5f}'.format(addTogether()))

'''
10 5 14 9
93 45 84 59
145 95 143 92
995 487 996 488
2000 1000 1999 999
9998 4999 9996 4998
9999 5000 9999 5256
1271 18 1922 18
156 45 156 46
5600 2800 5595 2795
9191 19 9189 19
9876 1234 9899 1222
'''

```

⚠️：如何输入一长段话

```python
import sys
for line in sys.stdin:
```

#### 方法二：？？一遍遍历

```python
import sys
for line in sys.stdin:
    p, q, r, s = [int(i) for i in line.split()]
    ans = 1
    for i in range(1, max(q, s) + 1):
        if i <= q:
            ans = ans * (p - q + i) / i
        if i <= s:
            ans = ans / (r - s + i) * i
    print('{0:.5f}'.format(ans))
```

