### Principles of Binary Search
1. search space must decrease after each interation
2. target should not be roled out accidentally, be careful of Left and Right

### 1. Classic Binary Search

    Example: array[7] 1 2 3 4 5 6 7 whether target = 4 is in this array or not.

    if the target is in this array, return the index
    
    if not, return -1
    
   Java

```java
    public class solution {
        public int binarySearch(int[] array, int target) {
            if (array == null || array.length == 0) {
                return -1;
            }
            int left = 0;
            int right = array.length - 1;
            // 'left <= right' because even left 1 element we still need to check it
            while (left <= right) {
                // 'mid' here is to prevent overflow
                // 'var mid' inside the while loop
                int mid = left + (right - left) / 2;
                if (array[mid] == target) {
                    return mid;
                } else if (array[mid] < target) {
                // 'left = mid + 1' is better because we do not need to consider array[mid] anymore
                    left = mid + 1;
                } else {
                // same reason shown above
                    right = mid - 1;
                }
            }
            return -1;
        }
    }
    // TC = O(log n)
    // SC = O(1)
```

   Python

``` python
    class Solution(object):
        def binarySearch(slef, array, target):
            left, right = 0, len(array) - 1
            while left <= right:
            # in python '//' is floor division
                mid = left + (right - left) // 2
                if array[mid] == target:
                    return mid
                elif array[mid] > target:
                    right = mid - 1
                else:
                    left = mid + 1
            return - 1
                    
```

### 2. Binary Search a 2D matrix

2D matrix, sorted on each row, first element of next row is larger(or equal) to the last element of previous row
now giving a target number, return true or false to indicate if the target is in the matrix

```java
    class Solution {
        public boolean searchMatrix(int[][] matrix, int target) {
            if (matrix.length == 0 || matrix[0].length == 0) {
                return false;
            }
            int col = matrix[0].length;
            int row = matrix.length;
            int left = 0;
            int right = row * col - 1;
            while (left <= right) {
                int mid = left + (right - left) / 2;
                // notice how to convert mid to the row and col index
                if (matrix[mid / col][mid % col] == target) {
                    return true;
                } else if (matrix[mid / col][mid % col] > target) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            }
            return false;
        }
}
TC = O(log m*n)
SC = O(1)
```

### 3. Closet Element to Target

How to find an element in the array that is closest to the target number?

For example: target = 4
            int a[5] = {1, 2, 3,(4) 8, 9}
            return the index of the closest element
            
```java
    public class Solution {
        public int closest(int[] array, int target) {
            if (array == null || array.length == 0) {
                return -1;
            }
            int left = 0;
            int right = array.length - 1;
            // here the loop stop condition is 'left < right -1'
            // 'left < right' or 'left <= right' are wrong
            while (left < right - 1) {
                int mid = left + (right - left) / 2;
                if (array[mid] == target) {
                    return mid;
                } else if (array[mid] > target) {
                // here 'right' and 'left' equal to 'mid'
                // not 'mid - 1' or 'mid + 1'
                // because we need to check if array[mid] is the closest element
                // the target should not be roled out!!!
                    right = mid;
                } else {
                    left = mid;
                }
            }
            if (Math.abs(array[left] - target) < Math.abs(array[right] - target)) {
                return left;
            } else {
                return right;
            }
        }
    }
```

### 4. First Target

How to return the index of the first occurrence of an element, for example 5?

A[7] = {4, 5, 5, 5, 5, 5, 5}

if target is not in the array, return -1

otherwise, return the index

```java
    public class Solution {
        public int firstOccur(int[] array, int target) {
            if (array == null || array.length == 0) {
                return -1;
            }
            int left = 0;
            int right = array.length - 1;
            while (left < right - 1) {
                int mid = left + (right - left) / 2;
                // since we need to find the first target
                // we should narrow the search space by moving right pointer
                if (array[mid] == target) {
                    right = mid;
                } else if (array[mid] < target) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
            if (array[left] == target) {
                return left;
            }
            if (array[right] == target) {
                return right;
            }
            return -1;
        }
    }
```


