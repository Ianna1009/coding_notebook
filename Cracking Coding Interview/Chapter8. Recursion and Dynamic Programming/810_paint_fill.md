## 8.10 Paint Fill

Implement the "Pain Fill" function that one might see on many image editing programs. That is, given a screen (represented by a two-dimensional array of colors), a point, and a new color, fill in the surrounding area until the color changes from the original color.

**Solution #1: (DFS)**

    def paintFill(screen, origin, color):
        if len(screen) == 0:
            return
        r, c = origin
        origin_color = screen[r][c]
        paint(screen, r, c, color, origin_color)
        

    def paint(screen, row, col, color, orgcolor):
        if row < 0 or col < 0 or row > len(screen)-1 or col > len(screen[0])-1 or screen[row][col] != orgcolor:
            return
        screen[row][col] = color
        dirs = zip([1, 0, -1, 0], [0, 1, 0, -1])
        for d in dirs:
            paint(screen, row+d[0], col+d[1], color, orgcolor)


**Solution #2: (BFS)**

    def paintFillBFS(screen, origin, color):
        if len(screen) == 0:
            return
        r, c = origin
        visit = [(r, c)]
        origin_color = screen[r][c]
        dirs = zip([1, 0, -1, 0], [0, 1, 0, -1])
        while visit:
            curr_r, curr_c = visit.pop(0)
            if curr_r < 0 or curr_r > len(screen) - 1 or curr_c < 0 or curr_c > len(screen[0]) - 1 or screen[curr_r][curr_c] != origin_color:
                continue
            screen[curr_r][curr_c] = color
            for d in dirs:
                r, c = curr_r+d[0], curr_c+d[1]
                visit.append((r, c))
