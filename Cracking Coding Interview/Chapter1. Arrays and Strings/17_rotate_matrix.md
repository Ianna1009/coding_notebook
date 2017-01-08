## 1.7 Rotate Matrix

Given a image represented by an NxN matrix, where each pixel in the image is 4 bytes, write a method to rotate the image by 90 degrees. 

**Follow-Up: Can you do this in place?**

**Ideas:**
A better way to do this is to implement the swap index by index. In this case, we do the following:

    for i to n:
      tmp = top[i]
      top[i] = left[i]
      left[i] = bottom[i]
      bottom[i] = right[i]
      right[i] = tmp

We perform such a swap on each layer, starting form the outermost layer and working our way inwards. (Alternatively, we could start from the inner layer and work outwards)

**Solution:**

    def rotate(self, matrix):
        # Cases when the matrix cannot be rotated
        if len(matrix) == 0 or len(matrix[0]) != len(matrix):
            return False

        n = len(matrix)
        for layer in xrange(n):
            first = layer
            last = n - 1 - layer
            for i in xrange(first, last):
                offset = i - first
                top = matrix[first][i]
                # left -> top:
                matrix[first][i] = matrix[last - offset][first]
                # bottom -> left:
                matrix[last - offset][first] = matrix[last][last - offset]
                # right -> bottom:
                matrix[last][last - offset] = matrix[i][last]
                # top -> right:
                matrix[i][last] = top
        return True
        
**This algorithm is O(n^2) since we need to touch n^2 elements in the matrix.**

                
              
      

