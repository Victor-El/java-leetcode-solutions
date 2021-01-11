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
