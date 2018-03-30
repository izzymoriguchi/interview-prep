## 123. Problem Title

### Description

Given an array of integers, every element appears twice except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

### My performance
- Came up with the first approach within 1 mins, and then thought about the bit manipulation approach within a few mins
- Implemented it within 15 mins

### My thought process/approach

nums [1,3,1,3,2] -> outputs 2

- One approach with extra memory:
  - Create a hashmap of Int key and val as int
  - iterate through the array, and if map contains the key, make the value to 0 else add the key value pair
  - after the loop, iterate over the map keys and find non zero value and that is the answer
- Second approach with using bit manuilation:
    ```
    1 -> 0001
    2 -> 0010
    3 -> 0011

    XOR 0001 ^ 0001 = 0000
    1 ^ 3 ^ 1 ^ 3 ^ 2 
    = 0001 ^ 0011 ^ 0001 ^ 0011 ^ 0010 
    = (0001 ^ 0001) ^ (0011 ^ 0011) ^ 0010
    = 0000 ^ 0000 ^ 0010
    = 0010
    = 2
    ```

### Complexity analysis
- First approach:
  - Time complexity : O(N)
  - space complexity: O(N)    
- Second Approach:
  - Time complexity : O(N)
  - space complexity: O(1)
  
### My solution/attempt

```java
class Solution {
    public int singleNumber(int[] nums) {
        int value = nums[0];
        for (int i = 1; i < nums.length; i++) {
            value = value ^ nums[i];
        }
        return value;
    }
}
```