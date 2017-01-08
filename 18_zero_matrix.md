## 1.8 Zero Matrix

Write an algorithm such that if an element in an NxN matrix is 0, its entire row and column are set to 0.

**Ideas:**

At first glance, this problem seems easy: just iterate through the matrix and every time we see a cell with value zero, set its row and column to 0. There's one problem with that solution though: when we come across other cells in that row and columns, we'll see the zeros and change their row and column to zero. Pretty soon, our entire matrix will be set to zeros.

One way around this is to keep a record matrix which flags the zero locations. We would then do a second pass through the matrix to set the zeros. This would take O(MN) space.

Do we really need O(MN) space? No, since we're going to set the entire row and column to zero, we don't need to track that it was exactly cell[2][4] (row 2, column 4). We only need to know that row 2 has a zero somewhere, and column 4 has a zero somewhere. We'll set the entire row and column to zero anyway. so why would we care to keep track of the exact location of the zero?

1. We use two arrays to keep track of all the rows with zeros and all the columns with zeros. 

2. We then nullify rows and columns based on the values in these arrays.

**Solution #1:**

    def setZeros(self, matrix):
        row = [False for _ in xrange(len(matrix))]
        column = [False for _ in xrange(len(matrix[0]))]
        #Store the row and column index with value 0
        for i in xrange(len(matrix)):
            for j in xrange(len(matrix[0])):
                if matrix[i][j] == 0:
                    row[i] = True
                    column[j] = True
        # Nullify rows:
        for i in xrange(len(row)):
            if row[i]:
                self.nullifyRow(matrix, i)
        # Nullify columns:
        for j in xrange(lem(column)):
            if column[j]:
                self.nullifyColumn(matrix, j)
                
    def nullifyRow(self, matrix, r):
        for j in xrange(len(matrix[0])):
            matrix[r][j] = 0
    
    def nullifyColumn(self, matrix, c):
        for i in xrange(len(matrix)):
            matrix[i][c] = 0

**Analysis:**

To make this somewhat more space efficient, we could use a bit vector instead of a boolean array. It would still be O(N) space.

We can reduce the space to O(1) by using the first row as a replacement for the row array and the first column as a replacement for the column array. This works as follows:

1. Check if the first row and first column have any zeros, and set variables rowHasZero and columnHasZero. (We'll nullify the first row and first column later, if necessary.)

2. Iterate through the rest of the matrix, setting matrix[i][0] and matrix[0][j] to zero wherever there's a zero in matrix[i][j].

3. Iterate through rest of matrix, nullifying row i if there's zero in matrix[i][0].

4. Iterate through rest of matrix, nullifying column j if there's a zero in matrix[0][j].

5. Nullify the first row and first column, if necessary (based on values from step 1).

**Solution #2:**

    def setZeros(self, matrix):
        rowHasZero = False
        columnHasZero = False
        # Check if the first row has a zero:
        for j in xrange(len(matrix[0])):
            if matrix[0][j] == 0:
                rowHasZero = True
                break
        # Check if first column has a zero
        for i in xrange(len(matrix)):
            if matrix[i][0] == 0:
                columnHasZero = True
                break
        # Check for zeros in the rest of the array:
        for i in xrange(len(matrix)):
            for j in xrabge(len(matrix[0])):
                if matrix[i][j] == 0:
                    matrix[i][0] = 0
                    matrix[0][j] = 0
                    
        # Nullify rows based on values in first column:
        for i in xrange(len(matrix[0])):
            if matrix[i][0] == 0:
                self.nullifyRow(matrix, i)
        # Nullify columns based on values in first row:
        for j in xrange(len(matrix)):
            if matrix[0][j] == 0:
                self.nullifyColumn(matrix, j)
        # Nullify the first column:
        if rowHasZero:
            self.nullifyRow(matrix, 0)
        # Nullify the first row:
        if columnHasZero:
            self.nullifyColumn(matrix, 0)




