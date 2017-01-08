## 155.Min Stack

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

    push(x) -- Push element x onto stack.
    pop() -- Removes the element on top of the stack.
    top() -- Get the top element.
    getMin() -- Retrieve the minimum element in the stack.

**Example:**


    MinStack minStack = new MinStack();
    minStack.push(-2);
    minStack.push(0);
    minStack.push(-3);
    minStack.getMin();   --> Returns -3.
    minStack.pop();
    minStack.top();      --> Returns 0.
    minStack.getMin();   --> Returns -2.
    

**Solution #1 Using One Stack:**

    class MinStack(object):

        def __init__(self):
            """
            initialize your data structure here.
            """
            self.stack = []
            self.MIN = float('inf')

        def push(self, x):
            """
            :type x: int
            :rtype: void
            """
            if x <= self.MIN:
                self.stack.append(self.MIN)
                self.MIN = x
            self.stack.append(x)


        def pop(self):
            """
            :rtype: void
            """
            if self.stack.pop() == self.MIN:
                self.MIN = self.stack.pop()


        def top(self):
            """
            :rtype: int
            """
            return self.stack[-1]


        def getMin(self):
            """
            :rtype: int
            """
            return self.MIN



    # Your MinStack object will be instantiated and called as such:
    # obj = MinStack()
    # obj.push(x)
    # obj.pop()
    # param_3 = obj.top()
    # param_4 = obj.getMin()
    
**Solution #2: (Using two Stacks)**

    class MinStack(object):

        def __init__(self):
            """
            initialize your data structure here.
            """
            self.stack = []
            self.minstack = []

        def push(self, x):
            """
            :type x: int
            :rtype: void
            """
            if len(self.minstack) == 0 or x <= self.minstack[-1]:
                self.minstack.append(x)
            self.stack.append(x)

        def pop(self):
            """
            :rtype: void
            """
            if len(self.stack) == 0:
                print "Pop from empty stack!"
            elif self.stack[-1] == self.minstack[-1]:
                self.minstack.pop()
            self.stack.pop()

        def top(self):
            """
            :rtype: int
            """
            return None if len(self.stack) == 0 else self.stack[-1]

        def getMin(self):
            """
            :rtype: int
            """
            return None if len(self.minstack) == 0 else self.minstack[-1]
    

    
        