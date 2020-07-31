# [BestCoder2020-3-Fight](http://acm.hdu.edu.cn/showproblem.php?pid=6789)

#### 方法一：双重循环

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
        int x,y,z;
        cin>>x>>y>>z;
        int ans=1e9+7;
        int l,m,r;
        int a,b,c;
        for(int i=0;i<=1000;i++){
            l = 1000 - y*i;
            if(l+y<=0)
                continue;
            for(int j=0;j<=1000;j++){
                r = 1000 - y*j;
                if(r+y<=0)
                    continue;
                m = 1000 - i*x-j*z;
                if(m+max(x,z)<=0)
                    continue;
                int maxi;
                if(m<=0){
                    if(l<=0&&r<=0){
                        maxi=0;
                    }else if(l<=0){
                        maxi=0;
                    }else if(r<=0){
                        maxi=0;
                    }else{
                        maxi=min((l+z-1)/z,(r+x-1)/x);
                    }
                }else{
                    if(l<=0&&r<=0){
                        maxi=0;
                    }else if(l<=0){
                        maxi=r/x+(r%x!=0);
                    }else if(r<=0){
                        maxi=l/z+(l%z!=0);
                    }else{
                        if((l+z-1)/z==(r+x-1)/x)
                            maxi=(r+x-1)/x;
                        else
                            maxi=1e9;
                    }
                }
                
                if(ans>i+j+maxi){
                    a=i,b=j,c=maxi;
                }
                 
                ans=min(ans,i+j+maxi);
            }
        }
        //cout<<a<<" "<<b<<" "<<c<<":";
        //cout<<1000-a*y-c*z<<" "<<1000-a*x-b*z<<" "<<1000-b*y-c*x<<endl;
        cout<<ans<<endl;
    }
    return 0;
}
/*

 2
 1 1 1
 1 2 3

 */

```

#### ⚠️

当a>0、b>0，使两个相互攻击后都小于零，需要满足攻击次数相等。