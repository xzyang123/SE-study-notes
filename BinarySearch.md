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







































