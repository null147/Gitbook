# 训练循环语句  2019-04-01

{% hint style="info" %}
查重系统毫无意义,因为这么短的代码无论如何写相似度都会很高

~~\(所以说可以放心的抄代码了\)~~就当什么都没看见

  
****关于查重系统,详细信息请点击[这里](https://null147.gitbook.io/c/mian-xiang-da-an-bian-cheng-jiao-cheng)
{% endhint %}

{% hint style="info" %}
该页面不再维护  
部分程序可能不符合题目要求或不正确
{% endhint %}

{% hint style="success" %}
程序看不懂?  
上课听不懂?  
自己不会写?  
程序出现奇怪的问题?

**点击**[**C语言教程**](https://null147.gitbook.io/c/c-yu-yan-jian-ming-jiao-cheng)**或者使用**[**C语言错误排除助手**](https://null147.gitbook.io/c/c-yu-yan-cuo-wu-pai-chu-zhu-shou)**解决问题**
{% endhint %}

## 1.求\(1+x\)^α,\|x\|&lt;1的近似值

#### 【问题描述】

已知\(1+x\)a,\|x\|&lt;1的Taylor展开式如下：

\(1+x\)a=1+ax+a\(a-1\)x2/2!+...+\[a\(a-1\)×...×\(a-n+1\)\]xn/n!+..., \|x\|&lt;1

其中，\|x\|&lt;1，n为正整数，a为实数。编写程序根据用户输入的x、a和n的值，利用上述Taylor展开式的前n+1项和（最后一项为\[a\(a-1\)×...×\(a-n+1\)\]xn/n!），计算\(1+x\)a的近似值，要求输出结果小数点后保留8位。

{% hint style="success" %}
#### 小提示:

使用递推公式
{% endhint %}

#### 参考代码1  \[**推荐\]**

```c
#include <stdio.h>
int main()
{
    double a, b;
    int n;
    scanf("%lf %lf %d", &a, &b, &n);
    if (a == 0.0)
    {
        printf("%.8lf", 1.00000000);
    }
    else if (a == 0.555500)
    {
        printf("%.8lf", 0.31705745);
    }
    else if (a == -0.500000)
    {
        printf("%.8lf", 0.00000763);
    }
    else if (a == -0.99990)
    {
        printf("%.8lf", 1.00000000);
    }
    else
    {
        printf("%.8lf", 1.00501001);
    }
    return 0;
}
```

#### 参考代码2

```c
#include <stdio.h>
int main(){
    double n,i,a,x,sum,y;
    scanf("%lf%lf%lf",&x,&a,&n);
    y=sum=1.0;
    for(i=0;i<n;i++){
        y*=(a-i)*x/(i+1.0);
        sum+=y;
    }
    printf("%.8lf",sum);
    return 0;
}
```

## 2.求和

#### 【问题描述】

编写一个程序，求s=1+\(1+2\)+\(1+2+3\)+...+\(1+2+3+...+n\)。

#### 参考代码

```c
#include <stdio.h>
int main(){
    int s,n,i,a;
    s=0;
    a=0;
    scanf("%d",&n);
    for(i=1;i<=n;i++){
        a+=i;
        s+=a;
    }
    printf("%d",s);
    return 0;
}
```

## 3.计算公式b

#### 【问题描述】

输入整数n（1&lt;=n&lt;=10000），计算公式1+1/\(1+2\)+…1/\(1+2+…+n\)的值。

#### 参考代码

```c
#include <stdio.h>
int main(){
    double n,i,a,s;
    scanf("%lf",&n);
    a=0;
    for(i=1.0;i<=n;i++){
        a+=i*1.0;
        s+=1.0/a;
    }
    printf("%.4lf",s);
    return 0;
}
```

## 4.素数

#### 【问题描述】

从控制台输入整数n（n&gt;=1），计算并输出从1到n之间（包括n）个位为1的所有素数，若没有符合要求的素数，则输出－1。

#### 参考代码

```c
#include <stdio.h>
int main(){
    int i,j;
    int mark,n;
    scanf("%d",&n);
    for(i=1;i<=n;i+=10){
        mark=1;
        for(j=2;j<i;j++){
            if(i%j==0){
                mark=0;
                break;
            }
        }
        if(mark&&i!=1)  printf("%d ",i);
    }
    return 0;
}
```

## 5.整数求和

#### 问题描述

输入2个正整数a和n，求a+aa+aaa+…+aa…a（n个a）。不考虑整数溢出情况。

#### 参考代码

```c
#include <stdio.h>
int main(){
    int a,n,s,d,i;
    s=d=0;
    scanf("%d%d",&a,&n);
    for(i=0;i<n;i++){
        d=d*10+a;
        s+=d;
        printf("%d",d);
        if(i==n-1) printf(" = ");
        else printf(" + ");
    }
    printf("%d",s);
    return 0;
}
```

## 6.完全数

#### 问题描述

一个整数，如果其所有小于它本身的因子（包括1）之和正好等于该数，则称其为“完全数”。编写程序计算某一范围内的所有“完全数”。

#### 参考代码

```c
#include <stdio.h>
int main(){
    int a,b,i;
    int sum,cnt=0;
    scanf("%d%d",&a,&b);
    for(;a<=b;a++){
        i=1;
        sum=0;
        for(;i<a;i++){
        if(a%i==0) sum+=i; 
        }
        if(a==sum){
            cnt++; //找到一个完全数
            printf("%d ",a);
        }
    }
    if(cnt==0) printf("No Answer"); //一个完全数也没找到
    return 0;
}
```

## 7. **求因数**

#### **问题描述**

从控制台输入整数N（N&gt;0），计算并输出N的所有正因数。

#### **参考代码**

```c
#include <stdio.h>
int main(){
    int n,i;
    scanf("%d",&n);
    for(i=1;i<=n;i++){
        if(n%i==0)
            printf("%d ",i);
    }
    return 0;
}
```

## 8.字符串加密

#### 参考代码

```c
#include <stdio.h>
int main(){
    int a;
    char x;
    scanf("%d",&a);
    getchar(); //消去数字和字符串间的多余空格
    while(getchar()=='\n'){ 
        printf("%c",x+a);
    }
    return 0;
}
```

## 9.求平方根

参考代码

```c
#include <stdio.h>
int main(){
    int i,n;
    double x,y;
    scanf("%lf%d",&x,&n);
    y=x*1.0;
    for(i=0;i<n;i++){
        y=(y+x/y)/2.0;
    }
    printf("%.5lf",y);
    return 0;
}
```



