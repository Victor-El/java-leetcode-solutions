# java-leetcode-solutions
Solutions to java leetcode problems

## Arrays
**Find max consecutive ones**
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

**Find Numbers with Even Number of Digits**

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

**Squares of a Sorted Array**
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
