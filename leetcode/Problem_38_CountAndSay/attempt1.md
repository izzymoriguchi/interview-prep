## 38. Count and Say

### Description

The count-and-say sequence is the sequence of integers with the first five terms as following:

1.     1
2.     11
3.     21
4.     1211
5.     111221

1 is read off as "one 1" or 11.

11 is read off as "two 1s" or 21.

21 is read off as "one 2, then one 1" or 1211.

Given an integer n, generate the nth term of the count-and-say sequence.

Note: Each term of the sequence of integers will be represented as a string.

### My performance
- Came up with the approach within 5 mins
- Took 30 mins to implement

### My thought process/approach
- Loop from 1 to n
    - Loop through string
        - If prev char is not same as curr char, append to sb
        - If they are the same, increment count
    - After the loop, append the last char with the corresponding count

### Complexity analysis
- Time complexity : O(N * K)
- space complexity: O(1)
  
### My solution/attempt

```java
class Solution {
    public String countAndSay(int n) { 
        String prev = "1";
        int i = 1;
        while (i < n) {
            StringBuilder sb = new StringBuilder();
            int count = 1;
            int size = prev.length(); 
            int j;
            for (j = 1; j < size; j++) {
                if (prev.charAt(j - 1) != prev.charAt(j)) {
                    sb.append(count);
                    sb.append(prev.charAt(j - 1));
                    count = 1;
                } else {
                    count++;
                }
            }
            sb.append(count);
            sb.append(prev.charAt(j - 1));
            prev = sb.toString();
            i++;
        }
        return prev;
    } 
}
```


### Solution
Solution by zhibzhang
https://leetcode.com/problems/count-and-say/discuss/16040/Straightforward-Java-Solution

```java
 public class Solution {
    public String countAndSay(int n) {
        String s = "1";
        for(int i = 1; i < n; i++){
            s = countIdx(s);
        }
        return s;
    }
    
    public String countIdx(String s){
        StringBuilder sb = new StringBuilder();
        char c = s.charAt(0);
        int count = 1;
        for(int i = 1; i < s.length(); i++){
            if(s.charAt(i) == c){
                count++;
            }
            else
            {
                sb.append(count);
                sb.append(c);
                c = s.charAt(i);
                count = 1;
            }
        }
        sb.append(count);
        sb.append(c);
        return sb.toString();
    }
}
```

### Lessons learned
- I can create a separate method for counting and building a new string.