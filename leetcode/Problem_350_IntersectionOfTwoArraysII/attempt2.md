## 350. Intersection of Two Arrays II

### Description

Given two arrays, write a function to compute their intersection.

Example:

Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2, 2].

Note:

Each element in the result should appear as many times as it shows in both arrays.

The result can be in any order.

Follow up:
What if the given array is already sorted? How would you optimize your algorithm?

What if nums1's size is small compared to nums2's size? Which algorithm is better?

What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

### My performance
- Came up with the approach in 7 mins
- Implemented it within 10 mins

### My thought process/approach
- Create a hashmap to store a the item as a key and the number of occurrence as value
- Iterate over the nums1 array and put item in the map and update the count (the value the map) as we iterate.
- Iterate over the nums2 array check if the current item exists in the map.
    - If the map contains the current element and the count(value in map) is not zero, add the elem to the output and decrement the corresponding count(value in the map)
    - If it doesn't contain the current element, then no nothing and keep iterating

### Complexity analysis
- Time complexity : O(N + M)
- space complexity: O(N + M)
  
### My solution/attempt

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        HashMap<Integer, Integer> map = new HashMap<>();
        ArrayList<Integer> out = new ArrayList<>();
        for (int i = 0; i < nums1.length; i++) {
            if (map.containsKey(nums1[i])) {
                map.put(nums1[i], map.get(nums1[i]) + 1);
            }
            map.put(nums1[i], 1);
        }
        
        for (int i = 0; i < nums2.length; i++) {
            int item = nums2[i];
            if (map.containsKey(item) && map.get(item) > 0) {
                out.add(item);
                map.put(item, map.get(item) - 1);
            }
        }
        
        int[] output = new int[out.size()];
        for (int i = 0; i < output.size(); i++) {
            output[i] = out.get(i);
        }
        return output;
    }
}
```
