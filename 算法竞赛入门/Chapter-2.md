# Chapter-2：循环结构程序设计

## 2-1 for循环

```c
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);
    for(int i = 1;i<=n;i++)
    {
        printf("%d\n",i);
    }
    return 0;
}
```

### 例题2-1 aabb

```
输出所有形如aabb的4位完全平方数（即前两位数字相等，后两位数字也相等）。
```

我的代码：

```c
#include <stdio.h>
#include <math.h>

int main()
{
    int a;
    for(int i=1;i<=9;i++)
    {
        for(int j=0;j<=9;j++)
        {
            a = i * 1100 + j * 11;
            if((sqrt(a)) == int(sqrt(a)))
                printf("%d",a);
        }
    }
}

```

书中给出代码：(floor(x)函数返回不超过x的最大整数。)

```c
#include <stdio.h>
#include <math.h>

int main()
{
    int a;
    for(int i=1;i<=9;i++)
    {
        for(int j=0;j<=9;j++)
        {
            a = i * 1100 + j * 11;
            int b = floor(sqrt(a) + 0.5);
            if(b * b == a)
                printf("%d\n",a);
        }
    }
    return 0;
}
```

还给了这样的：

```c
#include <stdio.h>
#include <math.h>

int main()
{
    for (int x=1;;x++)
    {
        int n = x * x;
        if (n<1000) continue;
        if(n>9999) break;
        int hi = n/100;
        int lo = n%100;
        if(hi/10 == hi%10 && lo/10 == lo%10) printf("%d\n",n);
    }
    return 0;
}
```

## 2-2 while循环和do-while循环

### 例题2-2 3n+1问题

```
对于任意大于1的自然数n，若n为奇数，则将n变为3n+1，否则变为n的一半。经过若干次这样的变换，一定会使n变为1。例如：3->10->5->16->8->4->2->1。
输入n,输出变换的次数。n<=10^9。
样例输入：
3
样例输出：
7
```

我的代码：(未考虑题目给出n值大小对运行的影响，同样出现乘法溢出问题。)

```c
#include <stdio.h>
#include <math.h>

int main()
{
    int n;
    scanf("%d",&n);
    int i = 0;
    while(n!=1)
    {
        if(n % 2 ==1)
            n = 3 * n + 1;
        else
            n = n/2;
        i++;
    }
    printf("%d",i);
}
```

书中给出代码：(有bug，当输入为987654321时，乘法溢出，出现负数了。)

```c
#include <stdio.h>
#include <math.h>

int main()
{
    int n,count=0;
    scanf("%d",&n);
    while(n>1)
    {
        if(n % 2 ==1)
            n = 3 * n + 1;
        else
            n = n/2;
        count++;
    }
    printf("%d\n",count);
    return 0;
}
```

书中给出改进代码：

```c
#include <stdio.h>
#include <math.h>

int main()
{
    int n2,count=0;
    scanf("%d",&n2);
    long long n = n2;
    while(n>1)
    {
        if(n % 2 ==1)
            n = 3 * n + 1;
        else
            n = n/2;
        count++;
    }
    printf("%d\n",count);
    return 0;
}
```

### 例题2-3 近似计算

```
计算pi/4 = 1-1/3+1/5-1/7+…,直到最小一项小于10^(-6)。
```

我的代码：

```c
#include <stdio.h>
#include <math.h>

int main()
{
    int i = 1;
    int a = 0;
    float sum = 0.0;
    float b;
    while (1)
    {
        b = 1.0/i;
        printf("%.7f\n",b);
        if (b<pow(10,-6)) break;
        sum = sum + b * pow(-1,a);
        i = i + 2;
        a = a + 1;
    }
    printf("%.7f",sum);
    return 0;
}
```

书中给出代码：

```c
#include <stdio.h>

int main()
{
    double sum = 0;
    for(int i = 0; ;i++)
    {
        double term = 1.0/(i*2+1);
        if(i % 2==0) sum += term;
        else sum -= term;
        if(term< 1e-6) break;
    }
    printf("%.6f\n",sum);
    return 0;
}
```

## 2-3 循环的代价

### 例题2-4 阶乘之和

```
输入n，计算S=1！+2！+3！+……+n!的末6位（不含前导0）。n<=10^6,n!表示前n个正整数之积。
样例输入：
10
样例输出：
37913
```

我的代码：

```c
#include <stdio.h>

int main()
{
    int n,m = 1;
    long long s = 0;
    scanf("%d",&n);
    for(int i=1;i<=n;i++)
    {
        m = m * i;
        s = s + m;
        printf("%d\n",s);
    }
    printf("%d",s % 1000000);
    return 0;
}
```

书中给出代码为

```c
#include <stdio.h>

int main()
{
    int n,s = 0;
    scanf("%d",&n);
    for(int i = 1;i<=n;i++)
    {
        int factorial = 1;
        for(int j = 1;j<=i;j++)
        {
            factorial *= j;
        }
        s += factorial;
    }
    printf("%d\n",s % 1000000);
    return 0;
}
```

此外。介绍了time.h和clock()函数获得程序运行时间。



## 2-4 算法竞赛中的输入输出框架

例题2-5 数据统计

```
输入一些整数，求出它们的最小值、最大值和平均数（保留3位小数）。输入保证这些都是不超过1000的整数。
样例输入：
2 8 3 5 1 7 3 6
样例输出：
1 8 4.375
```

我的代码为：（用冒泡法排序。

