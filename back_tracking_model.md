## Back Tracking Model

Using the idea of back tracking, we keep searching for the correct solution until we find it or if some conditions conflicts the constrains we go back to the previous level.

    def bTracking(self, res, initial-case):
    
      if solution found:
          res.append(solution)
          return
      if conditions not satified:
          return
          
      (Sometimes pruning is needed:
      `check for valid conditions`)
      
      for case in validConditions:
          do bTracking(self, res, case)