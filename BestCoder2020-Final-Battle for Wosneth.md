# [BestCoder2020-Final-Battle for Wosneth](http://acm.hdu.edu.cn/showproblem.php?pid=6838)

```c++
//#include<bits/stdc++.h>
#include <iostream>
#include <vector>
#include <map>
#include <queue>
#define ll long long
using namespace std;
const int maxn = 1e5+10;
const ll mod = 998244353;
// 费马小定理求逆元
long long qpower(long long a,long long b,int mod){
    long long ans = 1;
    while(b){
        if(b&1){
            ans*=a;
            ans%=mod;
        }
        b>>=1;
        a=a*a%mod;
    }
    return ans;
}
int main() {
    int test;
    cin>>test;

    while (test--) {
        int m,p,q;
        cin>>m>>p>>q;
        ll inv_100 =qpower(100,mod-2,mod);
        ll inv_p =qpower(p,mod-2,mod);
        ll inv_q =qpower(q,mod-2,mod);
        ll times = m*100ll%mod*inv_p%mod;
        ll a = m;
        a=(a-(times+mod-1)%mod*q%mod*inv_100%mod+mod)%mod;
        cout<<a<<endl;
        
        }
    return 0;
}


```

气死我了😤，常数100要写成100ll，否则WA