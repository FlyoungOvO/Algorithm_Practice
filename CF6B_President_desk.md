CF6B President desk

```c++
#include<iostream>
using namespace std;

bool vis[26];
char desk[105][105];
int n,m;
char p;
int dx[4]={1,0,-1,0};
int dy[4]={0,1,0,-1};

void dfs(int x,int y)
{
    int nx,ny;
    for(int i=0;i<4;i++){
        nx=x+dx[i];
        ny=y+dy[i];
        if(nx>=0&&nx<n&&ny>=0&&ny<m){
            if(desk[nx][ny]!='.'){
                if(desk[nx][ny]!=p){
                    vis[desk[nx][ny]-'A']=1;
                    desk[nx][ny]='.';
                }
                else{
                    desk[nx][ny]='.';
                    dfs(nx,ny);
                }
            }
        }
    }
}

int main()
{
    cin>>n>>m>>p;
    int sx,sy;
    for(int i=0;i<n;i++){
        for(int j=0;j<m;j++)
            cin>>desk[i][j];
    }
    
    for(int i=0;i<n;i++){
        for(int j=0;j<m;j++){
            if(desk[i][j]==p){
                dfs(i,j);
                break;
            }
        }
    }
    int ans=0;
    for(int i=0;i<26;i++){
        if(vis[i])
            ans++;
    }
    cout<<ans<<endl;
    return 0;
}
```
