## 475.Heaters

Winter is coming! Your first job during the contest is to design a standard heater with fixed warm radius to warm all the houses.

Now, you are given positions of houses and heaters on a horizontal line, find out minimum radius of heaters so that all houses could be covered by those heaters.

So, your input will be the positions of houses and heaters seperately, and your expected output will be the minimum radius standard of heaters.

**Note:**

1. Numbers of houses and heaters you are given are non-negative and will not exceed 25000.

2. Positions of houses and heaters you are given are non-negative and will not exceed 10^9.

3. As long as a house is in the heaters' warm radius range, it can be warmed.

4. All the heaters follow your radius standard and the warm radius will the same.

**Example 1:**

    Input: [1,2,3],[2]
    Output: 1
    Explanation: The only heater was placed in the position 2, and if we use the radius 1 standard, then all the houses can be warmed.
**Example 2:**

    Input: [1,2,3,4],[1,4]
    Output: 1
    Explanation: The two heater was placed in the position 1 and 4. We need to use radius 1 standard, then all the houses can be warmed.
    
**Ideas:**

* In order to heat every house, we need to start with houses, searching for the nearest heater. That way, we can get the minimal range of one heater from that house.
* If we search through all houses, eventually we'll get a list of ranges which denote the minimal ranges from the nearest heater. If we choose the largest one, we can ensure that the farthest house will be covered within the range of its nearest heater.
* Thus algorithm will be as follows:

    * Scan through locations of houses, for each house searching for the nearest heater and get the distance between that heater and this house, say range(i)
    
    * Choose max(range(1), range(2), ..., range(n)) as the minimum radius of heaters
    
* Note that in order to search for the nearest heater, we might use an efficient way: binary search once all the heater locations are sorted.

**Solution: (Binary Search)**


    def findRadius(self, houses, heaters):
        """
        :type houses: List[int]
        :type heaters: List[int]
        :rtype: int
        """
        heaters.sort()
        res = 0
        for pos in houses:
            h = self.bsearch(pos, heaters)
            r = abs(h - pos)
            res = max(r, res)
        return res
        
    def bsearch(self, p, heaters):
        start = 0
        end = len(heaters)-1
        while start + 1 < end:
            mid = (start + end) / 2
            if heaters[mid] < p:
                start = mid
            elif heaters[mid] > p:
                end = mid
            else:
                return heaters[mid]
        l, r = heaters[start], heaters[end]
        if l <= p < r:
            return l if p-l < r-p else r
        elif p < l:
            return l
        elif r <= p:
            return r
            
**Be Carefull!**
 
1. When doing binary search, be careful using `start = mid` instead of `start = mid+1` (`end = mid` instead of `end = mid-1`). 

    Because eventually our search space will be a range with endpoints `start` and `end`, thus `heaters[mid] < p` means this `mid` heater might be the rightmost heater we are looking for on the left of `p`, it should be included in our search space. Therefore, our start should be shifted to the place of mid in the next round. 
            