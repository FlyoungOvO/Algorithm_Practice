

# 洛谷题解笔记

### P 5143 攀爬者![image-20211001142044733](C:\Users\DFlyoung\AppData\Roaming\Typora\typora-user-images\image-20211001142044733.png)

```c++
#include<iostream>
#include<cmath>
#include<algorithm>
using namespace std;

struct pos    //用结构体表示一个三维坐标，同时便于后面只比较z坐标
{
    int x,y,z;
}a[50005];   //用数组来储存该种结构体

bool compare(pos a,pos b) //比较函数，让sort()按照z坐标从小到大的顺序进行排序
{
    return a.z<=b.z;
}   //可用重载小于运算符的方式优化速度（还没学，记得补）
int main()
{
    int n;
    double ans=0,dis=0; //初始化数据（这真的很重要！）
    cin>>n;
    for(int i=0;i<n;i++){
        cin>>a[i].x>>a[i].y>>a[i].z;
    }
    sort(a,a+n,compare); //前两个参数分别为起始地址和结束地址
    for(int i=0;i<n-1;i++){ //注意i<n-1，如果i<n的话，i+1会取到第n+1个位置
        dis=sqrt(pow(a[i+1].x-a[i].x,2)+pow(a[i+1].y-a[i].y,2)+pow(a[i+1].z-a[i].z,2));
        ans+=dis;
    }
    printf("%.3lf",ans);
    return 0;
}
```



### P 1271 选举学生会

![image-20211001144126426](C:\Users\DFlyoung\AppData\Roaming\Typora\typora-user-images\image-20211001144126426.png)

```c++
#include<iostream>
#include<algorithm>
using namespace std;

int main()   //对STL中sort算法的简单应用
{
    int n,m;
    int a[2000010];
    cin>>n>>m;
    for(int i=0;i<m;i++){
        cin>>a[i];
    }
    sort(a,a+m);
    for(int i=0;i<m;i++){
        cout<<a[i]<<" ";
    }
    return 0;
}

```

为了进一步优化，我们用桶排，这样就不需要开辟像a[200000]这么大一片内存了

```c++
#include<iostream>
using namespace std;
int b[1000];

int main()
{
    int n,m,a;
    cin>>n>>m;
    for(int i=0;i<m;i++){
        cin>>a;
        ++b[a];  //貌似b[a]++在这里也可以
    }
    for(int i=0;i<1000;i++){
        for(int j=0;j<b[i];j++){
            cout<<i<<" ";
        }
    }
    return 0;
}

```



### P1093 奖学金

![image-20211003143703039](C:\Users\DFlyoung\AppData\Roaming\Typora\typora-user-images\image-20211003143703039.png)

```c++
#include <iostream>
#include <algorithm>
using namespace std;

typedef struct Stu
{
    int num;
    int chi;
    int math;
    int eng;
    int sum = 0;
} stu;

bool cmp(stu a, stu b)
{
    if (a.sum != b.sum)
        return a.sum > b.sum;
    else  //之前尝试过用两个if，但编译器会报warning，其原因是编译器考虑到2个if可能无法包含所有情况，造成没有返回值的情况
    {
        if(a.chi!=b.chi)
            return a.chi>b.chi;
        else
            return a.num<b.num;
    }
}

int main()
{
    int n;
    cin >> n;
    stu a[305];
    for (int i = 1; i <= n; i++)
    {
        scanf("%d%d%d", &a[i].chi, &a[i].math, &a[i].eng);
        a[i].num = i;
        a[i].sum = a[i].chi + a[i].math + a[i].eng;
    }
    sort(a + 1, a + n + 1, cmp); //sort(首地址，结束地址的下一位，cmp)
    for (int j = 1; j <= 5; j++)
    {
        printf("%d %d\n", a[j].num, a[j].sum);
    }
    return 0;
}
```



### P1012 拼数

![image-20211006231334878](C:\Users\DFlyoung\AppData\Roaming\Typora\typora-user-images\image-20211006231334878.png)

