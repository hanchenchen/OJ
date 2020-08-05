# [BestCoder2020-3-Distance](http://acm.hdu.edu.cn/showproblem.php?pid=6776)

2020 年百度之星·程序设计大赛 - 初赛三 Distance

```c++
#include<bits/stdc++.h>
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int test;
    cin>>test;
    while (test--) {
        vector<long long> arr(1);
        int x = 0,n = 0,minv = 1e9+7;
        cin>>n;
        for(int i=0;i<n;i++){
            scanf("%d",&x);
            minv = min(x,minv);
            arr.push_back((long long)x);
        }
        for(int i=1;i<=n;i++){
            arr[i]-=minv;
        }
        sort(arr.begin(),arr.end());
        long long ans = 0;
        for(int i=1;i<=n/2;i++){
            ans += (2*i-n-1)*arr[i] + (2*(n/2+i)-n-1)*arr[n/2+i];
        }
        if(n%2){
            int i=n;
            ans += (2*i-n-1)*arr[i] ;
        }
        cout<<ans<<endl;
    }
    return 0;
}

```

