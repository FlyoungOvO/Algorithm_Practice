CF6B
```c++
#include<iostream>
#include<cstring>
using namespace std;

char map[105][105];
int n,m;
int dx[4]={1,0,-1,0};
int dy[4]={0,1,0,-1};

void dfs(int x,int y,char c)
{
	map[x][y]=c;
	for(int i=0;i<4;i++){
		int nx=x+dx[i],ny=y+dy[i];
		if(map[nx][ny]=='.'&&nx>=0&&nx<n&&ny>=0&&ny<m){
			if(map[x][y]=='B')
				dfs(nx,ny,'W');
			if(map[x][y]=='W')
				dfs(nx,ny,'B');
		}
	}
}

void MyPrint(int a,int b)
{
	for(int i=0;i<a;i++){
		for(int j=0;j<b;j++){
			cout<<map[i][j];
		}
		cout<<endl;
	}
}

int main(){
	cin>>n>>m;
	int sx,sy;
	for(int i=0;i<n;i++){
		for(int j=0;j<m;j++){
			cin>>map[i][j];
		}
	}
    for(int i=0;i<n;i++){
        for(int j=0;j<m;j++){
            if(map[i][j]=='.'){
                dfs(i,j,'B');
            }
        }
    }
	MyPrint(n,m);
	return 0;
}
```
