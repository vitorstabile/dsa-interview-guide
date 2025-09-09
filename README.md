# DSA

1. [Chapter 1: Static Arrays](#chapter1)
	- [Chapter 1 - Part 1: Remove Duplicates From Sorted Array](#chapter1part1)
3. [Chapter 2: Recursion](#chapter2)
    - [Chapter 2 - Part 1: Generate Parentheses(Recursion with Backtracking)](#chapter2part1)

## <a name="chapter2"></a>Chapter 1: Static Arrays

#### <a name="chapter1part1"></a>Chapter 1 - Part 1: Remove Duplicates From Sorted Array

You are given an integer array nums sorted in non-decreasing order. Your task is to remove duplicates from nums in-place so that each element appears only once.

After removing the duplicates, return the number of unique elements, denoted as k, such that the first k elements of nums contain the unique elements.

Note:

The order of the unique elements should remain the same as in the original array.
It is not necessary to consider elements beyond the first k positions of the array.
To be accepted, the first k elements of nums must contain all the unique elements.

**Example 1:**

```
Input: nums = [1,1,2,3,4]

Output: [1,2,3,4]
```

Explanation: You should return k = 4 as we have four unique elements.

**Example 2:**

```
Input: nums = [2,10,10,30,30,30]

Output: [2,10,30]
```

Explanation: You should return k = 3 as we have three unique elements.

**Solution - Two Pointers**

Time & Space Complexity
- Time complexity: O(n)
- Space complexity: O(1)

```py
from typing import List


class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        left_pointer = 1
        for right_pointer in range(1, len(nums)):
            if nums[right_pointer] != nums[right_pointer - 1]:
                nums[left_pointer] = nums[right_pointer]
                left_pointer = left_pointer + 1
        return left_pointer

test_1 = [0,0,1,1,1,2,2,3,3,4]
test_2 = [2,10,10,30,30,30]
k_1 = Solution().removeDuplicates(test_1)
k_2 = Solution().removeDuplicates(test_2)
print(k_1) # 5
print(test_1[:k_1]) # [0, 1, 2, 3, 4]
print(k_2) # 3
print(test_2[:k_2]) # [2, 10, 30]
```

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int l = 1;
        for (int r = 1; r < nums.length; r++) {
            if (nums[r] != nums[r - 1]) {
                nums[l++] = nums[r];
            }
        }
        return l;
    }

}


public class Main {

    public static void main(String[] args) {

        Solution solution = new Solution();
        int[] test_1 = {0,0,1,1,1,2,2,3,3,4};
        int[] test_2 = {2,10,10,30,30,30};
        int k_1 = solution.removeDuplicates(test_1);
        int k_2 = solution.removeDuplicates(test_2);
        System.out.println(k_1); // 5
        for (int i = 0; i < k_1; i++) {
            System.out.print(test_1[i] + " "); // 0 1 2 3 4 
        }
        System.out.println();
        System.out.println(k_2); // 3
        for (int i = 0; i < k_2; i++) {
            System.out.print(test_2[i] + " "); // 2 10 30
        }
        System.out.println();

    }

}
```

**Solution - Sorted Set**

## <a name="chapter2"></a>Chapter 2: Recursion

#### <a name="chapter2part1"></a>Chapter 2 - Part 1: Generate Parentheses(Recursion with Backtracking)

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

```
Example 1:

Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
Example 2:

Input: n = 1
Output: ["()"]
 

Constraints:

1 <= n <= 8
```

Explanation:

1. The idea is to add ')' only after valid '('
2. We use two integer variables left & right to see how many '(' & ')' are in the current string
3. If left < n then we can add '(' to the current string
4. If right < left then we can add ')' to the current string

```py
class Solution(object):
    def generateParenthesis(self, n):
        def dfs(left, right, s):
            if len(s) == n * 2:
                res.append(s)
                return

            if left < n:
                dfs(left + 1, right, s + '(')

            if right < left:
                dfs(left, right + 1, s + ')')

        res = []
        dfs(0, 0, '')
        return res


solution = Solution()
print(solution.generateParenthesis(3))
```

For n = 2, the recursion tree will be something like this,

```
								   	(0, 0, '')
								 	    |	
									(1, 0, '(')  
								   /           \
							(2, 0, '((')      (1, 1, '()')
							   /                 \
						(2, 1, '(()')           (2, 1, '()(')
						   /                       \
					(2, 2, '(())')                (2, 2, '()()')
						      |	                             |
					res.append('(())')             res.append('()()')

```

Java Example

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> res = new ArrayList<String>();
        recurse(res, 0, 0, "", n);
        return res;
    }
    
    public void recurse(List<String> res, int left, int right, String s, int n) {
        if (s.length() == n * 2) {
            res.add(s);
            return;
        }
        
        if (left < n) {
            recurse(res, left + 1, right, s + "(", n);
        }
        
        if (right < left) {
            recurse(res, left, right + 1, s + ")", n);
        }
    }
	// See above tree diagram with parameters (left, right, s) for better understanding
}
```
