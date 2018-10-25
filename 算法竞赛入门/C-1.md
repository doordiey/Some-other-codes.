# Chapter-1：程序设计入门

## 1-1：

```c
#include <stdio.h>

int main() {
    printf("%d",1+2);
    return 0;
}
```

### 相关实验简单略过。

## 1-2

```c
#include <stdio.h>

int main() {
    printf("%.1f",8.0/5.0);
    return 0;
}
```

### 相关实验简单略过。

## 1-3

```c
#include <stdio.h>
#include <math.h>

int main()
{
    printf(".8%f\n",1+2*sqrt(3)/(5-0.1));
    return 0;
}
```

### 相关实验简单略过。

## 1-4

```c
#include <stdio.h>

int main()
{
    int a,b;
    scanf("%d%d",&a,&b);
    printf("%d\n",a+b);
    return 0;
}
```

### 相关实验简单略过。

## 例题1-1 圆柱体的表面积

```
样例输入：
3.5 9
样例输出：
Area = 274.889 
```

我的代码：

```c
#include <stdio.h>
#include <math.h>

int main()
{
    float a,b,Area;
    const double pi = acos(-1.0);
    scanf("%f%f",&a,&b);
    Area = 2*pi*a*a+2*pi*a*b; 
    printf("Area=%.3f",Area);
    return 0;
}
```

## 例题1-2 三位数反转

```
样例输入：
127
样例输出：
721
```

我的代码：

```c
#include <stdio.h>

int main()
{
    int a,b,c,d,e,h;
    scanf("%d",&a);
    b = a%100;
    c = a/100;
    d = b/10;
    e = b%10;
    h = e * 100 + d * 10 + c;
    printf("%d",h);
    return 0;
}
```

书中给出解决代码为：

```c
#include <stdio.h>

int main()
{
    int n;
    scanf("%d",&n);
    printf("%d%d%d\n",n%10,n/10%10,n/100);
    return 0;
}
```

考虑问题存在漏洞，当输入为520时应输出25还是025问题。上述书中代码结果为025，我的代码为25.书中对于输出为25的代码也有给出。

```c
#include <stdio.h>

int main()
{
    int n,m;
    scanf("%d",&n);
    m = (n%10)*100 + （n/10%10)*10 + (n/100);
    printf("%03d\n",m);
    return 0;
}
```

此处%03d表示输出三位整数不足用0补全。

## 例题1-3 交换变量

```
输入两个整数a和b，交换二者的值，然后输出。
样例输入：
824 16
样例输出：
16 824
```

我的代码：

```c
#include <stdio.h>

int main()
{
    int a,b;
    scanf("%d%d",&a,&b);
    a = a + b ;
    b = a - b ;
    a = a - b ;
    printf("%d %d",a,b);
}
```

书中给出代码（三变量法）：便于理解

```c
#include <stdio.h>

int main()
{
    int a,b,c;
    scanf("%d%d",&a,&b);
    c = a ;
    a = b ;
    b = c ;
    printf("%d %d",a,b);
}
```

还有一种更简单的方法（只考虑效果）：

```c
#include <stdio.h>

int main()
{
    int a,b,c;
    scanf("%d%d",&a,&b);
    printf("%d %d",b,a);
}
```

## 例题1-4 鸡兔同笼问题

```
已知鸡和兔的总数量为n，总腿数为m，输入n和m，依次输出鸡的数目和兔的数目，如果无解，则输出No answer.
样例输入：
14 32
样例输出：
12 2
样例输入：
10 16
样例输出：
No answer
```

我的代码：

```c
#include <stdio.h>

int main()
{
    int a,b,n,m,i;
    scanf("%d%d",&n,&m);
    i = m - n * 2;
    if((i/2)>n||(i/2)<0)
    {
        printf("No answer");
    }
    else
    {
        b = i / 2;
        a = n - b;
        printf("%d %d",a,b);
    }
}
```

书中给出代码：

```c
#include <stdio.h>

int main()
{
    int a,b,n,m;
    scanf("%d%d",&n,&m);
    a = (4*n-m)/2;
    b = n - a ;
    if(m%2 == 1 || a < 0 || b < 0)
        printf("No answer");
    else
        printf("%d %d",a,b);
    return 0;
}
```

