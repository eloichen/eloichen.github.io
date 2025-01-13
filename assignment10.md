# Assignment #10: dp & bfs

Updated 2 GMT+8 Nov 25, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### LuoguP1255 数楼梯

dp, bfs, https://www.luogu.com.cn/problem/P1255

思路：



代码：

```python
l=[1,1]
for i in range(2,5001):
    l.append(l[-1]+l[-2])
print(l[int(input())])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![1a4ad3ec1dc66e2d303b56fa66a2be4](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\1a4ad3ec1dc66e2d303b56fa66a2be4.png)



### 27528: 跳台阶

dp, http://cs101.openjudge.cn/practice/27528/

思路：



代码：

```python
l=[1,1]
for i in range(2,26):
    l.append(sum(l))
print(l[int(input())])
```



代码运行截图 ==（至少包含有"Accepted"）==

![4d2b0bb99802e8d54e8f6a72ca10c92](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\4d2b0bb99802e8d54e8f6a72ca10c92.png)



### 474D. Flowers

dp, https://codeforces.com/problemset/problem/474/D

思路：要多dp以下，要不然会超时。



代码：

```python
t,k=map(int,input().split())
l=[1]*(10**5+1)
for i in range(k,10**5+1):
    l[i]=(l[i-k]+l[i-1])%(10**9+7)
ans=[0]
for i in range(1,10**5+1):
    ans.append((ans[-1]+l[i])%(10**9+7))
for i in range(t):
    a,b=map(int,input().split())
    print((ans[b]-ans[a-1])%(10**9+7))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![6ac9df47a9c46acf42cf44b8be6fac8](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\6ac9df47a9c46acf42cf44b8be6fac8.png)



### LeetCode5.最长回文子串

dp, two pointers, string, https://leetcode.cn/problems/longest-palindromic-substring/

思路：暴力枚举



代码：

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        ans = s[0]
        for i in range(len(s) - 1):
            j, k = 0, 0
            while i - j >= 0 and i + j <= len(s) - 1 and s[i - j] == s[i + j]:
                j += 1
            while i - k >= 0 and i + k + 1 <= len(s) - 1 and s[i - k] == s[i + 1 + k]:
                k += 1
            if 2 * j - 1 > 2 * k and 2*j - 1 > len(ans):
                ans = s[i - j + 1 : i + j]
            elif 2 * k > len(ans):
                ans = s[i - k + 1 : i + k + 1]
        return ans
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![985c1e8b14df01cb7430ab89ce8872f](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\985c1e8b14df01cb7430ab89ce8872f.png)





### 12029: 水淹七军

bfs, dfs, http://cs101.openjudge.cn/practice/12029/

思路：输入太复杂了，照着答案改的才对。



代码：

```python
from collections import deque
import sys
input = sys.stdin.read

def is_valid(x, y, m, n):
    return 0 <= x < m and 0 <= y < n
directions=[(0,1),(0,-1),(-1,0),(1,0)]
def bfs(start_x, start_y, start_height, m, n, h, water_height):
    queue = deque([(start_x, start_y, start_height)])
    water_height[start_x][start_y] = start_height
    while queue:
        x, y, height = queue.popleft()
        for dx,dy in directions:
            nx, ny = x+dx,y+dy
            if 0 <= nx < m and 0 <= ny < n and h[nx][ny] < height:
                if water_height[nx][ny] < height:
                    water_height[nx][ny] = height
                    queue.append((nx, ny, height))

def main():
    data = input().split() 
    idx = 0
    k = int(data[idx])
    idx += 1
    results = []

    for _ in range(k):
        m, n = map(int, data[idx:idx + 2])
        idx += 2
        h = []
        for i in range(m):
            h.append(list(map(int, data[idx:idx + n])))
            idx += n
        water_height = [[0] * n for _ in range(m)]

        i, j = map(int, data[idx:idx + 2])
        idx += 2
        i, j = i - 1, j - 1

        p = int(data[idx])
        idx += 1

        for _ in range(p):
            x, y = map(int, data[idx:idx + 2])
            idx += 2
            x, y = x - 1, y - 1
            if h[x][y] <= h[i][j]:
                continue
            bfs(x, y, h[x][y], m, n, h, water_height)

        results.append("Yes" if water_height[i][j] > 0 else "No")

    sys.stdout.write("\n".join(results) + "\n")

if __name__ == "__main__":
    main()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![7d533bd90935ed7733a718afcb44bd1](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\7d533bd90935ed7733a718afcb44bd1.png)



### 02802: 小游戏

bfs, http://cs101.openjudge.cn/practice/02802/

思路：参考了答案的思路



代码：

```python
from collections import deque

def bfs(start, end, grid, h, w):
    queue = deque([start])
    visited = set()
    directions = [(0, -1), (-1, 0), (0, 1), (1, 0)]

    ans = []
    while queue:
        x, y, d_i_r, seg = queue.popleft()
        if (x, y) == end:
            ans.append(seg)
            break

        for i, (dx, dy) in enumerate(directions):
            nx, ny = x + dx, y + dy

            if 0 <= nx <= h + 1 and 0 <= ny <= w + 1 and (nx, ny, i) not in visited:
                new_dir = i
                new_seg = seg if new_dir == d_i_r else seg + 1
                if (nx, ny) == end:
                    ans.append(new_seg)
                    continue

                if grid[nx][ny] != 'X':
                    visited.add((nx, ny, i))
                    queue.append((nx, ny, new_dir, new_seg))

    if len(ans) == 0:
        return -1
    else:
        return min(ans)


board = 1
while True:
    w, h = map(int, input().split())
    if w == h == 0:
        break

    cards = [' ' * (w + 2)] + [' ' + input() + ' ' for _ in range(h)] + [' ' * (w + 2)]
    print('Board #{}:'.format(board))
    pair = 1
    while True:
        y1, x1, y2, x2 = map(int, input().split())
        if x1 == y1 == x2 == y2 == 0:
            break

        start = (x1, y1, -1, 0)
        end = (x2, y2)

        seg = bfs(start, end, cards, h, w)
        if seg == -1:
            print('Pair {}: impossible.'.format(pair))
        else:
            print('Pair {}: {} segments.'.format(pair,seg))
        pair += 1
    print()
    board += 1
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![8e236c4e4155f4e800d8facdeae8fb1](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\8e236c4e4155f4e800d8facdeae8fb1.png)



## 2. 学习总结和收获

这次作业前面都很简单，最后两题卡了我很久，特别是小游戏，只能看答案了。最近有点忙每日选做没时间做，争取以后补上。