```c++
#include<iostream>
#include<algorithm>
#include<string>
using namespace std;

bool cmp(string a,string b)
{
    return a+b>b+a; //妙中之妙！
    /*如果这样写：
bool cmp（string a，string b）{
    return a>b;
    会发生321>32的情况，具体原因是字符串自己的关系运算是这样设定的 
}*/
}

int main()
{
    int n;
    cin>>n;
    string a[25];
    for(int i=0;i<n;i++){
        cin>>a[i];
    }
    sort(a,a+n,cmp);
    for(int i=0;i<n;i++){
        cout<<a[i];
    }
    return 0;
}
```



### P5738 ![image-20211008170617559](C:\Users\DFlyoung\AppData\Roaming\Typora\typora-user-images\image-20211008170617559.png)

```c++
#include<iostream>
#include<algorithm>
using namespace std;

int a[25];
double b[105];

int main()
{
    int n,m;
    double sum=0,ans=0;
    cin>>n>>m;
    for(int i=0;i<n;i++){
        sum=0; //非常重要，每换一名选手，都应将sum的值归零，不然会继承上一次的sum值
        for(int j=0;j<m;j++){
            cin>>a[j];
            sum+=a[j];
        }
        sort(a,a+m);
        sum=sum-a[0]-a[m-1];
        b[i]=sum/(m-2);
    }
    sort(b,b+n);
    ans=b[n-1];
    printf("%.2lf",ans);
    return 0;
}
```



### P3613  //对map容器的应用![image-20211016230033999](C:\Users\DFlyoung\AppData\Roaming\Typora\typora-user-images\image-20211016230033999.png)

```c++
#include<iostream>
#include<map>
using namespace std;

int n,q,x,y,flag,k;

map<int,map<int,int>>a;

int main()
{
    scanf("%d%d",&n,&q);
    for(int i=0;i<q;i++){
        scanf("%d%d%d",&flag,&x,&y);
        if(flag==1){
            scanf("%d",&a[x][y]);
        }
        else{
            printf("%d\n",a[x][y]);
        }
    }
    return 0;
}
```

### P1449

```c++
#include<bits/stdc++.h>
using namespace std;

stack<int>p;
string s;

int main()
{
    cin>>s;
    int i=0,j=0;
    int a=0,b=0;
    for(int k=0;k<s.length();k++){
        if(s[k]=='@') break;
        else if(s[k]=='.'){
            p.push(a);
            a=b=0;
        }
        else if(s[k]>='0'&&s[k]<='9'){
            a=b*10+s[k]-'0';
            b=a;
        }
        else{
            if(s[k]=='+'){i=p.top();p.pop();j=p.top();p.pop();p.push(i+j);}
            if(s[k]=='-'){i=p.top();p.pop();j=p.top();p.pop();p.push(j-i);}
            if(s[k]=='*'){i=p.top();p.pop();j=p.top();p.pop();p.push(i*j);}
            if(s[k]=='/'){i=p.top();p.pop();j=p.top();p.pop();p.push(j/i);}
        }
    }
    cout<<p.top()<<endl;
    return 0;
}
```

### P1996（队列应用）

```c++
#include<bits/stdc++.h>
using namespace std;

queue<int>q;

int main()
{
    int n,m;
    int now=1;
    cin>>n>>m;
    for(int i=1;i<=n;i++) q.push(i);
    while(!q.empty()){
        if(now==m){
            cout<<q.front()<<" ";
            q.pop();
            now=1;
        }else{
            q.push(q.front());
            now++;
            q.pop();
        }
    }
    return 0;
}
```

```c++
//P1
#include<bits/stdc++.h>
using namespace std;

bool vis[1005];
queue<int>dic;

int main()
{
    int m,n,count=0;
    scanf("%d%d",&m,&n);
    for(int i=1;i<=n;i++){
        int x;
        cin>>x;
        if(vis[x]) continue;
        else{
            if(dic.size()>=m){
                vis[dic.front()]=0;
                dic.pop();
            }
            dic.push(x);
            vis[x]=true;
            count++;
        }
    }
    cout<<count;
    return 0;
}
```



