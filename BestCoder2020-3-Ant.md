# [BestCoder2020-3-Ant](http://acm.hdu.edu.cn/showproblem.php?pid=6788)

#### 方法一：逆元

##### 快速幂+费马小定理

```c++
//#include<bits/stdc++.h>
#include <iostream>
#include <vector>
#include <map>
using namespace std;


vector<int> path;
vector<int> arr[100000+5];
int father[100000+5],son[100000+5];
void find_path(int x, int pre,int m){
    son[x]=0;
    father[x]=pre;
    for(auto i:arr[x]){
        if(i==pre||son[i])
            continue;
        son[x]++;
        find_path(i,x,m);
    }
}

// 扩展欧几里得求逆元
void exgcd(int a,int b,int &d,int &x,int &y){
    if(!b){
        d = a;
        x = 1;
        y = 0;
    }else{
        exgcd(b,a%b,d,y,x);
        y-=a/b*x;
    }
}
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
    int mod=1e9+7;
    long long inv[200002]={0};
    for(int i=1;i<200002;i++){
        inv[i]=qpower(i,mod-2,mod);
    }
    while (test--) {
        
        int n,m,x,y;
        scanf("%d %d",&n,&m);
        //cin>>n>>m;
        for(int i=0;i<=n;i++){
            arr[i]=vector<int>(0);
            //i.clear();
        }
        memset(father,0,sizeof(father));
        memset(son,0,sizeof(son));
        for(int i=0;i<n-1;i++){
            scanf("%d %d",&x,&y);
            //cin>>x>>y;
            arr[x].push_back(y);
            arr[y].push_back(x);
            //father[y]=x;
            //son[x]++;
        }
        father[0]=1;
        find_path(1,1,m);
        int i=father[m];
        long long a=0,b=1,c,k=1;
        while(i!=1){
            /*
             c=(long long)son[i];
             a=(a*c%mod+b*(c-1)%mod)%mod;
             b=b*c%mod;
             k=k*(c+1)%mod;
             i=father[i];
             */
            c=(long long)son[i];
            a=(a+(c-1)*inv[c])%mod;
            k=(k*inv[c+1])%mod;
            //cout<<"!"<<a<<" "<<c<<" "<<i<<endl;
            i=father[i];
        }
        if(1!=m){
            /*
             c=(long long)son[i];
             a=(a+b)%mod;
             k=k*c%mod;
             b = b*k%mod;
             */
            c=(long long)son[i];
            if(c>1){
                a=(a+1)%mod;
            }
            a=(a+1)%mod;
            k=(k*inv[c])%mod;
            a=a*k%mod;
        }else{
            a=1;
        }
        
        
        //cout<<"!"<<a<<" "<<k<<" "<<endl;
        long long b_1,d,k_m;
        /*
         exgcd((int)a,(int)b,d,b_1,k_m);
         a/=d;
         b/=d;
         */
        //exgcd((int)b,(int)1e9+7,d,b_1,k_m);
        //b_1=(b_1+(int)1e9+7)%((int)1e9+7);
        //b_1= qpower(b,mod-2,mod);
        //a = (a*b_1)%((int)1e9+7);
        //cout<<"!!"<<b_1<<" "<<b<<" "<<(b_1*b)%((int)1e9+7)<<endl;
        cout<<a<<endl;
        
    }
    return 0;
}
/*
 3
 1 1
 4 2
 1 2
 1 3
 1 4
 5 4
 1 2
 1 3
 3 4
 3 5
 
 */



```

##### 扩展欧几里得

#### ⚠️

- $\left(a \% mod \right) / \left(b \% mod\right) \neq \left(a /b \right)\%mod$，所以应该先求逆，在求模
- 根结点有特殊情况。

