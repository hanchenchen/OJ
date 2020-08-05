#[BestCoder2020-3-Graph](http://acm.hdu.edu.cn/showproblem.php?pid=6790)

只求出每个环的大小
```c++
#include<iostream>
#include<map>
#include<vector>
//#include<bits/stdc++.h>
using namespace std;

const int max_nm = 1e5+2,mod = 998244353;
int vis[max_nm]={0},parent[max_nm]={0},level[max_nm]={0};
vector<int> arr[max_nm],son[max_nm],circle;
map<int,map<int,int>> isCircle;


vector<int> Subtraction(vector<int> &a,vector<int> &b){
    vector<int> re;
    int i=0,j=0;
    for(;i<a.size();i++){
        if(a[i]==b[j]){
            j++;
        }else{
            re.push_back(b[j]);
        }
    }
    return re;
}

int lca(int a, int b){
    int re = 1;
    while(level[a]>level[b]){
        if(isCircle[parent[a]][a])
            return -1;
        isCircle[parent[a]][a]=1;
        a=parent[a];
        re++;
    }
    while(level[a]<level[b]){
        if(isCircle[parent[b]][b])
            return -1;
        isCircle[parent[b]][b]=1;
        b=parent[b];
        re++;
    }
    while(a!=b){
        if(isCircle[parent[a]][a])
            return -1;
        isCircle[parent[a]][a]=1;
        a=parent[a];
        if(isCircle[parent[b]][b])
            return -1;
        isCircle[parent[b]][b]=1;
        b=parent[b];
        re++;
        re++;
    }
    return re;
}
bool dfs(int x, int pre){
    cout<<x<<" dfs"<<endl;
    vis[x]=1;
    level[x]=level[pre]+1;
    parent[x]=pre;
    son[pre].push_back(x);
    for(int i=0;i<arr[x].size();i++){
        if(vis[arr[x][i]]){
            if(parent[x]==arr[x][i])
                continue;
            
            int l =lca(arr[x][i],x);
            if(l>=0){
                circle.push_back(l);
            }else{
                return false;
            }
            continue;
        }
        if(!dfs(arr[x][i],x))
            return false;
    }
    return true;
}
int main(){
    int test = 0;
    cin>>test;
    
    while(test--){
        int n,m,u,v;
        
        cin>>n>>m;
        for(int i=0;i<m;i++){
            cin>>u>>v;
            arr[u].push_back(v);
            arr[v].push_back(u);
        }
        dfs(1,0);
        for(int i=1;i<=n;i++){
            cout<<vis[i]<<" "<<parent[i]<<" "<<level[i]<<endl;
        }
        for(int i=0;i<circle.size();i++){
            cout<<circle[i]<<" c"<<endl;
        }
    }
    return 0;
}

```

