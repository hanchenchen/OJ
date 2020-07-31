# [BestCoder2020-3-Chess](http://acm.hdu.edu.cn/showproblem.php?pid=6787)

| [hanchenchen](http://acm.hdu.edu.cn/userstatus.php?user=hanchenchen) | 702MS | 1480K | 1715B | G++  | 2020-07-27 14:08:58 |
| ------------------------------------------------------------ | ----- | ----- | ----- | ---- | ------------------- |
|                                                              |       |       |       |      |                     |

#### 方法一：动态规划

C++

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
        int n,m,ans=0;
        cin>>n>>m;
        long long dp[1000+5][11]={0};
        memset(dp[0],0,sizeof(dp));
        dp[0][0]=1;
        for(int i=2;i<=n;i++){
            for(int j=m;j>0;j--){
                long long s = dp[j][0];
                for(int k=10;k>0;k--){
                    s=(s+dp[j][k])%(int)(1e9+7);
                    dp[j][k]=dp[j-1][k-1]*(i-1)%(int)(1e9+7);
                }
                dp[j][0]=s;
            }
            /*
            for(int j=0;j<=m;j++){
                for(int k=1;k<11;k++){
                    cout<<dp[j][k]<<' ';
                }
                cout<<endl;
            }
            cout<<endl;
             */
        }
        if(dp[m][0]||m==0)
            cout<<dp[m][0]<<endl;
        else
            cout<<-1<<endl;
        
    }
    return 0;
}

```

