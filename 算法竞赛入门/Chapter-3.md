#  Chapter-3：数组和字符串

## 3-1 数组

```
读入一些整数，逆序输出到一行中。已知整数不超过100个。
```

我的代码：（写死了输入的个数。。。

```c
#include <stdio.h>

int main()
{
    int a[101];
    for(int i=1;i<=100;i++)
    {
        scanf("%d",&a[i]);
    }
    for(int j=100;j>=1;j--)
    {
        printf("%d",a[j]);
    }
}
```

书中给出代码：

```c
#include <stdio.h>
#define maxn 105
int a[maxn];

int main()
{
    int x,n=0;
    while (scanf("%d",&x) == 1)
        a[n++] = x;
    for(int i = n-1;i >=1;i--)
        printf("%d",a[i]);
    printf("%d\n"),a[0];
    return 0;
}
```

### 开灯问题

```
有n盏灯，编号为1~n。第一个人把所有灯打开，第二个人把所有编号为2的倍数的关了，第三个人把按下所有编号为3的倍数的开关，依此类推。一共有k个人，问最后哪些灯开着？输入n和k，输出开着的灯的编号。k<=n<=1000。
样例输入：
7 3
样例输出：
1 5 6 7
```

我的代码：

```c
#include <stdio.h>
#define maxn 1001
int a[maxn];

int main()
{
    int n,k,i,j,m;
    scanf("%d%d",&n,&k);
    for(i=1;i<=n;i++)
    {
        a[i] =0;
    }
    for(i=1;i<=k;i++)
    {
        m = n/i;
        for(j=1;j<=m;j++)
        {
            if(a[j*i] == 0)
                a[j*i] = 1;
            else
                a[j*i] = 0;
        }
    }
    for(i=1;i<=n;i++)
    {
        if(a[i]==1)
            printf("%d ",i);
    }
}
```

书中代码：

```c
#include <stdio.h>
#include <string.h>
#define maxn 1010
int a[maxn];

int main()
{
    int n,k,first=1;
    memset(a,0, sizeof(a));
    scanf("%d%d",&n,&k);
    for(int i =1;i<=k;i++)
    {
        for(int j=1;j<=n;j++)
            if(j % i ==0) a[j] = !a[j];
    }
    for(int i=1;i<=n;i++)
    {
        if(a[i]) {
            if (first) first = 0;
            else printf(" ");
            printf("%d", i);
        }
    }
    printf("\n");
    return 0;
}
```

### 蛇形填数

```
在n×n方阵里填入1，2，…,n×n，要求填成蛇形。例如，n=4方阵为：
10 11 12 1
9  16 13 2
8  15 14 3
7   6  5 4
多余的空格只是为了便于观察规律，不必严格输出。n<=8。
```

我的代码：(和书上一比，弱爆了。

```c
#include <stdio.h>
#include <string.h>
#include <math.h>

int main()
{
    int a[9][9];
    int n;
    memset(a,0, sizeof(a));
    scanf("%d",&n);
    a[n+1][n] = -1; //下
    a[n][0] = -1;
    a[0][n+1] = -1;
    a[0][1] = -1;
    int b = 1;//b代表圈数
    for(int i=1;i<=pow(n,2);i++)//将问题分析成蛇形走势的四个方向
    {
        int c = 0;//用于定位。
        int d;
        if(b%4==1)//下
        {
            c = b/4;
            for(d=1;d<=n;d++){
                if(a[d][n-c]==0)
                {
                    break;
                }
            }
            a[d][n-c] = i;
            if(a[d+1][n-c] != 0)
            {
                b++;
                printf("_");
            }
        }
        else if(b%4==2)//左
        {
            c = b/4;
            for(d=n;d>=1;d--){
                if(a[n-c][d]==0)
                {
                    break;
                }
            }
            a[n-c][d] = i;
            if(a[n-c][d-1] !=0)
            {
                b++;
            }
        }
        else if(b%4==3)//上
        {
            c = b/4;
            for(d=n;d>=1;d--){
                if(a[d][1+c]==0)
                {
                    break;
                }
            }
            a[d][1+c] = i;
            if(a[d-1][1+c]!=0)
            {
                b++;
            }
        }
        else if(b%4==0)//右
        {
            c = b/4;
            for(d=1;d<=n;d++){
                if(a[c][d]==0)
                {
                    break;
                }
            }
            a[c][d] = i;
            if(a[c][d+1]!=0)
            {
                b++;
            }
        }
    }
    for(int j=1;j<=n;j++)//输出。
    {
        printf("\n");
        for(int m=1;m<=n;m++)
        {
            printf("%3d ",a[j][m]);
        }
    }
}
```

书中代码：

```c
#include <stdio.h>
#include <string.h>
#define maxn 20
int a[maxn][maxn];

int main()
{
    int n,x,y,tot=0;
    memset(a,0, sizeof(a));
    scanf("%d",&n);
    tot = a[x=0][y=n-1] = 1;
    while (tot <n*n)
    {
        while (x+1<n && !a[x+1][y]) a[++x][y] = ++tot;
        while (y-1>=0 && !a[x][y-1]) a[x][--y] = ++tot;
        while (x-1>=0 && !a[x-1][y]) a[--x][y] = ++tot;
        while (y+1<n && !a[x][y+1]) a[x][++y] = ++tot;
    }
    for(int j=0;j<=n-1;j++)
    {
        printf("\n");
        for(int m=0;m<=n-1;m++)
        {
            printf("%3d",a[j][m]);
        }
    }
}
```

## 3-2字符数组

### 竖式问题

```
找出所有形如abc*de（三位数乘以两位数）的算式，使得在完整的竖式中，所有数字都属于一个特定的数字集合。输入数字集合（相邻数字之间没有空格），输出所有竖式。每个竖式前应有编号，之后应有一个空行。最后输出解的总数。（为了便于观察，竖式中的空格改用小数点表示，但所写程序中应该输出空格，而非小数点）。
样例输入：
2357
样例输出：
<1>
..775
×..33
------
.2325
2325.
------
25575

The number of solutions = 1
```



我的代码：

```
#include <stdio.h>
#include <string.h>

int main()
{
    int i,j,o,k,m,n;
    int is,what;
    char a[10];
    char b[20];
    i = 0;
    what = 0;
    scanf("%s",a);
    for(i=100;i<=999;i++)
    {
        for(int j=10;j<=99;j++)
        {
            is = 1;
            k = j * i;
            m = (j % 10) * i;
            n = (j / 10) * i;
            sprintf(b,"%d%d%d%d%d",i,j,m,n,k);
            for(o=0;o<strlen(a);o++)
            {
                if(strchr(b,a[i]) == NULL) is = 0;
            }
            if(is)
            {
                printf("<%d>\n",++what);
                printf("%5d\n×%4d\n-----\n%5d\n%4d\n-----\n%5d\n\n",i,j,m,n,k);
            }
        }
    }
}
```

