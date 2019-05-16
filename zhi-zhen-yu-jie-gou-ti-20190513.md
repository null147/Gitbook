---
description: '2019-05-13 17:27:00 至 2019-05-28 17:25:00'
---

# 指针与结构体 2019-05-13

{% hint style="info" %}
该页面未更新完毕,你所看到的不是最终版本
{% endhint %}

{% hint style="info" %}
**你觉得这个网站有什么值得改进的地方?**[**点击这里**](https://forms.office.com/Pages/ResponsePage.aspx?id=DQSIkWdsW0yxEjajBLZtrQAAAAAAAAAAAAN__tGLjjZUNVhQS1VOVFdGQjA0VkROSUVaNFZTSVVNRS4u)**!**
{% endhint %}

{% hint style="info" %}
&gt;广告位招商&gt;
{% endhint %}

## 1.结构体学生

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x6D4B;&#x8BD5;&#x6570;&#x636E;</th>
      <th style="text-align:left">&#x503C;</th>
      <th style="text-align:left">&#x671F;&#x671B;&#x8F93;&#x51FA;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x6D4B;&#x8BD5;&#x6570;&#x636E;1</td>
      <td style="text-align:left">
        <p>20180101 SunLi 68 95 100 87
          <br />
        </p>
        <p>20180102 ZhaoHong 85 41 85 70
          <br />
        </p>
        <p>20180103 liuJia 78 74 85 79
          <br />
        </p>
        <p>20180104 Lubang 74 85 52 70
          <br />
        </p>
        <p>20180105 Qiaokang 75 85 55 71
          <br />
        </p>
        <p>20180101 SunLi 68 95 100 87
          <br />
        </p>
      </td>
      <td style="text-align:left">20180101 SunLi 68 95 100 87</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6D4B;&#x8BD5;&#x6570;&#x636E;2</td>
      <td style="text-align:left">
        <p>20180111 SunLi 68 15 40 41
          <br />
        </p>
        <p>20180112 ZhaoHong 85 100 85 90
          <br />
        </p>
        <p>20180113 liuJia 78 74 85 79
          <br />
        </p>
        <p>20180114 Lubang 74 85 52 70
          <br />
        </p>
        <p>20180115 Qiaokang 75 85 55 71
          <br />
        </p>
        <p>20180112 ZhaoHong 85 100 85 90
          <br />
        </p>
      </td>
      <td style="text-align:left">20180112 ZhaoHong 85 100 85 90
        <br />
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6D4B;&#x8BD5;&#x6570;&#x636E;3</td>
      <td style="text-align:left">
        <p>20180121 SunLi 68 95 100 87
          <br />
        </p>
        <p>20180122 ZhaoHong 85 41 85 70
          <br />
        </p>
        <p>20180123 liuJia 78 74 85 79
          <br />
        </p>
        <p>20180124 Lubang 74 85 52 70
          <br />
        </p>
        <p>20180125 Qiaokang 95 85 99 93
          <br />
        </p>
        <p>20180125 Qiaokang 95 85 99 93
          <br />
        </p>
      </td>
      <td style="text-align:left">20180125 Qiaokang 95 85 99 93</td>
    </tr>
  </tbody>
</table>#### 参考代码

```c
#include <stdio.h>
//定义学生结构体
typedef struct Student //使用typedef就可以新定义一个类型名为Student
{
    int id;
    char name[32];
    int class1, class2, class3;
} Student;

int main()
{
    Student stu[5]; //声名Student类型的数组(结构体数组)
    double average[5];
    double average_max = 0;
    int index = 0, i = 0;
    for (i = 0; i < 5; i++)
    {
        scanf("%d %s %d %d %d", &stu[i].id, &stu[i].name, &stu[i].class1, &stu[i].class2, &stu[i].class3);
    }
    for (i = 0; i < 5; i++)
    {
        average[i] = (stu[i].class1 + stu[i].class2 + stu[i].class3) / (double)3; //计算平均值
    }
    for (i = 0; i < 5; i++)
    {
        if (average[i] >= average_max) //找到平均值的最大值
        {
            average_max = average[i];
            index = i;
        }
    }
    printf("%d %s %d %d %d %d", stu[index].id, stu[index].name, stu[index].class1, stu[index].class2, stu[index].class3, (int)average[index]);
    return 0;
}
```

## 2.指针与数组

| 测试数据 | 值 | 期望输出 |
| :--- | :--- | :--- |
| 测试数据1 | -1 -2 -3 -4 -5 -6 -7 -8 -9 0 | -45 |
| 测试数据2 | 10 2 5 6 9 41 -21 3 9 8 | 72 |
| 测试数据3 | 8 7 4 62 35 41 52 86 71 41 | 407 |

{% tabs %}
{% tab title="参考代码-用指针" %}
```c
#include <stdio.h>
int main()
{
    int arr[10], i = 0;
    for (i = 0; i < 10; i++)
    {
        scanf("%d", arr + i);//读入数组(用指针)
    }
    for ( i = 0; i < 10; i++)
    {
        static int sum = 0;
        sum += *(arr + i);//求和(用指针)
        if (i==9)
        {
            printf("%d", sum);//求和完毕就打印结果,然后结束程序
            return 0;
        } 
    }
    return 0;
}
```
{% endtab %}

{% tab title="参考代码-不用指针" %}
```c
#include <stdio.h>
int main()
{
    int arr[10], i = 0;
    for (i = 0; i < 10; i++)
    {
        scanf("%d", arr[i]);//读入数组
    }
    for ( i = 0; i < 10; i++)
    {
        static int sum = 0;
        sum += arr[i];//求和
        if (i==9)
        {
            printf("%d", sum);//求和完毕就打印结果,然后结束程序
            return 0;
        } 
    }
    return 0;
}
```
{% endtab %}
{% endtabs %}

## 3.动态分配内存

| 测试数据 | 第一组 | 第二组 | 期望输出 |
| :--- | :--- | :--- | :--- |
| 测试数据1 | 4 | 65 98 78 82 | 80.750000 138.687500 |
| 测试数据2 | 6 | 78 86 62 42 51 35 | 59.000000   338.000000 |
| 测试数据3 | 6 | 78 0 0 0 0 0 | 71.466667   511.362222 |
| 测试数据4 | 4 | -40 -60 -80 -90 | -67.500000   368.750000 |

{% tabs %}
{% tab title="参考代码-最简方法" %}
```c
#include<stdio.h>
int main()
{
    int n = 0, i = 0, sum = 0;
    double sum_fc=0;
    int arr[100];
    scanf("%d", &n);
    for (i = 0; i < n; i++)
    {
        scanf("%d", &arr[i]);
    }
    for ( i = 0; i < n; i++)
    {
        sum += arr[i];
    }
    double avg=(double)sum/(double)n;
    for ( i = 0; i < n; i++)
    {
        sum_fc += (arr[i] - avg) * (arr[i] - avg);
    }
    printf("%12.6lf %12.6lf", avg, sum_fc / n);
    return 0;
}
```
{% endtab %}

{% tab title="参考代码-动态分配内存" %}
```c
#include<stdio.h>
#include<stdlib.h>//calloc函数在stdlib.h中
int main()
{
    int n = 0, i = 0, sum = 0;
    double sum_fc=0;
    int *arr = (int *)calloc(n, sizeof(int));//calloc函数可以动态申请内存空间,返回个指向数组首地址的指针
    scanf("%d", &n);
    for (i = 0; i < n; i++)
    {
        scanf("%d", &arr[i]);
    }
    for ( i = 0; i < n; i++)
    {
        sum += arr[i];
    }
    double avg=(double)sum/(double)n;
    for ( i = 0; i < n; i++)
    {
        sum_fc += (arr[i] - avg) * (arr[i] - avg);
    }
    printf("%12.6lf %12.6lf", avg, sum_fc / n);
    return 0;
}
```
{% endtab %}
{% endtabs %}

## 4.指针判断年月日

{% hint style="info" %}
神说:战士的最后一发子弹当留给自己
{% endhint %}

```text
刘少瑞.神说:战士的最后一发子弹当留给自己
```

