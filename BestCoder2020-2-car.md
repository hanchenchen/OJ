# [BestCoder2020-2-Car](http://acm.hdu.edu.cn/showproblem.php?pid=6778)

```c++
//#include<bits/stdc++.h>
#include <iostream>
#include <vector>
#include <map>

using namespace std;
int n,arr[10],day[5],ans,c;
bool dfs(int num, int m, int x){
    c++;
    if(num == 10){
        int maxi = 0;
        for(auto i:day){
            maxi = max(maxi,i);
        }
        return maxi<=m;
    }
    bool flag=true;
    for(int i=0;i<5&&i<=x;i++){
        if(day[i]<=m)
            continue;
        flag=false;
        day[i]-=arr[num];
        if(i==x){
            if(dfs(num+1,m,x+1)){
                day[i]+=arr[num];
                return true;
            }
        }else{
            if(dfs(num+1,m,x)){
                day[i]+=arr[num];
                return true;
            }
        }
        day[i]+=arr[num];
    }
    return flag;
}
int main() {
    int test;
    cin>>test;
    while (test--) {
        cin>>n;
        int x;
        ans = n+1;
        memset(arr,0,sizeof(arr));
        for(int i=1;i<=n;i++){
            scanf("%d",&x);
            arr[x%10]++;
        }
        for(int i=0;i<5;i++){
            day[i]=n;
        }
        int left=1,right=n;
        while(left<right){
            int  mid = (left+right)/2;
            if(dfs(0,mid,1)){
                right = mid;
            }else{
                left = mid+1;
            }
        }
        cout<<left<<endl;
        //cout<<c<<"!"<<endl;
    }
    return 0;
}
/*
 12207031!

 8
 24414062!
 8
 17595733!
 752830!
 */

```

##### ⚠️

因为星期一、星期二……的顺序并不重要，所以`DSF`中的x能够让下次`DFS`迭代仅能选择一个空位。