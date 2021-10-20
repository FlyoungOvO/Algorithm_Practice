BFS
CF96B
```C++
#include<iostream>
using namespace std;

bool check(long long x)
{
    int a=0,b=0;
    while(x){
        if(x%10==4)
            a++;
        else
            b++;
        x/=10;
    }
    return a==b;
}

long long q[100010],head,tail,n;

int main()
{
    cin>>n;
    tail=1;
    q[tail]=0;
    while(head<tail){
        long long t=q[head++];
        if(t>=n&&check(t)){
            cout<<t<<endl;
            return 0;
        }
        q[tail++]=t*10+4;
        q[tail++]=t*10+7;
    }
    return 0;
}
```
