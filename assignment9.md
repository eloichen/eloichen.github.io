# Assignment #9: dfs, bfs, & dp

Updated 2107 GMT+8 Nov 19, 2024

2024 fall, Complied by <mark>陈一匡 物理学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 18160: 最大连通域面积

dfs similar, http://cs101.openjudge.cn/practice/18160

思路：



代码：

```python
import sys
sys.setrecursionlimit(10**8)
count=0
moves=[(1,1),(1,-1),(-1,-1),(-1,1),(1,0),(-1,0),(0,1),(0,-1)]
def clear(x,y):
    global count
    count+=1
    field[x][y]='.'
    for move in moves:
        if field[x+move[0]][y+move[1]]=='W':
            clear(x+move[0],y+move[1])
    return

t=int(input())
for _ in range(t):
    n,m=map(int,input().split())
    field=[['.']*(m+2)]
    for i in range(n):
        line=input()
        field.append(['.']+list(line)+['.'])
    field.append(['.']*(m+2))
    ans=0
    for i in range(1,n+1):
        for j in range(1,m+1):
            if field[i][j]=='W':
                count=0
                clear(i,j)
                ans=max(count,ans)
    print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![a1126d79c8ebe1435c1e06e05c42fb2](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\a1126d79c8ebe1435c1e06e05c42fb2.png)



### 19930: 寻宝

bfs, http://cs101.openjudge.cn/practice/19930

思路：



代码：

```python
from collections import deque
m,n=map(int,input().split())
treasure_map=[list(map(int,input().split())) for _ in range(m)]
visited=[[False]*n for _ in range(m)]
directions=[(1,0),(0,1),(-1,0),(0,-1)]
queue=deque([((0,0),0)])
flag=0
visited[0][0]=True
while queue:
    (x,y),step=queue.popleft()
    if treasure_map[x][y]==1:
        print(step)
        flag=1
        break
    else:
        for (dx,dy) in directions:
            # 不能直接更新x,y的值，因为有四个不同的方向要共用x,y。
            nx=x+dx
            ny=y+dy
            if 0<=nx<=m-1 and 0<=ny<=n-1 and not visited[nx][ny] and treasure_map[nx][ny]!=2:
                queue.append(((nx,ny),step+1))
                visited[nx][ny] = True
if flag==0:
    print('NO')
```



代码运行截图 ==（至少包含有"Accepted"）==

![98ec2a80f5560db8f19c2b1d26ca334](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\98ec2a80f5560db8f19c2b1d26ca334.png)



### 04123: 马走日

dfs, http://cs101.openjudge.cn/practice/04123

思路：



代码：

```python
moves=[(1,2),(1,-2),(-1,2),(-1,-2),(2,1),(2,-1),(-2,1),(-2,-1)]
w=0
def search(n,m,visited,x,y,d):
    global w
    if d==n*m:
        w+=1
        return
    for dx,dy in moves:
        if 0<=x+dx<n and 0<=y+dy<m and not visited[x+dx][y+dy]:
            visited[x+dx][y+dy]=True
            search(n,m,visited,x+dx,y+dy,d+1)
            visited[x+dx][y+dy]=False
t=int(input())
for _ in range(t):
    n,m,x,y=map(int,input().split())
    w=0
    visited=[[False]*m for i in range(n)]
    visited[x][y]=True
    search(n,m,visited,x,y,1)
    print(w)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![cf55a6c42e01eedc9f4c317ebed5ab4](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\cf55a6c42e01eedc9f4c317ebed5ab4.png)



### sy316: 矩阵最大权值路径

dfs, https://sunnywhy.com/sfbj/8/1/316

思路：



代码：

```python
moves=[(0,1),(1,0),(-1,0),(0,-1)]
ans=-float('inf')#需要考虑负数情况
path=[]
def dfs(visited,s,temp,x,y):
    global ans
    global path
    if x==n-1 and y==m-1:
        if s>ans:
            path=temp[:]#深拷贝
            ans=s
        return
    for dx,dy in moves:
        if 0<=x+dx<=n-1 and 0<=y+dy<=m-1 and not visited[x+dx][y+dy]:
            s+=matrix[x+dx][y+dy]
            temp.append((x+dx,y+dy))
            visited[x+dx][y+dy]=True
            dfs(visited,s,temp,x+dx,y+dy)
            visited[x+dx][y+dy]=False
            s-=matrix[x+dx][y+dy]
            temp.pop()

n,m=map(int,input().split())
matrix=[]
for _ in range(n):
    matrix.append(list(map(int,input().split())))
visited=[[False]*m for _ in range(n)]
visited[0][0]=True
dfs(visited,matrix[0][0],[(0,0)],0,0)
for i in path:
    print(i[0]+1,i[1]+1)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![f4ab3882e3babfdc9b00401813e712e](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\f4ab3882e3babfdc9b00401813e712e.png)





### LeetCode62.不同路径

dp, https://leetcode.cn/problems/unique-paths/

思路：

排列组合

代码：

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        ans=1
        for i in range(n-1):
            ans=ans*(m+n-2-i)
        for i in range(1,n):
            ans=ans//i
        return int(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![0b6ce916f32564b30d83e84b23d957a](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\0b6ce916f32564b30d83e84b23d957a.png)



### sy358: 受到祝福的平方

dfs, dp, https://sunnywhy.com/sfbj/8/3/539

思路：暴力枚举



代码：

```python
square_nums=set()
for i in range(1,31624):
    square_nums.add(i*i)
def f(a):
    if int(a) in square_nums:
        return 'Yes'
    for i in range(len(a)):
        if int(a[:i+1]) in square_nums and f(a[i+1:])=='Yes':
            return 'Yes'
    return 'No'

a=input()
print(f(a))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![9106bdb043de9652b5ba1ff6f2acf25](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\9106bdb043de9652b5ba1ff6f2acf25.png)



## 2. 学习总结和收获

作业基本上都是模版题，思路上不是特别复杂，但是写出来的时候还是有一些小地方卡住了（比如说深拷贝），今后要继续注意小细节，不能在很基础的地方犯错了。





