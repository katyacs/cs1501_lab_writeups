# Lab 8 Write-Up

## Code

```java
class Solution {
    public boolean isValid(String s) {
        if(s == null ||s.isEmpty())
            return true;
        Deque<Character> parenthesisStack = new ArrayDeque<>();
        for(int i = 0; i < s.length(); i++)
        {
            char curr = s.charAt(i);
            if(curr == '[' || curr == '{' || curr == '(')
                parenthesisStack.push(curr);
            else
            {
                if(parenthesisStack.isEmpty())
                    return false;
                char top =  parenthesisStack.peek();
                if (curr == ')' && top != '(') 
                    return false;
                if (curr == ']' && top != '[')
                    return false;
                if (curr == '}' && top != '{') 
                    return false;
                parenthesisStack.pop();
            }
            
        }
        return parenthesisStack.isEmpty();
    }
}
```
## Description

For this problem, we are given a string made up of open and closed parentheses and we need to determine whether the string is valid. 
A string is valid if every opening bracket is closed by the same type of bracket, and brackets are closed in the correct order.
I knew I wanted to use a stack to solve this problem, but I wasn't entirely sure how to implement a stack in Java, so I looked it up and apparently ArrayDeque is the recommended class.
First, if the string is null or empty, I return true because there are no unmatched brackets. 
Then I iterate through the string one character at a time and if the current character is an opening bracket, I push it onto the stack.
If the current character is a closing bracket, I first check whether the stack is empty and if it is, there is nothing for this bracket to match, so I return false. 
Otherwise, I peek at the top of the stack and check that it is the matching opening bracket for the current closing bracket. If it isn't a match, I return false. 
If it is, I pop the opening bracket off the stack since it has now been matched.
After processing every character, the string is valid only if the stack is empty. If any opening brackets are left over, they were never closed, so I return whether or not the stack is empty.

## Complexity Analysis

**Time Complexity: O(n)** where n is number of characters in the string. I only go through the string once and do a constant amount of work for each character.

**Space Complexity: O(n)** where n is the number of characters in the string in the worst case. As there could be a string with only open brackets, in which case every character gets pushed onto the stack before any are popped.
