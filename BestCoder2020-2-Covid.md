# [BestCoder2020-2-Covid](http://acm.hdu.edu.cn/showproblem.php?pid=6777)

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
        map<int,vector<int>> mm;
        int n,len,t,p;
        int mod = 11;
        cin>>n;
        for(int i=1;i<=n;i++){
            scanf("%d",&len);
            for(int j=0;j<len;j++){
                scanf("%d %d",&t,&p);
                mm[t*mod+p].push_back(i);
            }
        }
        vector<int> ans(n+1,0);
        ans[1]=1;
        for(int t=1;t<=100;t++){
            for(int p=1;p<=10;p++){
                int a = 0;
                for(auto iter:mm[t*mod+p]){
                    a = ans[iter];
                    if(a)
                        break;
                }
                if(a){
                    for(auto iter:mm[t*mod+p]){
                        ans[iter]=1;
                    }
                }
            }
        }
        int flag = 0;
        for(int i=1;i<=n;i++){
            if (ans[i]){
                if(flag)printf(" ");
                printf("%d",i);
                flag=1;
            }
        }
        cout<<endl;
    }
    return 0;
}

```

