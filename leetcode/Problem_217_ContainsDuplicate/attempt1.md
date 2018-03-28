## 217. Contains Duplicate

### Description

Given an array of integers, find if the array contains any duplicates. 
Your function should return true if any value appears at least twice in the array, 
and it should return false if every element is distinct.

### My performance
- Came up with the approach within 30 seconds
- Implemented it within 4 mins

### My thought process/approach
- Create a hash table, store the value each time when iterating
- If the set contains an item, return true
- When the loop is done, we can safely return false

### Complexity analysis
- Time complexity : O(N)
- space complexity: O(N)
  
### My solution/attempt

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashSet<Integer> set = new HashSet<>();
        for (int item : nums) {
            if (set.contains(item)) {
                return true;
            }
            set.add(item);
        }
        return false;
    }
}
```

