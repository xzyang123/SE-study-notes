### Selection Sort

原理： 每次在当前数组里面通过Interation的方式找到最小值，然后把最小值放在数组最左边

TC：因为要依序遍历数组，所以TC = O(n^2)

SC：O(1)

Solution 1
```java
    public int[] solve(int[] array) {
      if (array == null || array.length <= 1) {
        return array;
      }
      for (int i = 0; i < array.length - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < array.length; j++) {
          if (array[j] < array[minIndex]) {
            minIndex = j;
          }
        }
        swap(array, minIndex, i);
      }
      return array;
    }
    private void swap(int[] array, int a, int b) {
      int temp = array[a];
      array[a] = array[b];
      array[b] = temp; 
    }
```

Solution 2

用两个额外的stack，并且维护一个globle_min

Stack1 (input) [3 4
Stak2 (buffer) [
Stack3 (result) [1 2 
int globle_min = 2

TC = O(n^2)

Solution 3

只用一个额外的stack
Stack1 (intput) [1 3 2 4
Stack2 (buffer & output) [
