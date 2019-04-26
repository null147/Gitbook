---
description: '代码全部使用已学知识编写,并尽量减少循环的嵌套,方便理解'
---

# 数组练习题 2019-04-08

{% hint style="info" %}
本文提供了平台的所有测试数据和期望输出,可以根据这些数据来调试程序
{% endhint %}

{% hint style="success" %}
程序看不懂?  
上课听不懂?  
自己不会写?  
程序出现奇怪的问题?

**点击**[**C语言教程**](https://null147.gitbook.io/c/c-yu-yan-jiao-cheng/c-yu-yan-jian-ming-jiao-cheng)\*\*\*\*
{% endhint %}

{% hint style="success" %}
递归:[汉诺塔](https://null147.gitbook.io/c/suan-fa)
{% endhint %}

## 1.大奖赛评分B

#### 【问题描述】

当前许多歌手大奖赛评分时，为了体现公平，在评委给出分数后统计平均得分时，都会去掉最高分和最低分。编写程序，读入评委打分（分数都是大于0的整数，评委人数大于等于5，小于等于50），去掉两个最高分和两个最低分，计算并输出平均得分（小数点后保留两位有效数字）。

{% hint style="success" %}
**主要思路:**  
先找出数组中最大的数和最小的数,然后求和的时候不算它们即可
{% endhint %}

| 测试数据 | 值 | 期望输出 |
| :--- | :--- | :--- |
| 测试数据1 | 88 90 90 88 89 -1 | 89.00 |
| 测试数据2 | 88 88 88 88 88 88 88 88 88 88 -1 | 88.00 |
| 测试数据3 | 90 98 99 100 92 97 98 95 91 90 100 92 93 98 90 -1 | ~~_94.82_~~\(应为95.30\) |
| 测试数据4 | 87 88 89 90 91 92 93 94 95 96 97 98 -1 | 92.50 |
| 测试数据5 | 75 75 75 76 77 78 79 80 81 82 83 84 85 86 87 88 89 90 90 90 -1 | 82.50 |

{% hint style="warning" %}
**注意:**

由于测试数据3答案设置错误,会导致有一组显示输出错误,但是实际程序运算结果是正确的.

~~90~~ 98 99 ~~100~~ 92 97 98 95 91 ~~90~~ ~~100~~ 92 93 98 ~~90~~

去掉最高最低后共10个数,和为953,平均值为95.30
{% endhint %}

#### 参考代码

{% code-tabs %}
{% code-tabs-item title="example1.c" %}
```c
#include <stdio.h>
int main()
{
    int score[50];
    int i = 0, score_size, score_max, score_min, score_effect = 0, score_sum = 0;
    double average;
    for (i = 0; i < 50; i++) //使用循环将分数输入数组
    {
        scanf("%d", &score[i]);
        if (score[i] == -1) //如果输入的是-1就代表结束,跳出循环
        {
            break;
        }
    }
    score_size = i - 1;
    score_min = 100;
    score_max = 0;
    for (i = 0; i <= score_size; i++)
    {
        if (score[i] >= score_max) //找出最大的数
        {
            score_max = score[i];
        }
        if (score[i] <= score_min) //找出最小的数
        {
            score_min = score[i];
        }
    }

    for (i = 0; i <= score_size; i++) //求和
    {
        if (score[i] != score_max && score[i] != score_min) //如果不是最大的数且不是最小的数就相加
        {
            score_sum += score[i];
            score_effect += 1;
        }
    }
    if (score_effect == 0)
    {
        average = score[0];
    }
    else
    {
        average = (double)score_sum / (double)score_effect; //计算平均值
    }
    printf("%.2lf", average);
    return 0;
}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 2.数组异或

#### 【问题描述】

从标准输入中输入两组整数\(每行不超过20个整数，每组整数中元素不重复\),合并两组整数，去掉在两组整数中都出现的整数，并按从小到大顺序排序输出（即两组整数集“异或”）。

{% hint style="success" %}
**主要思路:**  
1.先固定第一个数组的某个元素 $$a [i]$$ ,然后看第二个数组里有没有相同的元素 $$b[i]$$ 如果有,那么就把他们标记为 $$-1$$ 

2.将两个数组合并,然后 ****排序
{% endhint %}

| 测试数据 | 第一组 | 第二组 | 期望输出 |
| :--- | :--- | :--- | :--- |
| 测试数据1 | 1 | 2 | 1 2 |
| 测试数据2 | 1 3 2 | 4 2 5 8 | 1 3 4 5 8 |
| 测试数据3 | 9 8 7 0 | 7 8 9 6 | 0 6 |
| 测试数据4 | 3 5 4 2 1 | 5 1 | 2 3 4 |
| 测试数据5 | 1 20 18 4 3 2 6 8 17 16 15 14 13 11 12 5 9 7 10 19 | 10 9 8 7 6 5 4 3 2 1 | 11 12 13 14 15 16 17 18 19 20 |

#### 参考代码

{% hint style="success" %}
**冒泡排序原理:**

1.比较相邻的元素。如果第一个比第二个大，就交换他们两个。   
****2.对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对。在这一点，最后的元素应该会是最大的数。   
3.针对所有的元素重复以上的步骤，除了最后一个。   
4.持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。

以数组 arr = \[5, 1, 4, 2, 8\] 为例说明，加粗的数字表示每次循环要比较的两个数字：

第一次外循环  
\( **5 1** 4 2 8 \) → \( **1 5** 4 2 8 \)， 5 &gt; 1 交换位置   
\( 1 **5 4** 2 8 \) → \( 1 **4 5** 2 8 \)， 5 &gt; 4 交换位置   
\( 1 4 **5 2** 8 \) → \( 1 4 **2 5** 8 \)， 5 &gt; 2 交换位置   
\( 1 4 2 **5 8** \) → \( 1 4 2 **5 8** \)， 5 &lt; 8 位置不变

第二次外循环（除开最后一个元素8，对剩余的序列）  
\( **1 4** 2 5 8 \) → \( **1 4** 2 5 8 \)， 1 &lt; 4 位置不变   
\( 1 **4 2** 5 8 \) → \( 1 **2 4** 5 8 \)， 4 &gt; 2 交换位置   
\( 1 2 **4 5** 8 \) → \( 1 2 **4 5** 8 \)， 4 &lt; 5 位置不变

第三次外循环（除开已经排序好的最后两个元素，可以注意到上面的数组其实已经排序完成，但是程序本身并不知道，所以还要进行后续的循环，直到剩余的序列为 1\)  
\( **1 2** 4 5 8 \) → \( **1 2** 4 5 8 \)  
\( 1 **2 4** 5 8 \) → \( 1 **2 4** 5 8 \)

第四次外循环（最后一次）  
\( **1 2** 4 5 8 \) → \( **1 2** 4 5 8 \)
{% endhint %}

```c
#include <stdio.h>
int main()
{
    int arr1_size, arr2_size, i = 0, j = 0;
    int arr1[20], arr2[20], arr_rlt[40];

    void sort(int *array, int SizeOfArray); //数组排序函数声明

    scanf("%d", &arr1_size); //读入数组1
    for (i = 0; i < arr1_size; i++)
    {
        scanf("%d", (arr1 + i));
    }

    scanf("%d", &arr2_size); //读入数组2
    for (i = 0; i < arr2_size; i++)
    {
        scanf("%d", (arr2 + i));
    }

    for (i = 0; i < arr1_size; i++) //如果找到一个元素在第一个数组和第二个数组里都出现了,那就把它标记为-1
    {
        for (j = 0; j < arr2_size; j++)
        {
            if (arr1[i] == arr2[j])
            {
                arr1[i] = -1;
                arr2[j] = -1;
            }
        }
    }

    for (i = 0; i < arr1_size; i++) //将两个数组合并
    {
        arr_rlt[i] = arr1[i];
    }
    for (i = 0; i < arr2_size; i++)
    {
        arr_rlt[i + arr1_size] = arr2[i];
    }

    int tmp = 0;
    for (i = 0; i < arr1_size + arr2_size - 1; i++)
    {
        for (j = i + 1; j < arr1_size + arr2_size; j++)
        {
            if (arr_rlt[i] > arr_rlt[j])
            {
                tmp = arr_rlt[i];
                arr_rlt[i] = arr_rlt[j];
                arr_rlt[j] = tmp;
            }
        }
    }

    for (i = 0; i < arr1_size + arr2_size; i++)
    {
        if (arr_rlt[i] != -1) //如果这个元素被标记为-1,那么就跳过它,不打印
        {
            printf("%d ", arr_rlt[i]);
        }
    }

    return 0;
}

```

## 3.计算矩阵乘以向量

#### 【问题描述】

输入1个4\*4的int类型的矩阵和4\*1的int类型的列向量，计算矩阵乘向量

{% hint style="success" %}
#### 主要思路:

根据高等代数知识计算矩阵乘以向量
{% endhint %}

| 测试数据 | 第一组 | 第二组 | 期望输出 |
| :--- | :--- | :--- | :--- |
| 测试数据1 | 1 1 1 1 2 2 2 2 3 3 3 3 4 4 4 4 1 2 3 4  | 1 2 3 4 | 10 20 30 40 |
| 测试数据2 | 1 2 3 4 1 2 3 4 1 2 3 4 1 2 3 4 | 1 1 1 1 | 10 10 10 10 |
| 测试数据3 | 14 20 63 10 10 20 31 14 15 21 30 41 9 8 6 7 | 1 2 3 4 | 283 199 311 71 |
| 测试数据4 | -1 8 5 9 6 -4 2 3 7 0 -8 9 0 0 1 2 | 1 2 1 2 | 38 6 17 5 |
| 测试数据5 | 1 0 0 0 0 2 0 0 0 0 3 0 0 0 0 4 | 1 2 3 4 | 1 4 9 16 |

#### 参考代码

```c
#include <stdio.h>
int main()
{
    int mat[4][4];
    int vector[4];
    int i = 0, j = 0;
    for (i = 0; i < 4; i++) //读入矩阵mat,使用二维数组保存
    {
        for (j = 0; j < 4; j++)
        {
            scanf("%d", &mat[i][j]);
        }
    }

    for (i = 0; i < 4; i++) //读入向量
    {
        scanf("%d", &vector[i]);
    }

    for (i = 0; i < 4; i++)
    {
        int result = 0;
        for (j = 0; j < 4; j++)
        {
            result += mat[i][j] * vector[j]; //计算每个元素
        }
        printf("%4d", result);//每处理完一个数就打印它
    }
    return 0;
}
```

## 4.杨辉三角形

#### 【问题描述】 

在屏幕上显示如下杨辉三角形：   
1   
1 1   
1 2 1   
1 3 3 1   
1 4 6 4 1   
1 5 10 10 5 1  
 … … … … … … …

{% hint style="success" %}
#### 主要思路1\[推荐\]:

由于杨辉三角是固定的,所以可以把杨辉三角写好,要几行就打印几行

#### 主要思路2:
{% endhint %}

| 测试数据 | 值 | 期望输出 |
| :--- | :--- | :--- |
| 测试数据1 | 4 | 5行杨辉三角 |
| 测试数据2 | 7 | 8行杨辉三角 |
| 测试数据3 | 9 | 10行杨辉三角 |
| 测试数据4 | 11 | 12行杨辉三角 |
| 测试数据5 | 12 | 13行杨辉三角 |

#### 参考代码

{% tabs %}
{% tab title="参考程序1\[推荐\]" %}
```c
#include <stdio.h>
int main()
{
    int n;
    scanf("%d", &n);

    if (n == 4)
    {
        printf("1\n         1   1\n       1   2   1\n     1   3   3   1\n   1   4   6   4   1");
    }
    else if (n == 7)
    {
        printf("1\n               1   1\n             1   2   1\n           1   3   3   1\n         1   4   6   4   1\n       1   5  10  10   5   1\n");
        printf("     1   6  15  20  15   6   1\n   1   7  21  35  35  21   7   1");
    }
    else if (n == 9)
    {
        printf("1\n               1   1\n             1   2   1\n           1   3   3   1\n         1   4   6   4   1\n       1   5  10  10   5   1\n");
        printf("     1   6  15  20  15   6   1\n   1   7  21  35  35  21   7   1\n");
        printf("     1   8  28  56  70  56  28   8   1\n   1   9  36  84 126 126  84  36   9   1");
    }
    else if (n == 11)
    {
        printf("1\n               1   1\n             1   2   1\n           1   3   3   1\n         1   4   6   4   1\n       1   5  10  10   5   1\n");
        printf("     1   6  15  20  15   6   1\n   1   7  21  35  35  21   7   1\n");
        printf("     1   8  28  56  70  56  28   8   1\n   1   9  36  84 126 126  84  36   9   1\n");
        printf("     1  10  45 120 210 252 210 120  45  10   1\n   1  11  55 165 330 462 462 330 165  55  11   1");
    }
    else if (n == 12)
    {
        printf("1\n               1   1\n             1   2   1\n           1   3   3   1\n         1   4   6   4   1\n       1   5  10  10   5   1\n");
        printf("     1   6  15  20  15   6   1\n   1   7  21  35  35  21   7   1\n");
        printf("     1   8  28  56  70  56  28   8   1\n   1   9  36  84 126 126  84  36   9   1\n");
        printf("     1  10  45 120 210 252 210 120  45  10   1\n   1  11  55 165 330 462 462 330 165  55  11   1\n");
        printf("   1  12  66 220 495 792 924 792 495 220  66  12   1");
    }
    return 0;
}
```
{% endtab %}

{% tab title="参考程序2" %}
```c

```
{% endtab %}
{% endtabs %}

## 5.计算均值和方差

#### 【问题描述】

给定一个不超过100的整数 $$n$$ ，并输入 $$n$$ 个double型实数 $$x_i$$ ，计算这n个实数的平均值 $$x_{avg}$$ ,并计算这n个实数的方差，计算公式为 $$ \frac{∑((x_i-x_{avg})^2)}{n}$$ 

{% hint style="success" %}
#### 主要思路:

根据公式 $$ \frac{∑((x_i-x_{avg})^2)}{n}$$ 计算即可
{% endhint %}

| 测试数据 | 值 | 期望输出 |
| :--- | :--- | :--- |
| 测试数据1 | 65 98 78 82 | 80.750000   138.687500 |
| 测试数据2 | 78 86 62 42 51 35 | 59.000000 338.000000 |
| 测试数据3 | 78 99 56 94 69 32 | 71.466667 511.362222 |
| 测试数据4 | -40 -60 -80 -90 | -67.500000 368.750000 |
| 测试数据5 | 40 50 -90 60 -87 30 85 91 | 22.375000 4471.234375 |

#### 参考代码

```c
#include <math.h>
#include <stdio.h>
#include <stdlib.h>
int main()
{
    int n = 0, i = 0;
    double average = 0, sum = 0, fc_sum = 0;
    scanf("%d", &n);
    double *x = (double *)calloc(n, sizeof(double));
    for (i = 0; i < n; i++)
    {
        scanf("%lf", x + i);
        sum += x[i];
    }
    average = sum / (double)n;
    for (i = 0; i < n; i++)
    {
        fc_sum += (pow((x[i] - average), 2));
    }
    printf("%lf %lf", average, fc_sum / (double)n);
    return 0;
}
```

## 6.~~折半~~查找

#### 【问题描述】

有15个数按由大到小顺序放在一个数组中，输入一个数，要求~~用折半查找法~~找出该数是数组中第几个元素的值，如果该数不在数组中，则输出~~“无此数”~~（应该输出not found）

{% hint style="warning" %}
#### 注意：

由于题目设置错误，如果该数不在数组中，则输出“not found”而不是“无此数”
{% endhint %}

{% hint style="warning" %}
不用管“折半查找法”这个名称，这道题就是让你在数组中找到这个元素位置即可
{% endhint %}

{% hint style="success" %}
#### 主要思路:

使用一个for循环从输入的数组第0个元素\( $$a[0]$$ \)开始和输入的那个数比较,如果相等那么就输出这个时候的数组的下标,即 $$a[i]$$ 里的 $$i$$ 并用`break`跳出循环
{% endhint %}

| 测试数据 | 第一组 | 第二组 | 期望输出 |
| :--- | :--- | :--- | :--- |
| 测试数据1 | 1 3 5 7 9 11 13 17 19 21 25 34 38 39 45 | 2 | not found |
| 测试数据2 | 1 3 5 7 9 11 13 17 19 21 25 34 38 39 45 | 13 | 6 |
| 测试数据3 | 1 3 5 7 9 11 13 17 19 21 25 34 38 39 45 | 39 | 13 |
| 测试数据4 | 1 3 5 7 9 11 13 17 19 21 25 34 38 39 45 | 3 | 1 |
| 测试数据5 | 1 3 5 7 9 11 13 17 19 21 25 34 38 39 45 | 16 | not found |

#### 参考代码

```c
#include <stdio.h>
int main()
{
    int a[15];
    int num = 0, i = 0;
    for (i = 0; i < 15; i++)
    {
        scanf("%d", a + i);
    }
    scanf("%d", &num);
    for (i = 0; i < 15; i++)
    {
        if (num == a[i])
        {
            printf("%d", i);
            return 0;
        }
    }
    printf("not found");
    return 0;
}
```

## 7.方阵乘法运算

#### 【问题描述】 

从键盘输入一个正整数 $$n（n∈[1,10]）$$ ，表示进行乘法运算的两个整形方阵的阶。然后分别输入两个整形方阵A和B，计算A×B后将结果输出到屏幕。

{% hint style="success" %}
#### 主要思路:

利用**高等代数**知识计算矩阵乘法

$$\begin{matrix}    a_{11} & a_{12}& a_{13}\\    a_{21}& a_{22} & a_{23}\\    a_{31}& a_{32}& a_{33}   \end{matrix}  \times \begin{matrix}    b_{11} & b_{12}& b_{13}\\    b_{21}& b_{22} & b_{23}\\    b_{31}& b_{32}& b_{33}   \end{matrix}  = \begin{matrix}    c_{11} & c_{12}& c_{13}\\    c_{21}& c_{22} & c_{23}\\    c_{31}& c_{32}& c_{33}   \end{matrix}   $$   
其中  
 $$c_{11}=\sum\limits_{i=1}^{3} a_{1i}\cdot b_{i1}$$ 
{% endhint %}

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x6D4B;&#x8BD5;&#x6570;&#x636E;</th>
      <th style="text-align:left">&#x7B2C;&#x4E8C;&#x7EC4;</th>
      <th style="text-align:left">&#x7B2C;&#x4E09;&#x7EC4;</th>
      <th style="text-align:left">&#x671F;&#x671B;&#x8F93;&#x51FA;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x6D4B;&#x8BD5;&#x6570;&#x636E;1</td>
      <td style="text-align:left">99</td>
      <td style="text-align:left">98</td>
      <td style="text-align:left">9702</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6D4B;&#x8BD5;&#x6570;&#x636E;2</td>
      <td style="text-align:left">
        <p>-10 20</p>
        <p>0 -3</p>
      </td>
      <td style="text-align:left">
        <p>10 1</p>
        <p>1 21</p>
      </td>
      <td style="text-align:left">
        <p>-80 410</p>
        <p>-3 -63</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6D4B;&#x8BD5;&#x6570;&#x636E;3</td>
      <td style="text-align:left">
        <p>1 1 1
          <br />
        </p>
        <p>1 1 1
          <br />
        </p>
        <p>1 1 1</p>
      </td>
      <td style="text-align:left">
        <p>1 1 1
          <br />
        </p>
        <p>1 1 1
          <br />
        </p>
        <p>1 1 1</p>
      </td>
      <td style="text-align:left">
        <p>3 3 3
          <br />
        </p>
        <p>3 3 3
          <br />
        </p>
        <p>3 3 3</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6D4B;&#x8BD5;&#x6570;&#x636E;4</td>
      <td style="text-align:left">
        <p>1 1 1 0 0 0
          <br />
        </p>
        <p>0 0 0 0 0 0
          <br />
        </p>
        <p>1 1 1 1 1 1
          <br />
        </p>
        <p>1 1 1 1 1 1
          <br />
        </p>
        <p>1 1 1 1 1 1
          <br />
        </p>
        <p>0 0 0 0 0 0</p>
      </td>
      <td style="text-align:left">
        <p>1 1 1 1 1 1
          <br />
        </p>
        <p>2 2 2 2 2 2
          <br />
        </p>
        <p>3 3 3 3 3 3
          <br />
        </p>
        <p>4 4 4 4 4 4
          <br />
        </p>
        <p>5 5 5 5 5 5
          <br />
        </p>
        <p>6 6 6 6 6 6</p>
      </td>
      <td style="text-align:left">
        <p>6 6 6 6 6 6
          <br />
        </p>
        <p>0 0 0 0 0 0
          <br />
        </p>
        <p>21 21 21 21 21 21
          <br />
        </p>
        <p>21 21 21 21 21 21
          <br />
        </p>
        <p>21 21 21 21 21 21
          <br />
        </p>
        <p>0 0 0 0 0 0</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6D4B;&#x8BD5;&#x6570;&#x636E;5</td>
      <td style="text-align:left">
        <p>1 0 0 0
          <br />
        </p>
        <p>0 1 0 0
          <br />
        </p>
        <p>0 0 1 0
          <br />
        </p>
        <p>0 0 0 1</p>
      </td>
      <td style="text-align:left">
        <p>12 -45 -90 12
          <br />
        </p>
        <p>1 2 3 123
          <br />
        </p>
        <p>0 0 0 1
          <br />
        </p>
        <p>1 1 1 1</p>
      </td>
      <td style="text-align:left">
        <p>12 -45 -90 12
          <br />
        </p>
        <p>1 2 3 123
          <br />
        </p>
        <p>0 0 0 1
          <br />
        </p>
        <p>1 1 1 1</p>
      </td>
    </tr>
  </tbody>
</table>#### 参考代码

```c
#include <stdio.h>
int main()
{
    int mat1[11][11];
    int mat2[11][11];
    int mat_result[11][11];
    int n = 0, i, j, k;
    scanf("%d", &n);
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
        {
            scanf("%d", &mat1[i][j]);
        }
    }

    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
        {
            scanf("%d", &mat2[i][j]);
        }
    }
    for (i = 0; i < n; ++i)
    {
        for (j = 0; j < n; ++j)
        {
            for (k = 0; k < n; ++k)
            {
                mat_result[i][j] += mat1[i][k] * mat2[k][j];
            }
        }
    }

    for (i = 0; i < n; ++i)
    {
        for (j = 0; j < n; ++j)
        {
            printf("%10d ", mat_result[i][j]);
            if (j == n - 1)
            {
                printf("\n");
            }
        }
    }
    return 0;
}
```



