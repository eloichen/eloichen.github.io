# Assignment #C: 五味杂陈 

Updated 1148 GMT+8 Dec 10, 2024

2024 fall, Complied by <mark>陈一匡 物理学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 1115. 取石子游戏

dfs, https://www.acwing.com/problem/content/description/1117/

思路：



代码：

```python
while True:
    a,b=map(int,input().split())
    ans=True
    if a==b==0:
        break
    else:
        a,b=max(a,b),min(a,b)
        while b>0 and a//b<2:
            if a==b:
                break
            a,b=b,a-b
            ans=not ans
        print('win' if ans else 'lose')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![c7df95fe1659980362b2f3f0678e396](E:\HuaweiMoveData\Users\33722\Desktop\计算概论\assignment 12\c7df95fe1659980362b2f3f0678e396.png)



### 25570: 洋葱

Matrices, http://cs101.openjudge.cn/practice/25570

思路：



代码：

```python
n=int(input())
matrix = [list(map(int,input().split())) for _ in range(n)]
ans = 0
for i in range((n + 1) // 2):
    l=0
    if i != n - 1 - i:
        l+= sum(matrix[i][i: n - i])
        l+= sum(matrix[n - 1 - i][i: n - i])
        for j in range(i+1,n-1-i):
            l+= matrix[j][n-1-i]+matrix[j][i]
    if i == n - 1 - i:
        l+= sum(matrix[i][i: n - i])
    ans = max(l, ans)
print(ans)
```



代码运行截图 ==（至少包含有"Accepted"）==

![f409f1ad95598e5a83a7eb157d0c0de](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\f409f1ad95598e5a83a7eb157d0c0de.png)



### 1526C1. Potions(Easy Version)

greedy, dp, data structures, brute force, *1500, https://codeforces.com/problemset/problem/1526/C1

思路：



代码：

```python
import heapq
n=int(input())
l=list(map(int,input().split()))
h=0
potions=[]
for i in range(n):
    h+=l[i]
    heapq.heappush(potions,l[i])
    if h<0:
        if potions:
            h-=potions[0]
            heapq.heappop(potions)
print(len(potions))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![22749a0681a1c594b9082cd1ece2baa](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\22749a0681a1c594b9082cd1ece2baa.png)



### 22067: 快速堆猪

辅助栈，http://cs101.openjudge.cn/practice/22067/

思路：



代码：

```python
pigs,pigs_min=[],[]
while True:
    try:
        l=input().split()
        if l[0]=='pop':
            if pigs:
                pigs.pop()
                pigs_min.pop()
        elif l[0]=='min':
            if pigs_min:
                print(pigs_min[-1])
        else:
            w=int(l[1])
            pigs.append(w)
            if pigs_min:
                pigs_min.append(min(w,pigs_min[-1]))
            else:
                pigs_min.append(w)
    except EOFError:
        break
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![0236eec1078e0d10ac7fa1450e6418d](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\0236eec1078e0d10ac7fa1450e6418d.png)



### 20106: 走山路

Dijkstra, http://cs101.openjudge.cn/practice/20106/

思路：



代码：

```python
import heapq

m,n,p=map(int,input().split())
graph=[list(input().split()) for _ in range(m)]

def dijkstra(start_x,start_y,end_x,end_y):
    directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]
    if graph[start_x][start_y]=='#':
        return 'NO'
    dist=[[float('inf')]*n for _ in range(m)]
    dist[start_x][start_y]=0
    pos=[]
    heapq.heappush(pos,(0,start_x,start_y))
    while pos:
        d,x,y=heapq.heappop(pos)
        if x==end_x and y==end_y:
            return d
        for dx,dy in directions:
            nx,ny=x+dx,y+dy
            if 0<=nx<m and 0<=ny<n and graph[nx][ny]!='#':
                if dist[nx][ny]>dist[x][y]+abs(int(graph[nx][ny])-int(graph[x][y])):
                    dist[nx][ny]=dist[x][y]+abs(int(graph[nx][ny])-int(graph[x][y]))
                    heapq.heappush(pos,(dist[nx][ny],nx,ny))
    return 'NO'


for _ in range(p):
    start_x,start_y,end_x,end_y=map(int,input().split())
    print(dijkstra(start_x,start_y,end_x,end_y))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![4fc60408135aefa69ca8b198b70cae0](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\4fc60408135aefa69ca8b198b70cae0.png)



### 04129: 变换的迷宫

bfs, http://cs101.openjudge.cn/practice/04129/

思路：



代码：

```python
from collections import deque
directions=[(0,1),(-1,0),(1,0),(0,-1)]

t=int(input())
for _ in range(t):
    c,r,k =map(int,input().split())
    m=[list(input()) for _ in range(c)]

    ans=float('inf')
    queue=deque()
    x0,y0=0,0
    for i in range(c):
        for j in range(r):
            if m[i][j]=='S':
                x0,y0=i,j
                break
    queue.append((x0,y0,0))
    visited={(x0,y0,0)}
    while queue:
        x,y,step=queue.popleft()
        if m[x][y]=='E':
            ans=step
            break
        for dx,dy in directions:
            nx,ny=x+dx,y+dy
            if 0<=nx<c and 0<=ny<r and (nx,ny,(step+1)%k) not in visited and (m[nx][ny]!='#' or (step+1)%k==0):
                visited.add((nx,ny,(step+1)%k))
                queue.append((nx, ny, step + 1))
    if ans<float('inf'):
        print(ans)
    else:
        print('Oop!')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![e0dc092a2368bfd67750640dbb85c0e](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\e0dc092a2368bfd67750640dbb85c0e.png)



## 2. 学习总结和收获

正在学习笔试相关内容。



