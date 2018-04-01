## 283. Move Zeroes

### Description

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].

Note:
You must do this in-place without making a copy of the array.
Minimize the total number of operations.

### My performance
- Came up with the approach within 5 mins
- Implemented it within 15 mins

### My thought process/approach
- Have 2 pointers, p1 pointing the position of the first zero in the array, and p2 for 
iterating the whole array.
- First, find the zero index for p1, and set p1 and p2
- Loop through the array with p2 and
	- If p2 finds non zero value, we swap with value in p2 with p1. Then increment both pointers by 1
- Keep iterating with p2

### Complexity analysis
- Time complexity : O(N)
- space complexity: O(1)
  
### My solution/attempt

```java
class Solution {
    public void moveZeroes(int[] nums) {
        if (nums.length < 2) {
            return;
        }
    
        int n = nums.length;
        int i = 0;
        
        while (i < n && nums[i] != 0) { 
            i++;
        }
        int p1 = i; // p1 is the index of first zero in the array
        int p2 = p1 + 1; 
        while (p2 < n) {
            if (nums[p2] != 0) {
                int temp = nums[p1];
                nums[p1] = nums[p2];
                nums[p2] = temp;
                p1++;
            }
            p2++;
        }
    }
}
```

### Solution

Solution by Kurteck
https://leetcode.com/problems/move-zeroes/discuss/72011/Simple-O(N)-Java-Solution-Using-Insert-Index

``` java
// Shift non-zero values as far forward as possible
// Fill remaining space with zeros

public void moveZeroes(int[] nums) {
    if (nums == null || nums.length == 0) return;        

    int insertPos = 0;
    for (int num: nums) {
        if (num != 0) nums[insertPos++] = num;
    }        

    while (insertPos < nums.length) {
        nums[insertPos++] = 0;
    }
}
```

### Lessons learned
- I should check the corner case when nums is null
- From the solution, I learned that I could have just looked non zero values from the array and shift all the elements to the left. 