# [UVA-12169 Disgruntled Judge](https://vjudge.net/problem/UVA-12169)

|   Status    | Accepted            |
| :---------: | ------------------- |
|    Time     | 40ms                |
|   Length    | 932                 |
|    Lang     | PYTH3 3.5.1         |
|  Submitted  | 2020-07-22 16:56:04 |
| RemoteRunId | 25282403            |

Python3

```python
def exgcd(a: int, b: int, d: int, x: int, y: int):
    if not b:
        return a, 1, 0
    else:
        d, y, x = exgcd(b, a % b, d, y, x)
        y -= (a // b) * x
        return d, x, y


t = int(input())
arr = [-1]
for i in range(t):
    arr.append(int(input()))
    arr.append(-1)
if t <= 1:
    print(0)
    print(0)
    exit()
for a in range(10001):
    d = (arr[3] - a ** 2 * arr[1] + 10001) % 10001
    gcd, x, y = exgcd(a + 1, 10001, 0, 0, 0)
    # print(gcd, x, y, (a + 1) * x + 10001 * y)
    if d % gcd:
        continue
    b = (x * d // gcd + 10001 // gcd) % 10001
    # print(a, b)
    for i in range(2, 2 * t + 1):
        if i % 2:
            if arr[i] != (a * arr[i - 1] + b) % 10001:
                break
        else:
            arr[i] = (a * arr[i - 1] + b) % 10001
        if i == 2 * t:
            for j in range(2, 2 * t + 1, 2):
                print(arr[j])
            exit()

'''
3
17
822
3014
'''
```