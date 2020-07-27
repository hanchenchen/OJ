# [BestCoder2020-3-Permutation](http://acm.hdu.edu.cn/showproblem.php?pid=6785)

2020 年百度之星·程序设计大赛 - 初赛三 Permutation

```c++
#include<bits/stdc++.h>
#include <iostream>
#include <vector>
#include <map>
using namespace std;

int main() {
    int test;
    cin>>test;
    while (test--) {
        long long n,m;
        
        // cout<<n<<m<<endl;
        scanf("%lld %lld",&n,&m);
        m = min(n/2,m);
        printf("%lld\n",2*n*m-(1+m)*m-m*m);
    }
    return 0;
}
```

