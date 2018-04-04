## 66. Plus One

### Description

Given a non-negative integer represented as a non-empty array of digits, plus one to the integer.

You may assume the integer do not contain any leading zero, except the number 0 itself.

The digits are stored such that the most significant digit is at the head of the list.

### My performance
- Came up with my approach within 9 mins
- Implemented it within 19 mins

### My thought process/approach
- Create ArrayList to store the output
- Traverse from the end. Add 1 to the least significant digit
- If the sum is 10, keep traversing.
- If the sum is less than 10, keep traversing and add the digit to array list.

### Complexity analysis
- Time complexity : O(N)
- space complexity: O(N)
  
### My solution/attempt

```java
class Solution {
    public int[] plusOne(int[] digits) {
        ArrayList<Integer> list = new ArrayList<>();
        int n = digits.length;
        boolean carry = false;
        
        if (digits[n - 1] + 1 == 10) {
            list.add(0);
            carry = true;
        } else {
            list.add(digits[n - 1] + 1);
        }
        
        for (int i = n - 2; i >= 0; i--) {
            int sum = digits[i];
            if (carry) {
                if (sum + 1 == 10) {
                    list.add(0);
                } else {
                    list.add(sum + 1);
                    carry = false;
                }
            } else {
                list.add(sum);
            }
        }
        
        if (carry) {
            list.add(1);
        }
        
        int[] output = new int[list.size()];
        int counter = 0;
        for (int i = list.size() - 1; i >= 0; i--) {
            output[counter] = list.get(i);
            counter++;
        }
        return output;
    }
}
```

### Solution

Solution by diaa https://leetcode.com/problems/plus-one/discuss/24082/My-Simple-Java-Solution

```java
public int[] plusOne(int[] digits) {
        
    int n = digits.length;
    for(int i=n-1; i>=0; i--) {
        if(digits[i] < 9) {
            digits[i]++;
            return digits;
        }
        
        digits[i] = 0;
    }
    
    int[] newNumber = new int [n+1];
    newNumber[0] = 1;
    
    return newNumber;
}
```

### Lessons learned
- In my implementation, I did some unnecessary things. We need to create a new array only when the most significant digit in the array is 9. 
	- Therefore, I could have just used the original array to update value and return immediately.
	- If non most significant digits are 9, we can just set that value to 0.
	- If we didn't return within the loop, that means the most significant digit was 9, so we need to create a new array with original size + 1.
		- In this case, all digits except for the most significant digit are 0s, so we just need to set the most significant digit to 1 in the new array.