```c
#include <stdio.h>
#include <time.h>

int main()
{
    int a[8],sum,m;
    float avg;
    sum = 0;
    for(int i=0;i<=7;i++)
    {
        scanf("%d",&a[i]);
        sum = sum + a[i];
        printf("%d\n",sum);
    }
    avg = sum/8.0;
    for(int j=0;j<=7;j++)
    {
        for (int k = 0;k <= 7-j ; j++) {
            if(a[k] >a[k+1])
            {m = a[k];
            a[k] = a[k+1];
            a[k+1] = m;}
        }
    }
    printf("%d %d %.3f",a[0],a[7],avg);
}
```

书中给出的:(有bug)

```c
#include <stdio.h>

int main() {
    int x, n = 0, min, max, s = 0;
    while (scanf("%d", &x) == 1){
        s += x;
        if(x<min) min =x;
        if(x>max) max =x;
        n++;
    }
    printf("%d %d %.3f",min,max,(double)s/n);
    return 0;
}
```

## 习题相关

### 习题2-1 水仙花数

```
输出100~999中的所有水仙花数。若3位数ABC满足ABC=A^3+B^3+C^3,则称其为水仙花数。例如153 = 1^3+5^3+3^3，所以153是水仙花数。
```

我的代码；

```c
#include <stdio.h>
#include <math.h>

int main() {
    int a,b,c;
    for(a=1;a<=9;a++)
    {
        for(b=0;b<=9;b++){
            for(c=0;c<=9;c++){
                if(a*100 + b*10 + c == pow(a,3)+pow(b,3)+pow(c,3))
                    printf("%d%d%d\n",a,b,c);
            }
        }
    }
}
```

### 习题2-2 韩信点兵

```
输入包含多组数据，每组数据包含3个非负整数a,b,c，表示每种队形排尾的人数（a<3,b<5,c<7)，输出总人数的最小值（或报告无解）。已知总人数不少于10，不超过100。输入文件结束为止。
样例输入：
2 1 6
2 1 3
样例输出：
Case 1:41
Case 2:No answer
```

我的代码：

```c
#include <stdio.h>
#include <math.h>

int main() {
    int a,b,c,d;
    scanf("%d%d%d",&a,&b,&c);
    d = 0;
    for(int i = 10;i<=100;i++)
    {
        if(i%3==a&&i%5==b&&i%7==c)
        {
            printf("%d",i);
            d++;
        }
    }
    if(d==0)
    {
        printf("No answer");
    }
}
```

### 习题2-3 倒三角形

```
输入正整数n<=20,输出一个n层的倒三角形。例如，n=5时输出如下：
#########
 #######
  #####
   ###
    #
```

我的代码：

```c
#include <stdio.h>

int main() {
    int n;
    scanf("%d",&n);
    for(int i=n-1;i>=0;i--)
    {
        int h;
        h = i * 2 + 1;
        for(int j=1;j<=h;j++)
        {
            printf("#");
        }
        printf("\n");
        for(int m=-1;m<n-i-1;m++)
        {
            printf(" ");
        }
    }
}
```

### 习题2-4 子序列的和

```
输入两个正整数n<m<10^6,输出1/n^2+1/(n+1)^2+…+1/(m^2),保留5位小数。输入包含多组数据，结束标记为n=m=0。提示：本题有陷阱。
样例输入：
2 4
65536 655360
0 0
样例输出：
Case 1:0.42361
Case 2:0.00001
```

我的代码：

```c
#include <stdio.h>
#include <math.h>

int main() {
    int n,m;
    float sum,a;
    sum =0.0;
    scanf("%d%d",&n,&m);
    for (int i=n;i<=m;i++)
    {
        a = 1.0/i;
        sum = sum + pow(a,2);
    }
    printf("%.5f",sum);
}
```

### 习题2-5 分数化小数

```
输入正整数a,b,c，输出a/b的小数形式，精确到小数点后c位。a,b<=10^6,c<=100.输入包含多组数据，结束标记为a=b=c=0。
样例输入：
1 6 4
0 0 0
样例输出：
Case 1:0.1667
```

我的代码： 

```c
#include <stdio.h>
#include <math.h>

int main() {
    while (1){
        int a,b,h,e;
        double d;
        scanf("%d%d%d",&a,&b,&h);
        if(a==0&&b==0&&h==0)
        {
            break;
        }
        d = a*1.0/b;
        e = (int)(d * pow(10,h) +0.5);
        printf("0.%d",e);

    }
}
```

### 习题2-6 排序

```
用1，2，3，…，9组成3个三位数abc,def和ghi，每个数字恰好使用一次，要求abc:def:ghi=1：2：3。按照“abc def ghi”的格式输出所有解，每行一个解。提示：不必太动脑筋。
```

我的代码：(关键9个数和不变，乘积不变。)

```c
#include <stdio.h>

void result(int num, int &add, int &mul);
int main()
{
    int i, j, k;
    int add, mul;
    for(i = 123; i <330; i++)
    {
        j = i * 2;
        k = i * 3;
        add = 0;
        mul = 1;
        result(i, add, mul);
        result(j, add, mul);
        result(k, add, mul);
        if(add == 45 && mul == 362880)
            printf("%d %d %d\n", i, j, k);
    }
    return 0;
}
void result(int num, int &add, int &mul)
{
    int bai,shi,ge;
    bai = num / 100;
    shi = num / 10 % 10;
    ge = num % 10;
    add = add + bai + shi + ge;
    mul = mul * bai * shi * ge;
}
```