## 例题1-5 三整数排序

``` 
输入3个整数，从小到大排序后输出。
样例输入：
20 7 33
样例输出：
7 20 33
```

我的代码:(可能性全部列出来了，if一把梭。)

```c
#include <stdio.h>

int main()
{
    int a,b,c;
    scanf("%d%d%d",&a,&b,&c);
    if(a<b&&a<c&&b<c) printf("%d %d %d",a,b,c);
    if(a<b&&a<c&&b>c) printf("%d %d %d",a,c,b);
    if(b<a&&b<c&&a<c) printf("%d %d %d",b,a,c);
    if(b<a&&b<c&&c<a) printf("%d %d %d",b,c,a);
    if(c<a&&c<b&&b<a) printf("%d %d %d",c,b,a);
    if(c<a&&c<b&&a<b) printf("%d %d %d",c,a,b);
}
```

书中给出代码：（也给了我写了那个方法。

```c
#include <stdio.h>

int main()
{
    int a,b,c,t;
    scanf("%d%d%d",&a,&b,&c);
    if(a>b){t=a;a=b;b=t;}
    if(a>c){t=a;a=c;c=t;}
    if(b>c){t=b;b=c;c=t;}
    printf("%d %d %d",a,b,c);
    return 0;
}
```

## 习题：

### 1-1 平均数

```
输入三个整数，输出它们的平均数，保留3位小数。
```

我的代码：

```c
#include <stdio.h>

int main()
{
    int a,b,c;
    float t;
    scanf("%d %d %d",&a,&b,&c);
    t = (a + b + c)/3.0;
    printf("%.3f",t);
}
```

### 1-2 温度

```
输入华氏温度f，输出对应的摄氏温度c，保留3位小数。
```

我的代码：

```c
#include <stdio.h>

int main()
{
    int f;
    float c;
    scanf("%d",&f);
    c = 5 * (f - 32)/9.0;
    printf("%.3f",c);
}
```

### 1-3 连续和

```
输入正整数n，输出1+2+…+n的值。
```

我的代码：

```c
#include <stdio.h>

int main()
{
    int a,b;
    scanf("%d",&a);
    b = ((1 + a) * a)/2;
    printf("%d",b);
}
```

### 1-4 正弦和余弦

```
输入正整数n(n<360),输出n度的正弦、余弦函数值。
```

我的代码：

```c
#include <stdio.h>
#include <math.h>

#define Pi 3.1415

int main()
{
    int n;
    double n1,sin1,cos1;
    scanf("%d",&n);
    n1 = (n/180.0)*Pi;
    sin1 = sin(n1);
    cos1 = cos(n1);
    printf("%.4f\n",sin1);
    printf("%.4f\n",cos1);
}
```

### 1-5 打折

```
一件衣服95元，若消费满300元，可打八五折。输入购买衣服件数，输出需要支付的金额,保留两位小数。
```

我的代码：

```c
#include <stdio.h>

int main()
{
    int a,b;
    float c;
    scanf("%d",&a);
    b = a * 95;
    if(b >= 300)
        c = b * 0.85;
    else
        c = b;
    printf("%.2f",c);
}
```

### 1-6 三角形

```
输入三角形三条边的长度值（均为正整数），判断是否能为直角三角形的3个边长。如果可以。则输出yes,如果不能，则输出no。如果根本无法构成三角形，则输出not a triangle.
```

我的代码：

```c
#include <stdio.h>

int main()
{
    int a,b,c,t;
    scanf("%d%d%d",&a,&b,&c);
    if(a>b){t=a;a=b;b=t;}
    if(a>c){t=a;a=c;c=t;}
    if(b>c){t=b;b=c;c=t;}
    if(a + b <= c||c - a >= b)
        printf("not a triangle");
    else
    {
        if(a*a + b*b == c*c)
            printf("yes");
        else
            printf("no");
    }
}
```

### 1-7 年份

```
输入年份，判断是否为闰年，如果是，则输出yes,否则输出no.
```

我的代码：

```c
#include <stdio.h>

int main()
{
    int year;
    scanf("%d",&year);
    if(year % 4 == 0&&year % 100 !=0)
    {
        printf("yes");
    } else
    {
        printf("no");
    }
}
```



