# 算法

## 递归:汉诺塔

```python
import time

num = 0


def move(n, From, Buffer, To):
    if n == 1:
        print('{} -> {}'.format(From, To))
        global num
        num += 1
    else:
        move(n - 1, From, To, Buffer)
        move(1, From, Buffer, To)
        move(n - 1, Buffer, From, To)


if __name__ == '__main__':
    n = input('请输入层数')
    now = time.time()
    move(n, 'A', 'B', 'C')
    print('移动次数:{},耗时:{:3f}s'.format(num, time.time() - now))

```

