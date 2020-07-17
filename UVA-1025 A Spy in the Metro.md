# [UVA-1025 A Spy in the Metro](https://vjudge.net/problem/UVA-1025)

#### 方法一：动态规划

```python
num = 0
while 1:
    n = int(input())
    if not n:
        break
    t = int(input())
    betweenStation = [int(i) for i in input().split(' ')]
    m1 = int(input())
    departTime1 = [int(i) for i in input().split(' ')]
    m2 = int(input())
    departTime2 = [int(i) for i in input().split(' ')]

    stoptrains1 = [[0 for j in range(n)] for i in range(t + 1)]
    stoptrains2 = [[0 for j in range(n)] for i in range(t + 1)]
    for i in range(m1):
        nowTime = departTime1[i]
        for j in range(n):
            if nowTime > t:
                break
            stoptrains1[nowTime][j] = 1
            if j < n - 1:
                nowTime += betweenStation[j]
    for i in range(m2):
        nowTime = departTime2[i]
        for j in range(n):
            if nowTime > t:
                break
            stoptrains2[nowTime][n - j - 1] = 1
            if j < n - 1:
                nowTime += betweenStation[n - j - 2]

    dp = [[1e5 for j in range(n)] for i in range(t + 5)]
    dp[0][0] = 0
    for i in range(t + 1):
        # print(dp[i])
        for j in range(n):
            dp[i + 1][j] = min(dp[i][j] + 1, dp[i + 1][j])
            if j < n - 1 and stoptrains1[i][j] and i + betweenStation[j] <= t:
                dp[i + betweenStation[j]][j + 1] = min(dp[i][j], dp[i + betweenStation[j]][j + 1])
            if j > 0 and stoptrains2[i][j] and i + betweenStation[j - 1] <= t:
                dp[i + betweenStation[j - 1]][j - 1] = min(dp[i][j], dp[i + betweenStation[j - 1]][j - 1])
    num += 1
    if dp[t][n - 1] <= t:
        print('Case Number', str(num) + ':', dp[t][n - 1])
    else:
        print('Case Number', str(num) + ':', 'impossible')

'''

4
55
5 10 15
4
0 5 10 20
4
0 5 10 15
4
18
1 2 3
5
0 3 6 10 12
6
0 3 5 7 12 15
2
30
20
1
20
7
1 3 5 7 11 13 17
0

'''

```

⚠️

T=0的情况