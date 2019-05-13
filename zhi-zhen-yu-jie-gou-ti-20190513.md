---
description: '2019-05-13 17:27:00 至 2019-05-28 17:25:00'
---

# 指针与结构体 2019-05-13

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
​
```

## 2.指针与数组



