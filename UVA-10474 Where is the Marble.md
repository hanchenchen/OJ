## [UVA-10474 Where is the Marble?][https://vjudge.net/problem/UVA-10474]

 ```python
test = 1
while 1:
    [n, q] = [int(i) for i in input().split()]
    if n == 0 and q==0:
        exit()
    arr = []
    for i in range(n):
        arr.append(int(input()))
    arr.sort()
    dic = {}
    for i in range(n):
        if not arr[i] in dic.keys():
            dic[arr[i]] = i+1
    print('CASE# {0}:'.format(test))
    test+=1
    for i in range(q):
        x = int(input())
        if x in dic.keys():
            print('{0} found at {1}'.format(x, dic[x]))
        else:
            print('{0} not found'.format(x))
'''
4 1
2
3
5
1
5 
5 2
1
3
3
3
1
2
3 
0 0

'''
 ```



