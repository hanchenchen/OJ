# [BestCoder2020-3-Poker](http://acm.hdu.edu.cn/showproblem.php?pid=6775)

2020 年百度之星·程序设计大赛 - 初赛三 Poker

```c++
#include<iostream>
#include<map>
#include<vector>
//#include<bits/stdc++.h>
using namespace std;

int main(){
    int test = 0;
    cin>>test;
    
    while(test--){
        int n,m,p;
        int ans=0;
        cin>>n>>m>>p;
        if(n<m){
            cout<<0<<endl;
            continue;
        }
        int y = m-(100-p)*m/100;
        ans = (n-m)/y;
        n-=ans*y;
        while(n>=m&&n>0){
            //cout<<n<<" n"<<endl;
            if(n<m)
                break;
            int x = n/m;
            n-=x*y;
            ans+=x;
        }
        cout<<ans<<endl;
    }
    return 0;
}
```

