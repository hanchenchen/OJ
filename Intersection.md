# [Intersection](http://acm.hdu.edu.cn/showproblem.php?pid=6786)

2020 年百度之星·程序设计大赛 - 初赛三

```python
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
        int arr[3][100000+5]={0},ans=0;
        int x,y;
        int max_1=-1,max_2=-2;
        for(int i=0;i<n;i++){
            cin>>x>>y;
            //x = 2;
            //y = i+1;
            arr[x][y]=1;
            if(x==1){
                max_1=max(max_1,y);
            }else{
                max_2=max(max_2,y);
            }
        }
        
        //cout<<ans<<endl;
        if(arr[1][max_2+1])max_2++;
\
        ans=max(max_1+1,max_2+2);
        cout<<ans<<endl;
    }
    return 0;
}
```

