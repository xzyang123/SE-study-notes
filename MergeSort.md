### Merge Sort

原理：先把无序数组进行分割直到每个单元只有一个元素为止

然后再把只有一个元素的最小单元同其他的最小单元合并

重新组合成完整的数组，但是在每一次的合并过程中进行排序

这样最后得到的数组就是排序完成的数组。

```java
    public int[] mergeSort(int[] array) {
      if (array == null || array.length <= 1) {
        return array;
      }
      int[] helper = new int[array.length];
      mergeSort(array, helper, 0, array.length - 1);
      return array;
    }
    private void mergeSort(int[] array, int[] helper, int left, int right) {
      // base case
      if (left == right) {
        return;
      }
      int mid = left + (right - left) / 2;
      mergeSort(array, helper, left, mid);
      mergeSort(array, helper, mid + 1, right);
      merge(array, helper, left, mid, right);
    }
    private void merge(int[] array, int[] helper, int left, int mid, int right) {
      // copy elements from array to helper
      // use helper array as a buffer array
      // we do the comparasion in the helper array
      // then put correct order to the input array
      for (int i = left; i <= right; i++) {
        helper[i] = array[i];
      }
      int leftIndex = left;
      int rightIndex = mid + 1;
      while (leftIndex <= mid && rightIndex <= right) {
        if (helper[leftIndex] <= helper[rightIndex]) {
          array[left++] = helper[leftIndex++];
        } else {
          array[left++] = helper[rightIndex++];
        }
      }
      while (leftIndex <= mid) {
        array[left++] = helper[leftIndex++];
      }
      // here we do not need to do anything for rightPart
      // because the remained elements in the rightPart are in the corrected order already
    }
```

TC = O(n + nlogn)

    首先partition的时候每个元素都要被分割所以是O(n)
  
    然后merge的时候，每一层的所有元素都要排一次序，所以每层是O(n)
  
    根据recursion tree，我们有logn层，所以merge是O(nlogn)
  
    总和是O(n + nlogn)
  
SC = O(n)

    只用了一个长度为array.length的array
















