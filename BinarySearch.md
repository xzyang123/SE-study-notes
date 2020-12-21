### 1. Classic Binary Search

    Example: array[7] 1 2 3 4 5 6 7 whether target = 4 is in this array or not.

    if the target is in this array, return the index
    
    if not, return -1

```java
    // Java
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

``` python
    class Solution(object):
        def binarySearch(slef, array, target):
            left = 0
            right = len(array) - 1
```










































