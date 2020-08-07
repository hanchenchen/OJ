# [-BestCoder2020-2-Drink](http://acm.hdu.edu.cn/showproblem.php?pid=6779)

WA
```c++
//#include<bits/stdc++.h>
#include <iostream>
#include <vector>
#include <map>
#include <queue>

using namespace std;
const int maxn = 35,INF = 0x3f3f3f3f;
struct Edge{
    int from, to, cap, flow, cost;
    Edge(int u, int v, int c, int f, int w):from(u), to(v), cap(c), flow(f), cost(w){}
};
struct EdmondsKarp{
    int n,m;
    vector<Edge> edges;
    vector<int> G[maxn];
    int a[maxn]={0},p[maxn],d[maxn],inq[maxn];
    
    void init(int num){
        n = num;
        edges = vector<Edge> ();
        for(int i=0;i<n;i++){
            G[i]=vector<int> ();
        }
    }
    
    void addEdge(int from, int to, int cap, int flow, int cost){
        edges.push_back(Edge(from,to,cap,0,cost));
        edges.push_back(Edge(to,from,0,0,-cost));
        m =(int)edges.size();
        G[from].push_back(m-2);
        G[to].push_back(m-1);
    }
    bool BeelmanFord(int s, int t, long long &flow,long long &cost){
        memset(inq,0,sizeof(inq));
        for(int i=0;i<n;i++){
            d[i]=0xcfcfcfcf;
            p[i]=0;
        }
        d[s]=0;
        inq[s] = 1;
        p[s] = 0;
        a[s] = INF;
        queue<int> q;
        q.push(s);
        while(!q.empty()){
            int x = q.front();
            q.pop();
            inq[x]=0;
            for(int i=0;i<G[x].size();i++){
                Edge e = edges[G[x][i]];
                if(d[e.to]<d[x]+e.cost&&e.cap>e.flow){
                    d[e.to]=d[x]+e.cost;
                    p[e.to] = G[x][i];
                    a[e.to] = min(a[x], e.cap-e.flow);
                    if(!inq[e.to]){
                        q.push(e.to);
                        inq[x]=1;
                    }
                }
            }
        }
        return d[t]!=0xcfcfcfcf;
        
    }
    long long maxFlow(int s, int t){
        long long flow = 0,cost = 0;
        
        while(BeelmanFord(s,t,flow,cost)){
            flow+=(long long)a[t];
            cost+=(long long)a[t]*(long long)d[t];
            for(int u = t;u!=s;u=edges[p[u]].from){
                edges[p[u]].flow+=a[t];
                edges[p[u]^1].flow-=a[t];
            }
        }
        
        return cost;
    }
};
int main() {
    int test;
    cin>>test;
    while (test--) {
        int n,a,b,c;
        int arr[6] ={0};
        memset(arr,0,sizeof(arr));
        cin>>n>>a>>b>>c;
        int x;
        for(int i=0;i<n;i++){
            cin>>x;
            if(x==12){
                arr[0]++;
            }else if(x==21){
                arr[1]++;
            }else if(x==102){
                arr[2]++;
            }else if(x==120){
                arr[3]++;
            }else if(x==201){
                arr[4]++;
            }else{
                arr[5]++;
            }
        }
        EdmondsKarp ek;
        ek.init(11);
        ek.addEdge(0,1,arr[0],0,0);
        ek.addEdge(1,7,INF,0,3);
        ek.addEdge(1,8,INF,0,2);
        ek.addEdge(1,9,INF,0,1);
        
        ek.addEdge(0,2,arr[1],0,0);
        ek.addEdge(2,7,INF,0,3);
        ek.addEdge(2,8,INF,0,1);
        ek.addEdge(2,9,INF,0,2);
        
        ek.addEdge(0,3,arr[2],0,0);
        ek.addEdge(3,7,INF,0,2);
        ek.addEdge(3,8,INF,0,3);
        ek.addEdge(3,9,INF,0,1);
        
        ek.addEdge(0,4,arr[3],0,0);
        ek.addEdge(4,7,INF,0,1);
        ek.addEdge(4,8,INF,0,3);
        ek.addEdge(4,9,INF,0,2);
        
        ek.addEdge(0,5,arr[4],0,0);
        ek.addEdge(5,7,INF,0,2);
        ek.addEdge(5,8,INF,0,1);
        ek.addEdge(5,9,INF,0,3);
        
        ek.addEdge(0,6,arr[5],0,0);
        ek.addEdge(6,7,INF,0,1);
        ek.addEdge(6,8,INF,0,2);
        ek.addEdge(6,9,INF,0,3);
        
        ek.addEdge(7,10,a,0,0);
        ek.addEdge(8,10,b,0,0);
        ek.addEdge(9,10,c,0,0);
        
        cout<<ek.maxFlow(0,10)<<endl;
        
    }
    return 0;
}
/*
 5
 3 1 1 1
 012
 102
 201
 3 1 1 1
 012
 012
 012
 6 2 2 2
 012
 021
 120
 102
 210
 201
 0 0 0 0
 6 1 2 3
 012
 021
 120
 102
 210
 201
 */

```

