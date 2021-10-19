### DFS

```c++
#include<iostream>
using namespace std;

char a[105][105];
int n,m;

void dfs(int x,int y)
{
    a[x][y]='.';
    for(int dx=-1;dx<=1;dx++){
        for(int dy=-1;dy<=1;dy++){
            int nx=x+dx,ny=y+dy;
            if(nx>=0&&nx<n&&ny>=0&&ny<m&&a[nx][ny]=='W')
                dfs(nx,ny);
        }
    }
}

int main()
{
    int ans=0;
    cin>>n>>m;
    for(int i=0;i<n;i++){
        for(int j=0;j<m;j++){
            cin>>a[i][j];
        }
    }
    for(int i=0;i<n;i++){
        for(int j=0;j<m;j++){
            if(a[i][j]=='W'){
                dfs(i,j);
                ans++;
            }
        }
    }
    cout<<ans<<endl;
    return 0;
}


```

### BFS

```c++
int bfs()
{
    queue<P> que;
    for(int i=0;i<n;i++){
        for(int j=0;j<m;j++){
            d[i][j]=INF;
        }
    }
    que.push(P(sx,sy));
    d[sx][sy]=0;

    while(que.size()){
        P p =que.front(); que.pop();
        if(p.first==gx&&p.second==gy) break;

        for(int i=0;i<4;i++){
            int nx=p.first+dx[i],ny=p.second+dy[i];
            if(nx>=0&&nx<n&&ny>=0&&ny<m&&map[nx][ny]!='#'&& d[nx][ny]==INF){
                que.push(P(nx,ny));
                d[nx][ny]=d[p.first][p.second]+1;
            }
        }
    }
    return d[gx][gy];
}
```

### 贪心

```c++
#include<iostream>
#include<algorithm>
using namespace std;

int s[10000],t[10000];
int n;
pair<int,int> job[10000];

int main()
{
    int cnt=0,t=0;
    cin>>n;
    for(int i=0;i<n;i++) cin>>job[i].second;
    for(int i=0;i<n;i++) cin>>job[i].first;  //sort对pair数据进行排序，默认对first升序，因此把结束时间填入first
    sort(job,job+n);
    for(int i=0;i<n;i++){
        if(t<job[i].second){
            cnt++;
            t=job[i].first;
        }
    }
    printf("%d",cnt);
    return 0;
}
```

```c++
#include<bits/stdc++.h>
using namespace std;

string s,t;
int n;

int main()
{
    cin>>n;
    cin>>s;
    int begin=0,end=n-1;
    while(begin<=end){
        bool left = false;
        for(int i=0;begin+i<=end;i++){
            if(s[begin+i]<s[end-i]){
                left = true;
                break;
            }else if(s[begin+i]>s[end-i]){
                left = false;
                break;
            }
        }
        if(left) putchar(s[begin++]);
        else putchar(s[end--]);
    }
    
    return 0;
}
```

```c++
#include<iostream>
#include<algorithm>
using namespace std;

int n,r;
int a[1005];

int main()
{
    while(scanf("%d %d",&r,&n)&&r!=-1&&n!=-1){
        for(int i=0;i<n;i++){
            scanf("%d",&a[i]);
        }
        sort(a,a+n);
        int i=0;
        int ans=0;
        while(i<n){
            int tmp1=a[i++];
            while(i<n&&tmp1+r>=a[i]) i++;
            int tmp2=a[i-1];
            while(i<n&&tmp2+r>=a[i]) i++;
            ans++;
        }
        printf("%d\n",ans);
    }
    return 0;
}
```

