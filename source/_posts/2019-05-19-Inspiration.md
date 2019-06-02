---
title: Inspiration
description: 与编程有关的思考与灵感
date: 2019-05-19 22:46:21
tags:
    - Thinking
categories:
    - Induction
---

# 使用状态码的优势

首先在数据库层面, 无论是查询效率还是存储空间来看, 数字肯定是优于字符串的,
但同样地, 字符串的可读性是优于数字的;

如果用数字的话

1. 简化查询: 在设计良好的情况下, 可以采用大小比较的方式很快的筛选出特定的数据, 顺序在设计初就想好, 如果设想不会超过10个状态那就10,20,30这样进行编码以后添加状态可在符合原有规律的前提下采用二分法添加

2. 在后端采用枚举类形式, 可以实现与字符串同样的效果: 前端, 后端都可以使用字符串, 达到可读性的目的, 只需要在某个特定的地方(通常是DAO层)进行转换, java的话是可以直接转换的, 而且编译器还能帮助检查拼写错误

3. 如果后续添加的状态码打乱了之前的顺序怎么办: 如果直接在最后的状态码后面追加破坏了已有的规律, 可以对状态码进行重构: 由于程序各个地方都使用的是字符串, 或是枚举值, 我们只需要改变枚举类的映射关系即可, 而以前的数据的状态码可以使用更新语句进行更新; 如果数据量过大导致这种方法消耗过大的话可以考虑直接加上特殊的判定.

这么一来仅仅只牺牲了数据库的可读性, 但是换来了数据存储空间和查询效率的优化, 最重要的是查询的简化, 并且没有带来前后端编程时可读性的降低, 反而能够获得编译器的检查

[参考](https://segmentfault.com/q/1010000003709270)

# 思维漏洞

## 基于循环的排列组合
 C(100, 5)
``` js
var size = 100, count = 0;
for (let i1 = 0; i1 < size; ++i1) {
    for (let i2 = i1+1; i2 < size; ++i2) {
        for (let i3 = i2+1; i3 < size; ++i3) {
            for (let i4 = i3+1; i4 < size; ++i4) {
                for (let i5 = i4+1; i5 < size; ++i5) {
                    ++count;
                    //console.log(i1 + ' ' + i2  + ' ' + i3 + ' ' + i4 + ' ' + i5 )
                }
            }
        }
    }
}
console.log(count);
// 结果
C(100, 5) -> 75287520       VM241:10
A(100, 5) -> 9034502400.0
```

## [基于方法的排列组合](https://blog.csdn.net/lanchunhui/article/details/51824602)
1. 调用 scipy 计算排列组合的具体数值
    ``` python
    from scipy.special import comb, perm
    ```
    排列数
    A(3, 2)=6
    ```python
    perm(3, 2)
    ```
    6.0
    组合数
    C(3, 2)=3
    ```python
    comb(3, 2)
    ```
    3.0

2. 调用 itertools 获取排列组合的全部情况数
    ```python
    from itertools import combinations, permutations
    permutations([1, 2, 3], 2)
    ```

    可迭代对象
    <itertools.permutations at 0x7febfd880fc0>

    排列数
    ```python
    list(permutations([1, 2, 3], 2))
    ```
    [(1, 2), (1, 3), (2, 1), (2, 3), (3, 1), (3, 2)]

    组合数
    ```python
    list(combinations([1, 2, 3], 2))
    ```
    [(1, 2), (1, 3), (2, 3)]

- Github Gist 2018-11-03 11:46
