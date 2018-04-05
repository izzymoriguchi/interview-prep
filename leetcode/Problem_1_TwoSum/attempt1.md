## 1. Two Sum

### Description

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

### My performance
- Came up with the approach in 6 mins
- Implemented it within 7 mins

### My thought process/approach
- Approach 1: 
	- Use 2 nested loops, find all possible pairs from the array, and sum them up and check if they are equal. If they are, return a array of the pair
	- The time complexity of this approach is O(n^2), so we should optimize.

- Approach 2:
	- Create a hashmap --> use this to store (target - item) as a key and index of item as a value.
	- Loop through nums array, for each item, check if the item is in the hashmap.
  		- If the map contains the item, get the value (index) from the map and then return the pair as a array.
  		- If it doesn't contain the item, then store target - item as key and index as value.

### Complexity analysis
- Time complexity : O(N)
- space complexity: O(N)
  
### My solution/attempt

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(nums[i])) {
                return new int[] {map.get(nums[i]), i};
            }
            map.put(target - nums[i], i);
        }
        return new int[0];
    }
}
```

### Solution
Solution on the official solution

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[] { map.get(complement), i };
        }
        map.put(nums[i], i);
    }
    throw new IllegalArgumentException("No two sum solution");
}
```

### Lessons learned
- In my approach I stored target - nums[i] as a key whereas the solution uses nums[i] as key, but both work in the same way. 
- I wasn't sure about what to return at the end, but it's better to throw a exception than just returning a empty array. 