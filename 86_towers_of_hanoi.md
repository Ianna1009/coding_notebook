## 8.6 Towers of Hanoi

In the classic problem of the Towers of Hanoi, you have 3 towers and N disks of different sized which can slide onto any tower. The puzzle starts with disks sorted in ascending order of size from top to bottom (i.e. each dick sits on the top of an even larger one). You have the following constrains:

 1. Only one disk can be moved at a time.
 2. A disk is slid off the top of one tower onto another tower.
 3. A disk cannot be placed on top of a smaller disk.

Write a program to move the disks from the first tower to the last using stacks.

**Ideas:**

This problem sounds like a good candidates for the Base Case and Build approach.

Let's start with the smallest possible example: n = 1.

**Case n = 1.** Can we move Dick 1 from Tower 1 to Tower 3? Yes.
1. We simply move Disk 1 from Tower 1 to Tower 3.

**Case n = 2.** Can we move Disk 1 and Disk 2 from Tower 1 to Tower 3? Yes.
1. Move Disk 1 from Tower 1 to Tower 2.
2. Move Disk 2 from Tower 1 to Tower 3.
3. Move Disk 1 from Tower 2 to Tower 3.
Note how in the above steps, Tower 2 acts as a buffer, holding a disk while we move other disks to Tower 3. 

**Case n = 3.** Can we move Disk 1, 2 and 3 from Tower 1 to Tower 3? Yes.
1. We know we can move the top two disks from one tower to another (as shown earlier), so let's assume we've already done that. But instead, let's move them to Tower 2.
2. Move Disk 3 to Tower 3.
3. Move Disk 1 and Disk 2 to Tower 3. We've already known how to do this -- just repeat what we did in step 1.

**Case n = 4.** Can we move Disk 1, 2, 3, and 4 from Tower 1 to Tower 3? Yes.
1. Move Disk 1, 2, and 3 to Tower 2. We know hoe to do that from the earlier example.
2. Move Disk 4 to Tower 3.
3. Move Disk 1, 2 and 3 to Tower 3.

Remember that the labels of Tower 2 and Tower 3 aren't important. They're equivalent towers. So, moving disks to Tower 3 with Tower 2 serving as a buffer is equivalent to moving disks to Tower 2 with Tower 3 serving as a buffer.

**Solution: **

This approach lead to a natural recursive algorithm. In each part, we are doing the following steps. Outlines below with pseudocode.

    def moveDisk(self, n, origin, destination, buffer):
        # origin, destination, buffer are towers
        if n <= 0: 
            return
        # Move top n-1 disks from origin to buffer, using destination as a buffer.
        self.moveDisk(n-1, origin, buffer, destination)
        # Move top from origin to destination
        self.moveTop(origin, destination)
        # Move top n-1 disks from buffer to destination, using origin as a buffer.
        self.moveDisk(n-1, buffer, destination, origin)
        
**Complementary Design:**

The following code provides a more detailed implementation of this algorithm, using concepts of OOD.

    class Tower():
        
        def __init__(self, n):
            disks = []
            Tower = {i:disks for i in xrange(n)}
        
        def index(self):
            return index
        
        def add(self, d):
            if not self.disk and self.disks[-1] <= d:
                print "Error placing disk " %d
            else:
                self.disks.append(d)
                
        def moveTopTo(self, t):
            """ t: tower """
            top = disks.pop()
            t.append(top)
        
        def moveDisk(self, n, destination, buffer):
            if n > 0:
                self.moveDisks(n-1, buffer, destination)
                self.moveTopTo(destination)
                buffer.moveDisks(n-1, destination, this)
                
    