## 1.5 One Away

There are three types of edits that can be performed on strings: insert a character, remove a character, or replace a character. Given two strings, write a function to check if they are one edit (or zero edits) away.

**Example:**

    pale, ple -> true
    palse, pale -> true
    pale, bale -> true
    pale, bae -> false

**Ideas:**

* **Replacement:** This means they are different only in one place.
*  **Insertion:** This means if you compared the strings, they would be identical -- except for a shift at some point in the strings.
* **Removal:** Removal is just the inverse of insertion.
* Based on these definitions, removal and insertion would end up with different sizes and replacement will be ending with same length.

**Solution:**

  def oneEditAway(self, s1, s2):
      #Check lengths:
      if abs(len(s1) - len(s2)) > 1:
          return False
      #Get longer string and shorter one separately. s1 is longer
      if len(s1) < len(s2):
          s1, s2 = s2, s1
      
      index1, index2 = 0, 0
      foundDiff = False
      while index2 < len(s2) and index1 < len(s1):
          if s1[index1] != s2[index2]:
              # Ensure that this is the first diff found:
              if foundDiff:
                  return False
              foundDiff = True
              # On replace, move shorter pointer
              if len(s1) == len(s2):
                  index1 += 1
          else:
              # If matching, move shorter pointer
              index1 += 1
          # Always move pointer for longer string
          index2 += 1
      return True
         

