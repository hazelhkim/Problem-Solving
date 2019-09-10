Given a non-empty array of digits representing a non-negative integer, plus one to the integer.
The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.
You may assume the integer does not contain any leading zero, except the number 0 itself.

#### Example 1:
Input: [1,2,3] <br />
Output: [1,2,4] <br />
Explanation: The array represents the integer 123. <br />

#### Example 2:
Input: [4,3,2,1] <br />
Output: [4,3,2,2] <br />
Explanation: The array represents the integer 4321. <br />


## My Answer:

```java

class Solution {
    public int[] plusOne(int[] digits) {
        int index = digits.length - 1;
        digits[index] += 1;
      
        for(int i = index; i > 0; i --) {
            if(digits[i] == 10) {
                digits[i-1] += 1;
                digits[i] = 0;
            }
        }
        if(digits[0] == 10) {
            digits = new int[digits.length + 1];
            digits[0] = 1;
            digits[1] = 0;
        }
        return digits;
    }
}

```
