# DSA

1. [Chapter 1: Arrays](#chapter1)
	- [Chapter 1 - Part 1: Static Arrays](#chapter1part1)
      - [Chapter 1 - Part 1.1: Remove Duplicates From Sorted Array](#chapter1part1.1)
      - [Chapter 1 - Part 1.2: Remove Element](#chapter1part1.2)
    - [Chapter 1 - Part 2: Dynamic Arrays](#chapter1part2)
      - [Chapter 1 - Part 2.1: Concatenation of Array](#chapter1part2.1)
    - [Chapter 1 - Part 3: Stacks](#chapter1part3)
      - [Chapter 1 - Part 3.1: Valid Parentheses](#chapter1part3.1)
      - [Chapter 1 - Part 3.2: Min Stack](#chapter1part3.2)
3. [Chapter 4: Recursion](#chapter4)
    - [Chapter 4 - Part 1: Generate Parentheses(Recursion with Backtracking)](#chapter4part1)

## <a name="chapter1"></a>Chapter 1: Arrays

### <a name="chapter1part1"></a>Chapter 1 - Part 1: Static Arrays

**Time Complexity**

| Operation | Big-O Time | Notes
| :---: | :---: | :---: |
| Access | O(1) | |
| Insertion | O(1)∗ | O(n) if insertion in the middle since shifting will be required |
| Deletion | O(1)∗ | O(n) if insertion in the middle since shifting will be required |

```py
# Insert n into arr at the next open position.
# Length is the number of 'real' values in arr, and capacity
# is the size (aka memory allocated for the fixed size array).
def insertEnd(arr, n, length, capacity):
    if length < capacity:
        arr[length] = n

# Remove from the last position in the array if the array
# is not empty (i.e. length is non-zero).
def removeEnd(arr, length):
    if length > 0:
        # Overwrite last element with some default value.
        # We would also consider the length to be decreased by 1.
        arr[length - 1] = 0

# Insert n into index i after shifting elements to the right.
# Assuming i is a valid index and arr is not full.
def insertMiddle(arr, i, n, length):
    # Shift starting from the end to i.
    for index in range(length - 1, i - 1, -1):
        arr[index + 1] = arr[index]
    
    # Insert at i
    arr[i] = n

# Remove value at index i before shifting elements to the left.
# Assuming i is a valid index.
def removeMiddle(arr, i, length):
    # Shift starting from i + 1 to end.
    for index in range(i + 1, length):
        arr[index - 1] = arr[index]
    # No need to 'remove' arr[i], since we already shifted

def printArr(arr, capacity):
    for i in range(capacity):
        print(arr[i])

```

```java
public class StaticArray {

    // Insert n into arr at the next open position.
    // Length is the number of 'real' values in arr, and capacity
    // is the size (aka memory allocated for the fixed size array).
    public void insertEnd(int[] arr, int n, int length, int capacity) {
        if (length < capacity) {
            arr[length] = n;
        }
    }    
            
    // Remove from the last position in the array if the array
    // is not empty (i.e. length is non-zero).
    public void removeEnd(int[] arr, int length) {
        if (length > 0) {
            // Overwrite last element with some default value.
            // We would also consider the length to be decreased by 1.
            arr[length - 1] = 0;
            length--;
        }
    }        

    // Insert n into index i after shifting elements to the right.
    // Assuming i is a valid index and arr is not full.
    public void insertMiddle(int[] arr, int i, int n, int length) {
        // Shift starting from the end to i.
        for (int index = length - 1; index > i - 1; index--) {
            arr[index + 1] = arr[index];
        }
        // Insert at i
        arr[i] = n;
    }

    // Remove value at index i before shifting elements to the left.
    // Assuming i is a valid index.
    public void removeMiddle(int[] arr, int i, int length) {
        // Shift starting from i + 1 to end.
        for (int index = i + 1; index < length; index++) {
            arr[index - 1] = arr[index];
        } 
        // No need to 'remove' arr[i], since we already shifted
    }

    public void printArr(int[] arr, int length) {
        for (int i = 0; i < length; i++) {
            System.out.print(arr[i] + " ");
        }      
        System.out.println();
    }
}    
```

#### <a name="chapter1part1.1"></a>Chapter 1 - Part 1.1: Remove Duplicates From Sorted Array

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

```py
class Solution:
    def removeDuplicates(self, nums: list[int]) -> int:
        unique = sorted(set(nums))
        nums[:len(unique)] = unique
        return len(unique)
```

```java
public class Solution {
    public int removeDuplicates(int[] nums) {
        TreeSet<Integer> unique = new TreeSet<>();
        for (int num : nums) {
            unique.add(num);
        }
        int i = 0;
        for (int num : unique) {
            nums[i++] = num;
        }
        return unique.size();
    }
}
```

#### <a name="chapter1part1.2"></a>Chapter 1 - Part 1.2: Remove Element

You are given an integer array nums and an integer val. Your task is to remove all occurrences of val from nums in-place.

After removing all occurrences of val, return the number of remaining elements, say k, such that the first k elements of nums do not contain val.

Note:

- The order of the elements which are not equal to val does not matter.
- It is not necessary to consider elements beyond the first k positions of the array.
- To be accepted, the first k elements of nums must contain only elements not equal to val.

Return k as the final result.

**Example 1:**

```
Input: nums = [1,1,2,3,4], val = 1

Output: [2,3,4]
```

Explanation: You should return k = 3 as we have 3 elements which are not equal to val = 1.

**Example 2:**

```
Input: nums = [0,1,2,2,3,0,4,2], val = 2

Output: [0,1,3,0,4]
```

Explanation: You should return k = 5 as we have 5 elements which are not equal to val = 2.

Constraints:

- 0 <= nums.length <= 100
- 0 <= nums[i] <= 50
- 0 <= val <= 100

**Solution - Two Pointers**

```py
from typing import List


class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        left_point = 0
        for right_point in range(len(nums)):
            if nums[right_point] != val:
                nums[left_point] = nums[right_point]
                left_point = left_point + 1
        return left_point


test_1 = [1,1,2,3,4]
test_2 = [0,1,2,2,3,0,4,2]
k_1 = Solution().removeElement(test_1, 1)
k_2 = Solution().removeElement(test_2, 2)
print(k_1) # 3
print(test_1[:k_1]) # [2, 3, 4]
print(k_2) # 5
print(test_2[:k_2]) # [0, 1, 3, 0, 4]
```

```java
public class Solution {
    public int removeElement(int[] nums, int val) {
        int k = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != val) {
                nums[k++] = nums[i];
            }
        }
        return k;
    }
}
```

**Solution - Brute Force**

```py
class Solution:
    def removeElement(self, nums: list[int], val: int) -> int:
        tmp = []
        for num in nums:
            if num == val:
                continue
            tmp.append(num)
        for i in range(len(tmp)):
            nums[i] = tmp[i]
        return len(tmp)
```

```java
public class Solution {
    public int removeElement(int[] nums, int val) {
        List<Integer> tmp = new ArrayList<>();
        for (int num : nums) {
            if (num != val) {
                tmp.add(num);
            }
        }
        for (int i = 0; i < tmp.size(); i++) {
            nums[i] = tmp.get(i);
        }
        return tmp.size();
    }
}
```

### <a name="chapter1part2"></a>Chapter 1 - Part 2: Dynamic Arrays

**Time Complexity**

| Operation | Big-O Time | Notes
| :---: | :---: | :---: |
| Access | O(1) | |
| Insertion | O(1)∗ | O(n) if insertion in the middle since shifting will be required |
| Deletion | O(1)∗ | O(n) if insertion in the middle since shifting will be required |

```py
# Python arrays are dynamic by default, but this is an example of resizing.
class Array:
    def __init__(self):
        self.capacity = 2
        self.length = 0
        self.arr = [0] * 2 # Array of capacity = 2

    # Insert n in the last position of the array
    def pushback(self, n):
        if self.length == self.capacity:
            self.resize()
            
        # insert at next empty position
        self.arr[self.length] = n
        self.length += 1

    def resize(self):
        # Create new array of double capacity
        self.capacity = 2 * self.capacity
        newArr = [0] * self.capacity 
        
        # Copy elements to newArr
        for i in range(self.length):
            newArr[i] = self.arr[i]
        self.arr = newArr
        
    # Remove the last element in the array
    def popback(self):
        if self.length > 0:
            self.length -= 1
    
    # Get value at i-th index
    def get(self, i):
        if i < self.length:
            return self.arr[i]
        # Here we would throw an out of bounds exception

    # Insert n at i-th index
    def insert(self, i, n):
        if i < self.length:
            self.arr[i] = n
            return
        # Here we would throw an out of bounds exception       

    def print(self):
        for i in range(self.length):
            print(self.arr[i])
        print()
```

```java
public class DynamicArray {
    int capacity;
    int length;
    int[] arr;

    public DynamicArray() {
        capacity = 2;
        length = 0;
        arr = new int[2];
    }

    // Insert n in the last position of the array
    public void pushback(int n) {
        if (length == capacity) {
            this.resize();
        }
               
        // insert at next empty position
        arr[length] = n;
        length++;
    }

    public void resize() {
        // Create new array of double capacity
        capacity = 2 * capacity;
        int[] newArr = new int[capacity]; 
        
        // Copy elements to newArr
        for (int i = 0; i < length; i++) {
            newArr[i] = arr[i];
        }
        arr = newArr;
    }  

    // Remove the last element in the array
    public void popback() {
        if (length > 0) {
            length--;
        }  
    }     

    // Get value at i-th index
    public int get(int i) {
        if (i < length) {
            return arr[i];
        }    
        // Here we would throw an out of bounds exception
        return -1;
    }    

    // Insert n at i-th index
    public void insert(int i, int n) {
        if (i < length) {
            arr[i] = n;
            return;
        }    
        return;
        // Here we would throw an out of bounds exception  
    }        

    public void print() {
        for (int i = 0; i < length; i++) {
            System.out.println(arr[i]);
        }
    }
} 
```

#### <a name="chapter1part2.1"></a>Chapter 1 - Part 2.1: Concatenation of Array

You are given an integer array nums of length n. Create an array ans of length 2n where ans[i] == nums[i] and ans[i + n] == nums[i] for 0 <= i < n (0-indexed).

Specifically, ans is the concatenation of two nums arrays.

Return the array ans.

**Example 1:**

```
Input: nums = [1,4,1,2]

Output: [1,4,1,2,1,4,1,2]
```

**Example 2:**

```
Input: nums = [22,21,20,1]

Output: [22,21,20,1,22,21,20,1]
```

**Solution - Iteration**

Time complexity: O(n)
Space complexity: O(1)

```py
from typing import List


class Solution:
    def getConcatenation(self, nums: List[int]) -> List[int]:
        ans = nums
        for right_pointer in range(0, len(nums)):
            ans.append(nums[right_pointer])
        return ans


nums_test_1 = [1, 4, 1, 2]
nums_test_2 = [22, 21, 20, 1]
ans_1 = Solution().getConcatenation(nums_test_1)
ans_2 = Solution().getConcatenation(nums_test_2)
print(ans_1)  # [1, 4, 1, 2, 1, 4, 1, 2]
print(ans_2)  # [22, 21, 20, 1, 22, 21, 20, 1]

```

```java
public class Solution {
    public int[] getConcatenation(int[] nums) {
        int n = nums.length;
        int[] ans = new int[2 * n];
        for (int i = 0; i < n; i++) {
            ans[i] = ans[i + n] = nums[i];
        }
        return ans;
    }
}
```

### <a name="chapter1part3"></a>Chapter 1 - Part 3: Stacks

**Time Complexity**

| Operation | Big-O Time | Notes
| :---: | :---: | :---: |
| Push | O(1) | |
| Pop | O(1)∗ | Check if the stack is empty first |
| Peek / Top | O(1)∗ | Retrieves without removing |

```py
# Implementing a stack is trivial using a dynamic array
# (which we implemented earlier).
class Stack:
    def __init__(self):
        self.stack = []

    def push(self, n):
        self.stack.append(n)

    def pop(self):
        return self.stack.pop()

	def peek(self):
    return self.stack[-1]
```

```py
import java.util.ArrayList;

// Implementing a stack is trivial using a dynamic array
// (which we implemented earlier).
public class Stack {

    ArrayList<Integer> stack = new ArrayList<Integer>();

    public Stack() {   
    }

    public void push(int n) {
        stack.add(n);
    }

    public int pop() {
        return stack.remove(stack.size() - 1);
    }

    public int size() {
        return stack.size();
    }

	public int peek() {
    return stack.get(stack.size() - 1);
	}

}
```


#### <a name="chapter1part3.1"></a>Chapter 1 - Part 3.1: Valid Parentheses

You are given a string s consisting of the following characters: '(', ')', '{', '}', '[' and ']'.

The input string s is valid if and only if:

- Every open bracket is closed by the same type of close bracket.
- Open brackets are closed in the correct order.
- Every close bracket has a corresponding open bracket of the same type.

Return true if s is a valid string, and false otherwise.

**Example 1:**

```
Input: s = "[]"

Output: true
```

**Example 2:**

```
Input: s = "([{}])"

Output: true
```

**Example 3:**

```
Input: s = "[(])"

Output: false
```

Explanation: The brackets are not closed in the correct order.

Constraints:

- 1 <= s.length <= 1000

**Solution - Stack**

```py
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        for parenthese in s:
            if parenthese == '(':
                stack.append(parenthese)
            elif parenthese == '[':
                stack.append(parenthese)
            elif parenthese == '{':
                stack.append(parenthese)
            elif parenthese == ')':
                if stack and stack[-1] == '(':
                    stack.pop()
                else:
                    return False
            elif parenthese == ']':
                if stack and stack[-1] == '[':
                    stack.pop()
                else:
                    return False
            elif parenthese == '}':
                if stack and stack[-1] == '{':
                    stack.pop()
                else:
                    return False
        if stack:
            return False
        else:
            return True
```

```java
public class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        java.util.Map<Character, Character> closeToOpen = new java.util.HashMap<>();
        closeToOpen.put(')', '(');
        closeToOpen.put(']', '[');
        closeToOpen.put('}', '{');

        for (char c : s.toCharArray()) {
            if (closeToOpen.containsKey(c)) {
                if (!stack.isEmpty() && stack.peek() == closeToOpen.get(c)) {
                    stack.pop();
                } else {
                    return false;
                }
            } else {
                stack.push(c);
            }
        }
        return stack.isEmpty();
    }
}
```

#### <a name="chapter1part3.2"></a>Chapter 1 - Part 3.2: Min Stack

Design a stack class that supports the push, pop, top, and getMin operations.

- MinStack() initializes the stack object.
- void push(int val) pushes the element val onto the stack.
- void pop() removes the element on the top of the stack.
- int top() gets the top element of the stack.
- int getMin() retrieves the minimum element in the stack.

Each function should run in O(1) time.

**Example 1:**

```
Input: ["MinStack", "push", 1, "push", 2, "push", 0, "getMin", "pop", "top", "getMin"]

Output: [null,null,null,null,0,null,2,1]

Explanation:
MinStack minStack = new MinStack();
minStack.push(1);
minStack.push(2);
minStack.push(0);
minStack.getMin(); // return 0
minStack.pop();
minStack.top();    // return 2
minStack.getMin(); // return 1
```

**Constraints:**

- ```-2^31 <= val <= 2^31 - 1.```
- pop, top and getMin will always be called on non-empty stacks.

****Solution - Two Stacks**

```py
class MinStack:

    def __init__(self):
        self.min_stack = []
        self.stack = []

    def push(self, val: int) -> None:
        if len(self.stack) == 0:
            self.min_stack.append(val)
            self.stack.append(val)
        else:
            if self.min_stack[-1] >= val:
                self.min_stack.append(val)
                self.stack.append(val)
            else:
                self.stack.append(val)

    def pop(self) -> None:
        if len(self.stack) > 0:
            value = self.stack.pop()
            if value <= self.min_stack[-1]:
                self.min_stack.pop()

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.min_stack[-1]


commands = ["MinStack", "push", 5, "push", 0, "push", 2, "push", 4, "getMin", "pop", "getMin", "pop", "getMin"]
commands_2 = ["MinStack", "push", 1, "push", 2, "push", 0, "getMin", "pop", "top", "getMin"]
results = []
minStack = None
for i, command in enumerate(commands_2):
    if command == 'MinStack':
        minStack = MinStack()
        results.append(None)
    elif command == 'push':
        minStack.push(commands_2[i + 1])
        results.append(None)
    elif command == 'pop':
        minStack.pop()
        results.append(None)
    elif command == 'top':
        results.append(minStack.top())
    elif command == 'getMin':
        results.append(minStack.getMin())
print(results) # [None, None, None, None, 0, None, 2, 1]
```

```java
public class MinStack {
    private Stack<Integer> stack;
    private Stack<Integer> minStack;

    public MinStack() {
        stack = new Stack<>();
        minStack = new Stack<>();
    }

    public void push(int val) {
        stack.push(val);
        if (minStack.isEmpty() || val <= minStack.peek()) {
            minStack.push(val);
        }
    }

    public void pop() {
        if (stack.isEmpty()) return;
        int top = stack.pop();
        if (top == minStack.peek()) {
            minStack.pop();
        }
    }

    public int top() {
        return stack.peek();
    }

    public int getMin() {
        return minStack.peek();
    }
}
```

## <a name="chapter4"></a>Chapter 4: Recursion

### <a name="chapter4part1"></a>Chapter 4 - Part 1: Generate Parentheses(Recursion with Backtracking)

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
