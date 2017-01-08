## 20.Valid Parentheses

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

**Note:**

* Push to stack when a left parenthesis appears.
* Pop from stack when right appears, and compare to see if they match
* If they match, continue. Otherwise, return False
* Be careful when popping from the stack, if it's empty then just return False
* If there are still left parenthesis left at the end, that means stack is non-empty, then return False

**Solution:**

    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        left = {'[', '{', '('}
        right = {']', '}', ')'}
        stack = []
        for i in s:
            if i in left:
                stack.append(i)
            elif i in right:
                if len(stack) == 0:
                    return False
                l = stack.pop()
                if (i == ']' and l == '[') or (i == '}' and l == '{') or (i == ')' and l == '('):
                    continue
                else:
                    return False
        return len(stack) == 0
            