# java-leetcode-solutions
Solutions to java leetcode problems

## Arrays
### Find max consecutive ones

Given a binary array, find the maximum number of consecutive 1s in this array.

**Example:**

> Input: [1,1,0,1,1,1] <br>
> Output: 3 <br>
> Explanation: The first two digits or the last three digits are consecutive 1s. <br>
    The maximum number of consecutive 1s is 3.
    
```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int max = 0;
        int counter = 0;
        
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 1) {
                counter++;
                max = counter > max ? counter : max;
            } else {
                counter = 0;
            }
        }
        return max;
    }
}
```

### Find Numbers with Even Number of Digits

Given an array nums of integers, return how many of them contain an even number of digits.

**Example:**

> Input: nums = [12,345,2,6,7896] <br>
> Output: 2 <br>
> Explanation: <br>
> 12 contains 2 digits (even number of digits). <br>
> 345 contains 3 digits (odd number of digits). <br>
> 2 contains 1 digit (odd number of digits). <br>
> 6 contains 1 digit (odd number of digits). <br>
> 7896 contains 4 digits (even number of digits). <br> 
> Therefore only 12 and 7896 contain an even number of digits. <br>

```java
class Solution {
    public int findNumbers(int[] nums) {
        
        int numberOfEvenDigitsNumbers = 0;
        
        for (int i = 0; i < nums.length; i++) {
            
            int numberOfDigits = 0;
            int dividend = nums[i];
            
            while (true) {
                dividend = dividend / 10;
                numberOfDigits++;
                System.out.println(dividend);
                if (dividend == 0) {
                    if (numberOfDigits % 2 == 0) {
                        numberOfEvenDigitsNumbers++;
                    }
                    break;
                }
            }
            
        }
        
        return numberOfEvenDigitsNumbers;
    }
}
```

### Squares of a Sorted Array

Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

**Example:**

> Input: nums = [-4,-1,0,3,10] <br>
> Output: [0,1,9,16,100] <br>
> Explanation: After squaring, the array becomes [16,1,0,9,100]. <br>
> After sorting, it becomes [0,1,9,16,100]. <br>

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            nums[i] = (int) Math.pow(nums[i], 2);
        }
        return insertionSort(nums);
    }
    
    int[] insertionSort(int[] nums) {
        
        for (int i = 1; i < nums.length; i++) {
            int current = nums[i];
            int j = i - 1;
            while (j >= 0 && nums[j] > current) {
                nums[j + 1] = nums[j];
                j--;
            }
            nums[j + 1] = current;
        }
        
        return nums;
    }
}
```
### Duplicate Zeros

Given a fixed length array arr of integers, duplicate each occurrence of zero, shifting the remaining elements to the right.

Note that elements beyond the length of the original array are not written.

Do the above modifications to the input array in place, do not return anything from your function.

**Example:**
> Input: [1,0,2,3,0,4,5,0] <br>
> Output: null <br>
> Explanation: After calling your function, the input array is modified to: [1,0,0,2,3,0,0,4]

```java
class Solution {
    public void duplicateZeros(int[] arr) {
        for (int i = 0; i < arr.length; i++) {
            
            if (arr[i] == 0 && i < arr.length - 1) {
                for (int j = arr.length - 1; j > i + 1; j--) {
                    arr[j] = arr[j - 1];
                }
                arr[i + 1] = arr[i];
                i += 1;
            }
            
        }
    }
}
```

### Merge Sorted Array

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

The number of elements initialized in nums1 and nums2 are m and n respectively. You may assume that nums1 has enough space (size that is equal to m + n) to hold additional elements from nums2.

**Example:**
> Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3 <br>
> Output: [1,2,2,3,5,6] <br>

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        for (int i = m, j = 0; i < nums1.length; i++, j++) {
            nums1[i] = nums2[j];
        }
        insertionSort(nums1);
    }
    
    void insertionSort(int[] nums) {
        for (int i = 1; i < nums.length; i++) {
            int current = nums[i];
            int j = i - 1;
            
            while (j >= 0 && current < nums[j]) {
                nums[j + 1] = nums[j];
                j--;
            }
            nums[j + 1] = current;
        }
    }
}
```

