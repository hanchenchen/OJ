# [BestCoder2020-3-Discount](http://acm.hdu.edu.cn/showproblem.php?pid=6783)

2020 年百度之星·程序设计大赛 - 初赛三 Discount

```c++
//#include<bits/stdc++.h>
#include <iostream>
#include <vector>
#include <map>
using namespace std;

int main() {
    int test;
    cin>>test;
    while (test--) {
        int n;
        cin>>n;
        double b[105]={0},c[105]={0},ans=0;
        
        for(int i=1;i<=n;i++){
            scanf("%lf %lf",&b[i],&c[i]);
            ans = max(ans,(1.0-c[i])/(b[i]-c[i]+1.0));
        }
        printf("%0.5lf\n",ans);
    }
    return 0;
}
```