### 5. Last Target

The code is almost the same.

Here are the modifications:

    if (array[mid] == target) {
        left = mid;
    }
    
out of the loop, check right first
    
    if (array[right] == target) {
        return right;
    }
    if (array[left] == target) {
        return left;
    }


### 6. Closest K elements
given a target, a non-negative K and a sorted array in ascending order.
find the k closest numbers in the array

```java
    public class KClosest{
        public int[] class kClosest(int[] array, int target, int k) {
            int[] result = new int[k];
            
            int left = 0;
            int right = array.length - 1;
            // find the right and left pointers that closest to the target
            while (left < right - 1) {
                int mid = left + (right - left) / 2;
                if (array[mid] <= target) {
                    left = mid;
                } else {
                    right = mid;
                }
            }
            // only when right pointer is out of bound
            // and the value of left pointer is smaller than right pointer
            // we move left pointer
            for (int i = 0; i < k; i++) {
                if (right >= array.length || left >= 0 && Math.abs(array[left] - target) 
                <= Math.abs(array[right] - target)) {
                    result[i] = array[left--];
                } else {
                    result[i] = array[right++];
                }
            }
            return result;
        }
    }
```


### 7. Smallest element is larger than target

input[n] = { 1 3 4 5 8 9 } target = 7, return index of 8

```java
    public class Solution{
        public int smallestElementLargerThanTarget(int[] array, int target) {
            if (array == null || array.length == 0) {
                return -1;
            }
            int left = 0;
            int right = array.length - 1;
            while (left < right - 1) {
                if (array[mid] <= target) {
                    left = mid + 1;
                } else {
                    right = mid;
                }
            }
            if (array[left] > target) {
                return left;
            }
            if (array[right] > target) {
                return right;
            }
            return -1;
        }
    }
```

### 8. K-th smallest in two sorted Arrays
A[] = {2 6 7 10 13}
B[] = {1 3 4 13 20 29}
k = 5
output = 6

依然使用binary search的思想：每次搜索空间减半
1. 因为是在两个array里面找第k位最小的值
   所以我们可以分别在a和b里比较两个array对应的array[k/2-1]的大小
   然后把小的那个array的前k/2个数字舍去
2. 因为题目要求是找第K个最小的值，所以一定不在比完大小后
   小的那个array的k/2里
3. 根据这样的思路就可以完成搜索
   

```java
    public class Solution {
      public int kth(int[] a, int[] b, int k) {
        return helper(a, 0, b, 0, k);
        } 
      private int helper(int[] a, int aleft, int[] b, int bleft, int k) {
        if (aleft >= a.length) {
          return b[bleft + k - 1];
        }
        if (bleft >= b.length) {
          return a[aleft + k - 1];
        }
        if (k == 1) {
          return Math.min(a[aleft], b[bleft]);
        }

        int amid = aleft + k/2 - 1;
        int bmid = bleft + k/2 - 1;

        int aval = amid >= a.length ? Integer.MAX_VALUE : a[amid];
        int bval = bmid >= b.length ? Integer.MAX_VALUE : b[bmid];

        if (aval > bval) {
          return helper(a, aleft, b, bmid + 1, k - k/2);
        } else {
          return helper(a, amid + 1, b, bleft, k - k/2);
        }
      }
    }
```

### 9. binary search with unknown size

```java
    public int search(Dictionary dict, int target) {
    // 首先找到target对应的范围
    // 然后在这个小范围内进行binary search
        if (dict == null) {
            return -1;
        }

        int left = 0;
        int right = 1;
        while (dict.get(right) != null && dict.get(right) < target) {
            left= right;
            right = 2 * right;
        }
    return binary(dict, target, left, right);
  }

  public int binary(Dictionary dict, int target, int left, int right) {
    while (left <= right) { 
      int mid = left + (right - left) / 2;

      if (dict.get(mid) == null || dict.get(mid) > target){
        right = mid - 1;
      } else if (dict.get(mid) < target) {
        left = mid + 1;
      } else {
        return mid;
      }
    }
    return -1;
  }
```






























