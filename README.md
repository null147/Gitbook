---
description: '代码全部使用已学知识编写(教学进度由隋凯鹏提供),并尽量减少循环的嵌套,方便理解'
---

# 数组练习题 2019-04-08

## 1.大奖赛评分B

#### 【问题描述】

当前许多歌手大奖赛评分时，为了体现公平，在评委给出分数后统计平均得分时，都会去掉最高分和最低分。编写程序，读入评委打分（分数都是大于0的整数，评委人数大于等于5，小于等于50），去掉两个最高分和两个最低分，计算并输出平均得分（小数点后保留两位有效数字）。

| 测试数据 | 值 | 期望输出 |
| :--- | :--- | :--- |
| 测试数据1 | 88 90 90 88 89 -1 | 89.00 |
| 测试数据2 | 88 88 88 88 88 88 88 88 88 88 -1 | 88.00 |
| 测试数据3 | 90 98 99 100 92 97 98 95 91 90 100 92 93 98 90 -1 | ~~_94.82_~~\(应为95.30\) |
| 测试数据4 | 87 88 89 90 91 92 93 94 95 96 97 98 -1 | 92.50 |
| 测试数据5 | 75 75 75 76 77 78 79 80 81 82 83 84 85 86 87 88 89 90 90 90 -1 | 82.50 |

{% hint style="warning" %}
注意:由于测试数据3答案设置错误,会导致有一组显示输出错误,但是实际程序运算结果是正确的.

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
    for (i = 0; i <= score_size; i++) //找出最大的数
    {
        if (score[i] >= score_max)
        {
            score_max = score[i];
        }
    }
    for (i = 0; i <= score_size; i++) //找出最小的数
    {
        if (score[i] <= score_min)
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
    if (score_effect == 0)//如果所有的数都相等,平均值就是数组里的任意一个数
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

| 测试数据 | 第一组 | 第二组 | 期望输出 |
| :--- | :--- | :--- | :--- |
| 测试数据1 | 1 | 2 | 1 2 |
| 测试数据2 | 1 3 2 | 4 2 5 8 | 1 3 4 5 8 |
| 测试数据3 | 9 8 7 0 | 7 8 9 6 | 0 6 |
| 测试数据4 | 3 5 4 2 1 | 5 1 | 2 3 4 |
| 测试数据5 | 1 20 18 4 3 2 6 8 17 16 15 14 13 11 12 5 9 7 10 19 | 10 9 8 7 6 5 4 3 2 1 | 11 12 13 14 15 16 17 18 19 20 |

#### 参考代码

{% hint style="success" %}
小提示:这里定义了一个新的函数 sort ,其实不用管这个函数功能是怎么实现的,只需要知道这个函数可以把数组进行排序即可.  
**\[不需要重复造轮子\]**
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

    sort(arr_rlt, arr1_size + arr2_size); //调用排序函数

    for (i = 0; i < arr1_size + arr2_size; i++)
    {
        if (arr_rlt[i] != -1)//如果这个元素被标记为-1,那么就跳过它,不打印
        {
            printf("%d ", arr_rlt[i]);
        }
    }

    return 0;
}

//冒泡排序 函数第一个参数是要排序的数组 第二个参数是数组长度
void sort(int *array, int SizeOfArray)
{
    int i_, j_;
    int v;
    for (i_ = 0; i_ < SizeOfArray - 1; i_++)
        for (j_ = i_ + 1; j_ < SizeOfArray; j_++)
        {
            if (array[i_] > array[j_])
            {
                v = array[i_];
                array[i_] = array[j_];
                array[j_] = v;
            }
        }
}
```

