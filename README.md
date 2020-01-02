
# 记录一些有趣的算法题
## 1.给定一个列表, 只有一个元素没有重复，其他的元素都重复了两次，找到只重复一次的元素
### 方法1，暴力无脑，很慢
```

def func(lst):
    a = []
    for i in lst:
        if lst.count(i) == 1:
            a.append(i)
    return a
```

### 方法2，略微好一点，数据量大时很慢
```
def func(lst):
    a = []
    for i in lst:
        if i in a:
            a.remove(i)
        else:
            a.append(i)
    return a
```

### 方法3,很快，缺点是只能找一个元素，不能扩展。
原理是先把列表转集合去重，集合的和的二倍减去原列表的和就是只重复一次的元素。
```
def func(lst):
    a = set(lst)
    return sum(a)*2-sum(lst)
```

### 方法4，利用了一个数对任意数异或两次保持不变的特点,最快
```
def Find_single_show_num(lst):
    num= 0
    for i in lst:
        num ^= i
    return num
```

## 1.1 题1进阶，2个（或2个以上）元素只重复一次，剩下的元素重复两次，找出只重复一次的元素
以上的方法1， 方法2依然适用，但是据点依旧是慢，方法3不适用，方法4可以用但是需要改进
```
def func_3(lst):
    """num是两个只出现一次元素的异或结果，肯定不为0(因为只有相同的元素异或结果才为0)，不为0的十进制数转换为二进制后至少有一位为1，
    找到第一个"1"出现的位置（二进制表示中从后往前第一个"1"），并以此位置是否为1为标准把原列表拆分成两个列表，
    那么两个只出现一次的元素会被分在不同的列表，再对这两个列表分别求异或，得到的两个结果就是要找的两个元素了
    """
    num = Find_single_show_num(lst)
    loc_of_first_1 = bin(num)[::-1].index('1')
    a = []
    b = []
    for k in lst:
        if int(bin(k)[::-1][loc_of_first_1]) == 1:
            a.append(k)
        else:
            b.append(k)
    """此时a,b两个列表分别含有一个只出现一次的元素，其他元素出现两次，再次分别调用Find_single_show_num函数即可"""
    m = Find_single_show_num(a)
    n = Find_single_show_num(b)
    return m, n
```

## 2 归并排序
### 2.1 自底向上
```
def Gui_bing(lst):
    if len(lst) <= 1:
        return lst

    mid = int(len(lst) /2 )
    left = Gui_bing(lst[:mid])
    right = Gui_bing(lst[mid:])

    return merge_list(left, right)

def merge_list(left, right):
    result = []
    i, j = 0, 0
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    result += left[i:]
    result += right[j:]

    return result

a = [26,5,77,1,61,11,59,15,48,19]

print(Gui_bing(a))
```

### 2.2 自顶向下
```

```

