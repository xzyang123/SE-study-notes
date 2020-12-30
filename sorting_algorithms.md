### recursion的要点
1. 将一个大问题分解成小问题的组合(size n 的问题依赖于size n-1或size n-2或size n/2的组合)
2. 实现：

    2.1 base case：smallest problem to solve
    
    2.2 recursive rule：how to make the problem smaller
    
        如果我们可以解决最小号的问题，那如何把最小号的问题和大问题联系起来？

### recursion的时空间复杂度分析
1. 时间复杂度：整个recursion tree里面所有节点的时间复杂度之和
2. 空间复杂度：直上直下的粉红色路径上所有节点的空间复杂度之和

### Sorting Algorithms

1. Selection Sort

首先遍历整个数组找出最小值，然后把最小值放在最左边，然后再遍历剩下的数字，也再找出最小值顺着放在前一个最小值的旁边

然后用同样的方法一直循环下去直到数组最后只剩一个数字为止。

```java
    public int[] selectionSort(int[] array) {
        if 
    }
```

