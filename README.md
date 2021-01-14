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
