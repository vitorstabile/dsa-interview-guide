# DSA

1. [Chapter 1: Arrays](#chapter1)
	- [Chapter 1 - Part 1: Static Arrays](#chapter1part1)
      - [Chapter 1 - Part 1.1: Remove Duplicates From Sorted Array](#chapter1part1.1)
      - [Chapter 1 - Part 1.2: Remove Element](#chapter1part1.2)
      - [Chapter 1 - Part 1.3: Contains Duplicate](#chapter1part1.3)
      - [Chapter 1 - Part 1.4: Valid Anagram](#chapter1part1.4)
      - [Chapter 1 - Part 1.5: Two Sum](#chapter1part1.5)
      - [Chapter 1 - Part 1.6: Group Anagrams](#chapter1part1.6)
    - [Chapter 1 - Part 2: Dynamic Arrays](#chapter1part2)
      - [Chapter 1 - Part 2.1: Concatenation of Array](#chapter1part2.1)
    - [Chapter 1 - Part 3: Stacks](#chapter1part3)
      - [Chapter 1 - Part 3.1: Valid Parentheses](#chapter1part3.1)
      - [Chapter 1 - Part 3.2: Min Stack](#chapter1part3.2)
2. [Chapter 2: Linked Lists](#chapter2)
	- [Chapter 2 - Part 1: Singly Linked Lists](#chapter2part1)
	- [Chapter 2 - Part 2: Doubly Linked Lists](#chapter2part2)
	- [Chapter 2 - Part 3: Queues](#chapter2part3)
3. [Chapter 3: Recursion](#chapter3)
    - [Chapter 3 - Part 1: Generate Parentheses(Recursion with Backtracking)](#chapter3part1)

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

#### <a name="chapter1part1.3"></a>Chapter 1 - Part 1.3: Contains Duplicate

Given an integer array nums, return true if any value appears more than once in the array, otherwise return false.

**Example 1:**

```
Input: nums = [1, 2, 3, 3]

Output: true
```

**Example 2:**

```
Input: nums = [1, 2, 3, 4]

Output: false
```

**Solution - Set Lenght**

```py
from typing import List


class Solution:
    def hasDuplicate(self, nums: List[int]) -> bool:
        no_duplicates = set(nums)
        if len(nums) != len(no_duplicates):
            return True
        else:
            return False


solution = Solution()
print(solution.hasDuplicate([1, 2, 3, 3]))  # True
print(solution.hasDuplicate([1, 2, 3, 4]))  # False
print(solution.hasDuplicate([1]))  # False
print(solution.hasDuplicate([1, 1]))  # True
```

```java
public class Solution {
    public boolean hasDuplicate(int[] nums) {
        return Arrays.stream(nums).distinct().count() < nums.length;
    }
}
```

#### <a name="chapter1part1.4"></a>Chapter 1 - Part 1.4: Valid Anagram

Given two strings s and t, return true if the two strings are anagrams of each other, otherwise return false.

An anagram is a string that contains the exact same characters as another string, but the order of the characters can be different.

**Example 1:**

```
Input: s = "racecar", t = "carrace"

Output: true
```

**Example 2:**

```
Input: s = "jar", t = "jam"

Output: false
```

**Solution - Sort**

Time complexity: O(n.logn)
Space complexity: O(n)

```py
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        sorted_s = ''.join(sorted(s))
        sorted_t = ''.join(sorted(t))
        if not sorted_s == sorted_t:
            return False
        else:
            return True

solution = Solution()
print(solution.isAnagram("racecar","carrace"))  # True
print(solution.isAnagram("jar", "jam"))  # False
print(solution.isAnagram("jar", "jarr")) # False
```

```java
public class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }

        char[] sSort = s.toCharArray();
        char[] tSort = t.toCharArray();
        Arrays.sort(sSort);
        Arrays.sort(tSort);
        return Arrays.equals(sSort, tSort);
    }
}
```

**Solution - Map**

```py
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        countS, countT = {}, {}

        for i in range(len(s)):
            countS[s[i]] = 1 + countS.get(s[i], 0)
            countT[t[i]] = 1 + countT.get(t[i], 0)
        return countS == countT
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

#### <a name="chapter1part1.5"></a>Chapter 1 - Part 1.5: Two Sum

**Solution - Brute Force**

Time complexity: O(n^2)
Space complexity: O(1)

```py
from typing import List


class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        solution = []
        for i, first_value in enumerate(nums):
            for j, second_value in enumerate(nums):
                if i == j:
                    continue
                if first_value + second_value == target:
                    solution.append(i)
                    solution.append(j)
                    return solution


nums = [3, 4, 5, 6]
target = 7

nums_2 = [4, 5, 6]
target_2 = 10

nums_3 = [5, 5]
target_3 = 10

print(Solution().twoSum(nums, target)) # [0, 1]
print(Solution().twoSum(nums_2, target_2)) # [0, 2]
print(Solution().twoSum(nums_3, target_3)) # [0, 1]
```

```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] + nums[j] == target) {
                    return new int[]{i, j};
                }
            }
        }
        return new int[0];
    }
}
```

**Solution - HashMap**

Time complexity: O(n)
Space complexity: O(n)

```py
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        prevMap = {}  # val -> index

        for i, n in enumerate(nums):
            diff = target - n
            if diff in prevMap:
                return [prevMap[diff], i]
            prevMap[n] = i
```

```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> prevMap = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {
            int num = nums[i];
            int diff = target - num;

            if (prevMap.containsKey(diff)) {
                return new int[] { prevMap.get(diff), i };
            }

            prevMap.put(num, i);
        }

        return new int[] {};
    }
}
```

#### <a name="chapter1part1.6"></a>Chapter 1 - Part 1.6: Group Anagrams

**Solution - Sorting**

Time complexity: O(n.klogk)
Space complexity: O(n.k)

```py
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        my_hashset = dict()
        for i, str in enumerate(strs):
            sorted_str = ''.join(sorted(str))
            if not my_hashset.get(sorted_str):
                my_hashset[sorted_str] = [i]
            else:
                my_hashset[sorted_str].append(i)
        group = []
        for keys, values in my_hashset.items():
            new_group = []
            for value in values:
                new_group.append(strs[value])
            group.append(new_group)
        return group


strs = ["act", "pots", "tops", "cat", "stop", "hat"]
strs_2 = ["x"]
strs_3 = [""]

print(Solution().groupAnagrams(strs))  # [['act', 'cat'], ['pots', 'tops', 'stop'], ['hat']]
print(Solution().groupAnagrams(strs_2))  # [['x']]
print(Solution().groupAnagrams(strs_3))  # [['']]
```

```java
public class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> res = new HashMap<>();
        for (String s : strs) {
            char[] charArray = s.toCharArray();
            Arrays.sort(charArray);
            String sortedS = new String(charArray);
            res.putIfAbsent(sortedS, new ArrayList<>());
            res.get(sortedS).add(s);
        }
        return new ArrayList<>(res.values());
    }
}
```

**Solution - Hash Table**

Time complexity: O(n.k)
Space complexity: O(n.k)

```py
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        res = defaultdict(list)
        for s in strs:
            count = [0] * 26
            for c in s:
                count[ord(c) - ord('a')] += 1
            res[tuple(count)].append(s)
        return list(res.values())
```

```java
public class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> res = new HashMap<>();
        for (String s : strs) {
            int[] count = new int[26];
            for (char c : s.toCharArray()) {
                count[c - 'a']++;
            }
            String key = Arrays.toString(count);
            res.putIfAbsent(key, new ArrayList<>());
            res.get(key).add(s);
        }
        return new ArrayList<>(res.values());
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

## <a name="chapter2"></a>Chapter 2: Linked Lists

### <a name="chapter2part1"></a>Chapter 2 - Part 1: Singly Linked Lists

**Time Complexity**

| Operation | Big-O Time | Notes
| :---: | :---: | :---: |
| Access | O(n) | |
| Search | O(n)∗ | |
| Insertion | O(1)∗ | Assuming you already have a reference to the node at the desired position. OBS: Example Above |
| Deletion | O(1)∗ | Assuming you already have a reference to the node at the desired position OBS: Example Above |

Why using a index have a time complexity of O(n) and with a reference have a time complexity of O(1)?

Example:

```
HEAD → [10] → [20] → [30] → [40] → [50] → NULL
```

**Case 1: We want to insert 99 before 30 (at index 2).**

- Traverse from HEAD:
  - Index 0 → [10]
  - Index 1 → [20]
  - Stop at index 2 → [30]
- Traversal takes O(n).
- Update pointers:

```
[20] → [99] → [30]
```

 Complexity: traversal O(n) + pointer update O(1) = total O(n).

**Case 2: If we already have a reference to node [20]**

- We don’t traverse at all. We just do:

```
newNode = [99]
newNode.next = node20.next   // points to [30]
node20.next = newNode
```

- Result:

```
HEAD → [10] → [20] → [99] → [30] → [40] → [50] → NULL
```

Complexity: O(1) (just changing two pointers).

```py
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None


class SinglyLinkedList:
    def __init__(self):
        self.head = None
        self.tail = None

    def insert_at_end(self, data):
        new_node = Node(data)
        if self.head is None:
            self.head = new_node
            self.tail = new_node
        else:
            self.tail.next = new_node
            self.tail = new_node

    def insert_at_beginning(self, data):
        new_node = Node(data)
        if self.head is None:
            self.head = new_node
            self.tail = new_node
        else:
            new_node.next = self.head
            self.head = new_node

    def remove_from_front(self):
        if self.head is None:
            return

        if self.head == self.tail:
            self.head = None
            self.tail = None
            return

        self.head = self.head.next

    def remove_from_back(self):
        if self.head is None:
            return

        if self.head == self.tail:
            self.head = None
            self.tail = None
            return

        current = self.head
        while current.next != self.tail:
            current = current.next

        current.next = None
        self.tail = current

    def remove_at_index(self, index):
        if self.head is None:
            return

        if index == 0:
            if self.head == self.tail:
                self.tail = None
            self.head = self.head.next
            return

        current = self.head
        count = 0
        while current and count < index - 1:
            current = current.next
            count += 1

        if current is None or current.next is None:
            return

        if current.next == self.tail:
            self.tail = current
        current.next = current.next.next

    def print_list(self):
        current = self.head
        while current:
            print(current.data, end=" -> ")
            current = current.next
        print("None")


# Example Usage
singly_linked_list = SinglyLinkedList()

print("--- Inserting nodes ---")
singly_linked_list.insert_at_end('John')
singly_linked_list.insert_at_end('Bob')
singly_linked_list.insert_at_beginning('Laila')
singly_linked_list.insert_at_end('Susan')
singly_linked_list.print_list()  # Output: Laila -> John -> Bob -> Susan -> None

print("\n--- Removing from the front ---")
singly_linked_list.remove_from_front()
singly_linked_list.print_list()  # Output: John -> Bob -> Susan -> None

print("\n--- Removing from the back ---")
singly_linked_list.remove_from_back()
singly_linked_list.print_list()  # Output: John -> Bob -> None
```

```java
/*
public class ListNode {
    int val;
    ListNode next;

    public ListNode(int val) {
        this.val = val;
        this.next = null;
    }
}
*/

// Implementation for Singly Linked List
public class SinglyLinkedList {
    ListNode head;
    ListNode tail;

    public SinglyLinkedList() {
        head = new ListNode(-1);
        tail = head;
    }

    public void insertEnd(int val) {
        tail.next = new ListNode(val);
        tail = tail.next; 
    }

    public void remove(int index) {
        int i = 0;
        ListNode curr = head;
        while (i < index && curr != null) {
            i++;
            curr = curr.next;
        }
        
        // Remove the node ahead of curr
        if (curr != null && curr.next != null) {
            if (curr.next == tail) {
                tail = curr;
            }
            curr.next = curr.next.next;
        }
    }

    public void print() {
        ListNode curr = head.next;
        while (curr != null) {
            System.out.print(curr.val + " -> ");
            curr = curr.next;
        }

        System.out.println();
    }
    
}
```

### <a name="chapter2part2"></a>Chapter 2 - Part 2: Doubly Linked Lists

**OBS: Doubly linked lists have the benefit that we can traverse the list in both directions, as opposed to singly linked lists.**

**Time Complexity**

| Operation | Big-O Time | Notes
| :---: | :---: | :---: |
| Access | O(n) | |
| Search | O(n)∗ | |
| Insertion | O(1)∗ | Assuming you already have a reference to the node at the desired position. OBS: Example Above |
| Deletion | O(1)∗ | Assuming you already have a reference to the node at the desired position OBS: Example Above |

Why using a index have a time complexity of O(n) and with a reference have a time complexity of O(1)?

Example:

```
HEAD → [10] → [20] → [30] → [40] → [50] → NULL
```

**Case 1: We want to insert 99 before 30 (at index 2).**

- Traverse from HEAD:
  - Index 0 → [10]
  - Index 1 → [20]
  - Stop at index 2 → [30]
- Traversal takes O(n).
- Update pointers:

```
[20] → [99] → [30]
```

 Complexity: traversal O(n) + pointer update O(1) = total O(n).

**Case 2: If we already have a reference to node [20]**

- We don’t traverse at all. We just do:

```
newNode = [99]
newNode.next = node20.next   // points to [30]
node20.next = newNode
```

- Result:

```
HEAD → [10] → [20] → [99] → [30] → [40] → [50] → NULL
```

Complexity: O(1) (just changing two pointers).

```py
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
        self.prev = None


class DoublyLinkedList:
    def __init__(self):
        self.head = None
        self.tail = None

    def insert_at_end(self, data):
        new_node = Node(data)
        if self.head is None:
            self.head = new_node
            self.tail = new_node
        else:
            self.tail.next = new_node
            new_node.prev = self.tail
            self.tail = new_node

    def insert_at_beginning(self, data):
        new_node = Node(data)
        if self.head is None:
            self.head = new_node
            self.tail = new_node
        else:
            new_node.next = self.head
            self.head.prev = new_node
            self.head = new_node

    def remove_at_index(self, index):
        if self.head is None:
            return

        if index == 0:
            self.remove_from_front()
            return

        current = self.head
        count = 0
        while current and count < index:
            current = current.next
            count += 1

        if current is None:
            return

        if current == self.tail:
            self.remove_from_back()
            return

        current.prev.next = current.next
        current.next.prev = current.prev

    def remove_from_front(self):
        if self.head is None:
            return

        if self.head == self.tail:
            self.head = None
            self.tail = None
            return

        self.head = self.head.next
        self.head.prev = None

    def remove_from_back(self):
        if self.head is None:
            return

        if self.head == self.tail:
            self.head = None
            self.tail = None
            return

        self.tail = self.tail.prev
        self.tail.next = None

    def print_list_forward(self):
        current = self.head
        while current:
            print(current.data, end=" <-> ")
            current = current.next
        print("None")

    def print_list_backward(self):
        current = self.tail
        while current:
            print(current.data, end=" <-> ")
            current = current.prev
        print("None")


# Example Usage
dll = DoublyLinkedList()

print("--- Inserting nodes ---")
dll.insert_at_end('John')
dll.insert_at_end('Bob')
dll.insert_at_beginning('Laila')
dll.insert_at_end('Susan')
print("Forward traversal:", end=" ")
dll.print_list_forward()  # Output: Laila <-> John <-> Bob <-> Susan <-> None
print("Backward traversal:", end=" ")
dll.print_list_backward()  # Output: Susan <-> Bob <-> John <-> Laila <-> None

print("\n--- Removing 'Bob' (index 2) ---")
dll.remove_at_index(2)
print("Forward traversal:", end=" ")
dll.print_list_forward()  # Output: Laila <-> John <-> Susan <-> None

print("\n--- Removing from the front ('Laila') ---")
dll.remove_from_front()
print("Forward traversal:", end=" ")
dll.print_list_forward()  # Output: John <-> Susan <-> None

print("\n--- Removing from the back ('Susan') ---")
dll.remove_from_back()
print("Forward traversal:", end=" ")
dll.print_list_forward()  # Output: John <-> None
print("Backward traversal:", end=" ")
dll.print_list_backward()  # Output: John <-> None
```

```java
/*
public class DoublyLinkedListNode {
    
    int val;
    DoublyLinkedListNode next;
    DoublyLinkedListNode prev;

    public DoublyLinkedListNode(int val) {
        this.val = val;
        this.next = null;
        this.prev = null;
    }
}
*/

// Implementation for Doubly Linked List
public class DoublyLinkedList {
    DoublyLinkedListNode head;
    DoublyLinkedListNode tail;

    public DoublyLinkedList() {
        head = new DoublyLinkedListNode(-1);
        tail = new DoublyLinkedListNode(-1);
        head.next = tail;
        tail.prev = head;
    }

    public void insertFront(int val) {
        DoublyLinkedListNode newNode = new DoublyLinkedListNode(val);
        newNode.prev = head;
        newNode.next = head.next;
        
        head.next.prev = newNode;
        head.next = newNode;
    }

    public void insertEnd(int val) {
        DoublyLinkedListNode newNode = new DoublyLinkedListNode(val);
        newNode.next = tail;
        newNode.prev = tail.prev;
        
        tail.prev.next = newNode;
        tail.prev = newNode;
    }

    public void removeFront() {
        head.next.next.prev = head;
        head.next = head.next.next;
    }   

    public void removeEnd() {
        tail.prev.prev.next = tail;
        tail.prev = tail.prev.prev;
    }   
    
    public void print() {
        DoublyLinkedListNode curr = head.next;
        while (curr != tail) {
            System.out.print(curr.val + " -> ");
            curr = curr.next;
        }           
        System.out.println();
    }
}
```

### <a name="chapter2part3"></a>Chapter 2 - Part 3: Queues

**Time Complexity**

| Operation | Big-O Time | Notes
| :---: | :---: | :---: |
| Enqueue | O(1) | |
| Dequeue | O(1) | Check if the stack is empty first |

```py
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None


class Queue:
    def __init__(self):
        self.right = None
        self.left = None

    def enqueue(self, data):
        new_node = Node(data)
        # Queue is empty
        if self.right is None:
            self.right = new_node
            self.left = new_node
        # Queue is non-empty
        else:
            self.right.next = new_node
            self.right = self.right.next

    def dequeue(self):
        # Queue is empty
        if not self.left:
            return None

        # Remove left node and return value
        data = self.left.data
        self.left = self.left.next
        if not self.left:
            self.right = None
        return data

    def print_queue(self):
        current = self.left
        while current:
            print(current.data, end=" -> ")
            current = current.next
        print("None")


queue = Queue()
queue.enqueue('John')
queue.enqueue('Bob')
queue.enqueue('Laila')
print(queue.dequeue())  # remove John
queue.print_queue() # Bob -> Laila -> None
```

```java
// public class ListNode {
//     int val;
//     ListNode next;
//
//     public ListNode(int val) {
//         this.val = val;
//         this.next = null;
//     }
// }

public class Queue {
    ListNode left;  // front of Queue   front -> [1,2,3]
    ListNode right; // back of Queue   [1,2,3] <- back
    
    public Queue() {
        this.left  = null;
        this.right = null;
    }

    public void enqueue(int val) {
        ListNode newNode = new ListNode(val);
        if (this.right != null) {  
        // Queue is not empty 
            this.right.next = newNode;
            this.right = this.right.next;
        } else {       
        // Queue is empty             
            this.left = newNode;
            this.right = newNode;
        }
    }

    public int dequeue() {
        if (this.left == null) {
            // Queue is empty 
            System.exit(0);
        }
        int val = this.left.val;
        this.left = this.left.next;
        if (this.left == null) {
            this.right = null;
        }
        return val;
    }

    public void print() {
        ListNode cur = this.left;
        while(cur != null) {
            System.out.print(cur.val + " -> ");
            cur = cur.next;
        }
        System.out.println();
    }

}
```

## <a name="chapter3"></a>Chapter 3: Recursion

### <a name="chapter3part1"></a>Chapter 3 - Part 1: Generate Parentheses(Recursion with Backtracking)

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