### Remove Element

Given an array nums and a value val, remove all instances of that value in-place and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

**Example:**

> Input: nums = [3,2,2,3], val = 3 <br>
> Output: 2, nums = [2,2] <br>
> Explanation: Your function should return length = 2, with the first two elements of nums being 2. <br>
> It doesn't matter what you leave beyond the returned length. For example if you return 2 with nums = [2,2,3,3] or nums = [2,2,0,0], your answer will be accepted.

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        
        int length = nums.length;
        
        for (int i = 0; i < length; i++) {
            if (nums[i] == val) {
                if (nums[length - 1] == val) {
                    length--;
                    i = i - 1;
                    continue;
                }
                int temp = nums[i];
                nums[i] = nums[length - 1];
                nums[length - 1] = temp;
                length--;
            }
        }
        
        return length;
    }
}
```
### OR

```java
// Ordered solution
class Solution {
    public int removeElement(int[] nums, int val) {
        
        int length = nums.length;
        for (int j = 0; j < nums.length; j++) {
            for (int i = 0; i < length; i++) {
                if (nums[i] == val) {
                    remove(nums, i, length);
                    length--;
                }
            }
        }
        
        return length;
    }
    
    void remove(int[] nums, int pos, int length) {
        for (int i = pos + 1; i < length; i++) {
            nums[i - 1] = nums[i];
        }
    }
}
```

### Removing Duplicates from Sorted Arrays

Given a sorted array nums, remove the duplicates in-place such that each element appears only once and returns the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

**Example:**

> Input: nums = [0,0,1,1,1,2,2,3,3,4] <br>
> Output: 5, nums = [0,1,2,3,4] <br>
> Explanation: Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively. It doesn't matter what values are set beyond the returned length.

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        
        int length = nums.length;
        
        for (int i = 0; i < length; i++) {
            while (i + 1 < length && nums[i] == nums[i + 1]) {
                for (int j = i + 1; j < length; j++) {
                    nums[j - 1] = nums[j];
                }
                length--;
            }
        }
        
        return length;
    }
}
```

### Check if N and its double exist

Given an array arr of integers, check if there exists two integers N and M such that N is the double of M ( i.e. N = 2 * M).

More formally check if there exists two indices i and j such that :

- i != j
- 0 <= i, j < arr.length
- arr[i] == 2 * arr[j]

**Example:**
>Input: arr = [10,2,5,3] <br>
> Output: true <br>
> Explanation: N = 10 is the double of M = 5,that is, 10 = 2 * 5.

```java
class Solution {
    public boolean checkIfExist(int[] arr) {
        boolean nAndItsDoubleExist = false;
        
        for (int i = 0; i < arr.length; i++) {
            
            for (int j = 0; j < arr.length; j++) {
                if (i != j) {
                    if (arr[i] == arr[j] * 2) {
                        nAndItsDoubleExist = true;
                        break;
                    }
                }
            }
            
            if (nAndItsDoubleExist) {
                break;
            }
        }
        
        return nAndItsDoubleExist;
    }
}
```

### Valid Mountain Array

Recall that arr is a mountain array if and only if:

- arr.length >= 3
- There exists some i with 0 < i < arr.length - 1 such that:
    - arr[0] < arr[1] < ... < arr[i - 1] < arr[i]
    - arr[i] > arr[i + 1] > ... > arr[arr.length - 1]


**Examples:**

> Input: arr = [2,1] <br>
> Output: false

> Input: arr = [3,5,5] <br>
> Output: false

> Input: arr = [0,3,2,1] <br>
> Output: true

```java
class Solution {
    public boolean validMountainArray(int[] arr) {
        int peak = 0;
        boolean result = true;
        
        if (arr.length < 3) {
            return false;
        }
        
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] > arr[i - 1]) {
                peak = i;
            } else {
                break;
            }
        }
        
        if (peak >= arr.length - 1 || peak == 0) {
            return false;
        }
        
        for (int i = peak + 1; i < arr.length; i++) {
            
            if (!(arr[i] < arr[i - 1])) {
                result = false;
                break;
            }
        }
        
        return result;
    }
}
```
