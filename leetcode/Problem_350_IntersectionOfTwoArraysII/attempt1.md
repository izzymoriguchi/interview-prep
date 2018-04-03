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
- Came up with the approach within 10 mins
- Implemented it in 17 mins, but there was a bug in my implementation and did not completed it within 30 mins timeframe.

### My thought process/approach
  - Check size of two arrays, find the smaller array.
  - Create a linked list of longer array
  - Itereate over the small array
    - for each item, search the same item in the linked list, and if found the item, 
    add to the output and remove it from linkedlist

### Complexity analysis
- Time complexity : O(S * L) where S is the size of smaller array and L is the size of larger array
- space complexity: O(L)
  
### My solution/attempt

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        if (nums1.length <= nums2.length) {
            return intersectHelper(nums1, nums2);
        }
        return intersectHelper(nums2, nums1);
    }
    
    public int[] intersectHelper(int[] small, int[] large) {
        LinkedList<Integer> largeList = new LinkedList<>();
        ArrayList<Integer> outputList = new ArrayList<>();
        for (int item : large) {
            largeList.add(item);
        }
        
        for (int i = 0; i < small.length; i++) {
            int currInSmall = small[i];
            Iterator iter = largeList.iterator();
            while (iter.hasNext()) {
                int currItemInLarge = (int) iter.next();
                if (currItemInLarge == currInSmall) {
                    outputList.add(currInSmall);
                    iter.remove();
                }
            }
        }
        
        return outputList.stream().mapToInt(i -> i).toArray();
    }
}
```


### Solution

Solution by VanillaCoke https://leetcode.com/problems/intersection-of-two-arrays-ii/discuss/82241/AC-solution-using-Java-HashMap

```java
public class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        ArrayList<Integer> result = new ArrayList<Integer>();
        for(int i = 0; i < nums1.length; i++)
        {
            if(map.containsKey(nums1[i])) map.put(nums1[i], map.get(nums1[i])+1);
            else map.put(nums1[i], 1);
        }
    
        for(int i = 0; i < nums2.length; i++)
        {
            if(map.containsKey(nums2[i]) && map.get(nums2[i]) > 0)
            {
                result.add(nums2[i]);
                map.put(nums2[i], map.get(nums2[i])-1);
            }
        }
    
       int[] r = new int[result.size()];
       for(int i = 0; i < result.size(); i++)
       {
           r[i] = result.get(i);
       }
    
       return r;
    }
}
```

### Lessons learned
- At first I thought I can't use hashtable because there are duplicate items in both arrays, but I learned we can use HashMap to count the occurrence of each chars in both arrays.
- By using this method, we can optimize the time complexity to be O(S + L)