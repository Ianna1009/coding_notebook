## Flip Game 2

You are playing the following Flip Game with your friend: Given a string that contains only these two characters: + and -, you and your friend take turns to flip two consecutive "++" into "--". The game ends when a person can no longer make a move and therefore the other person will be the winner.

Write a function to determine if the starting player can guarantee a win.

    For example, given s = "++++", return true.
    The starting player can guarantee a win by flipping the middle "++" to become "+--+".

Follow up:
Derive your algorithm's runtime complexity.

___

**Solution:**


    class Solution(object):
        def canWin(self, s):
            """
            :type s: str
            :rtype: bool
            """
            state = [None for _ in xrange(len(s))]
            for i in xrange(len(s)):
                if s[i] == "+":
                    state[i] = True
                else:
                    state[i] = False
            return self.search(state)

        def search(self, state):
            for i in xrange(len(state)-1):
                if state[i] and state[i+1]:
                    state[i] = False
                    state[i+1] = False
                    if not self.search(state):
                        state[i] = True
                        state[i+1] = True
                        return True
                    else:
                        state[i] = True
                        state[i+1] = True
            return False
        
  ---
 ** Solution_2:**
 
     class Solution(object):  
        def canWin(self, s):  
            """ 
            :type s: str 
            :rtype: bool 
            """  
            if len(s) < 2:  
                return False  
            for i in range(len(s) - 1):  
                if s[i] == '+' and s[i+1] == '+' and not self.canWin(s[:i] + '-' + s[i+2:]):  
                    return True  
            return False  