### p1160（STL中list容器的应用）

```c++
#include<bits/stdc++.h>
using namespace std;
using Iter =list<int>::iterator;
list<int>q;
Iter pos[100005];
bool erased[100005]={0};

int main()
{
    int n,k,p,m,t;
    q.push_front(1);
    pos[1]=q.begin();
    scanf("%d",&n);
    for(int i=2;i<=n;i++){
        scanf("%d%d",&k,&p);
            if(p==0){   //左插
                pos[i]=q.insert(pos[k],i);
            }
            else{       //右插
                pos[i]=q.insert(next(pos[k]),i);
            }
    }
    scanf("%d",&m);
    for(int i=1;i<=m;i++){
        scanf("%d",&t);
        
        if(!erased[t])  q.erase(pos[t]);
        erased[t]=true;
    }
    for (int x : q)
    {
        printf("%d ", x);
    }
    return 0;
}
```

### 01背包问题

```c++
//P1060
#include<iostream>
#include<cmath>
using namespace std;

int v[30];
int w[30];
long long dp[30005];

int main()
{
	int n,m;
    cin>>n>>m;
    for(int i=0;i<m;i++){
        cin>>v[i]>>w[i];
    }
    for(int i=0;i<m;i++){
        for(int j=n;j>v[i];j--){
            dp[j]=max(dp[j],dp[j-v[i]]+w[i]*v[i]);
        }
    }
    cout<<dp[n]<<endl;
    return 0;
}
```

```c++
//P1
#include<iostream>
#include<cmath>
using namespace std;

int dp[2005][2005];
int mat[2005][2005];
int n,m;
int main()
{
    cin>>n>>m;
    for(int i=1;i<=m;i++){
        for(int j=1;j<=n;j++){
            scanf("%d",&mat[j][i]);
        }
    }
    for(int i=1;i<=n;i++){
        dp[i-1][0]=dp[i-1][m];
        for(int j=1;j<=m;j++){
            dp[i][j]=min(dp[i-1][j-1],dp[i-1][j])+mat[i][j];
        }
    }
    int ans=1e8;
    for(int i=1;i<=m;i++){
        ans=min(ans,dp[n][i]);
    }
    cout<<ans<<endl;
    return 0;
}
```

```c++
//二维01背包问题
#include<iostream>
#include<cmath>
using namespace std;

int v[55],m[55],c[55];
int dp[500][500];
int main()
{
    int V,M,n;
    cin>>V>>M;
    cin>>n;
    for(int i=0;i<n;i++)
        cin>>v[i]>>m[i]>>c[i];
    for(int i=0;i<n;i++){
        for(int j=V;j>=v[i];j--){
            for(int k=M;k>=m[i];k--){
                dp[j][k]=max(dp[j][k],dp[j-v[i]][k-m[i]]+c[i]);
            }
        }
    }
    cout<<dp[V][M]<<endl;
    return 0;
}
```

#### 完全背包问题

```c++
#include<iostream>
#include<cstring>
using namespace std;

bool prime[1005];
long long dp[1005];
int a[1005];
int getprime(int n)
{
    memset(prime,1,sizeof(prime));
    prime[0]=prime[1]=false;
    for(int i=2;i<=n;i++){
        for(int j=2*i;j<=n;j+=i){
            prime[j]=false;
        }
    }
    int sum=0;
    int k=0;
    for(int i=2;i<=n;i++){
        if(prime[i]){
            a[k++]=i;
            sum++;
        }
    }
    return sum;
}

int main()
{
    int n,pnum;
    cin>>n;
    pnum=getprime(n);
    dp[0]=1;
    for(int i=0;i<pnum;i++){
        for(int j=a[i];j<=n;j++){
            dp[j]+=dp[j-a[i]];
        }
    }
    cout<<dp[n];
    return 0;
}
```

