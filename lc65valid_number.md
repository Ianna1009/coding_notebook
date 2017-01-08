## LC65.Valid Number

Validate if a given string is numeric.

**Some examples:**

    "0" => true
    " 0.1 " => true
    "abc" => false
    "1 a" => false
    "2e10" => true


Note: It is intended for the problem statement to be ambiguous. You should gather all requirements up front before implementing one.
___

** Solution: **

    class Solution(object):
        def isNumber(self, s):
            """
            :type s: str
            :rtype: bool
            """
            n = len(s)
            i, e = 0, n-1
            while i < n and s[i] == " ":
                i += 1
            if i > e:
                return False
            while e >= i and s[e] == " ":
                e -= 1
            if s[i] == "+" or s[i] == "-":
                i += 1
            num, dot, exp = False, False, False
            while i <= e:
                ch = s[i]
                if ch >= "0" and ch <= "9":
                    num = True
                elif ch == ".":
                    if dot or exp:
                        return False
                    dot = True
                elif ch == "e":
                    if exp or not num:
                        return False
                    exp = True
                    num = False
                elif ch == "+" or ch == "-":
                    if s[i-1] != "e":
                        return False
                else:
                    return False
                i += 1
            return num
