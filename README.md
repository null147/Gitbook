---
description: 包含9道小题
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

{% hint style="info" %}
注意:由于测试数据3答案设置错误,会导致有一组显示输出错误,但是实际程序运算结果是正确的.

~~90~~ 98 99 ~~100~~ 92 97 98 95 91 ~~90~~ ~~100~~ 92 93 98 ~~90~~

去掉最高最低后共10个数,和为953,平均值为95.30
{% endhint %}

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



