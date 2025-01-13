# Assignment #D: 十全十美 

Updated 1254 GMT+8 Dec 17, 2024

2024 fall, Complied by <mark>陈一匡 物理学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 02692: 假币问题

brute force, http://cs101.openjudge.cn/practice/02692

思路：



代码：

```python
n=int(input())
for _ in range(n):
    items={'A':0,'B':0,'C':0,'D':0,'E':0,'F':0,'G':0,'H':0,'I':0,'J':0,'K':0,'L':0}
    states=[]
    for i in range(3):
        left,right,result=map(str,input().split())
        state=[left,right,result]
        states.append(state)
    coins=['A','B','C','D','E','F','G','H','I','J','K','L']
    for j in coins:
        found=False
        for t in range(2):
            items[j]=-1+2*t
            flag=0
            for k in range(3):
                l,r=0,0
                for w in states[k][0]:
                    l+=items[w]
                for w in states[k][1]:
                    r+=items[w]
                if (l>r and states[k][2]!='up') or (l<r and states[k][2]!='down') or (l==r and states[k][2]!='even'):
                    flag=1
                    break
            if flag==0:
                if items[j]==1:
                    out='heavy'
                else:
                    out='light'
                found=True
                print(j+' is the counterfeit coin and it is '+out+'.')
                break
        if found:
            break
        items[j]=0
        #注意初始化
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![dfa1d34a041b6e36a6529911fb514d5](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\dfa1d34a041b6e36a6529911fb514d5.png)



### 01088: 滑雪

dp, dfs similar, http://cs101.openjudge.cn/practice/01088

思路：



代码：

```python
import heapq
directions=[(-1,0),(1,0),(0,1),(0,-1)]
r,c=map(int,input().split())
height=[list(map(int,input().split())) for _ in range(r)]
queue=[]
for i in range(r):
    for j in range(c):
        heapq.heappush(queue,(height[i][j],i,j))
step=[[1]*c for _ in range(r)]

while queue:
    h_i,r_i,c_i=heapq.heappop(queue)
    for dr,dc in directions:
        if 0<=r_i+dr<r and 0<=c_i+dc<c and height[r_i][c_i]>height[r_i+dr][c_i+dc]:
            step[r_i][c_i]=max(step[r_i][c_i],step[r_i+dr][c_i+dc]+1)
ans=1
for i in range(r):
    ans=max(ans,max(step[i]))
print(ans)
```



代码运行截图 ==（至少包含有"Accepted"）==

![62edefb118c7aef1f37bb7254f572e9](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\62edefb118c7aef1f37bb7254f572e9.png)



### 25572: 螃蟹采蘑菇

bfs, dfs, http://cs101.openjudge.cn/practice/25572/

思路：



代码：

```python
from collections import deque
n=int(input())
maze=[list(map(int,input().split())) for _ in range(n)]
directions=[(1,0),(0,1),(0,-1),(-1,0)]

def valid(x,y,s):
    x_=x+directions[s][0]
    y_=y+directions[s][1]
    if 0<=x and x_<n and 0<=y and y_<n and maze[x][y]!=1 and  maze[x_][y_]!=1:
        return True
    return False

def bfs(s_x,s_y,s):
    queue=deque([(s_x,s_y)])
    visited=[[False]*n for _ in range(n)]
    visited[s_x][s_y]=True
    while queue:
        x,y=queue.popleft()
        if maze[x][y]==9 or maze[x+directions[s][0]][y+directions[s][1]]==9:
            return 'yes'
        for dx,dy in directions:
            nx,ny=x+dx,y+dy
            if valid(nx,ny,s) and not visited[nx][ny]:
                visited[nx][ny]=True
                queue.append((nx,ny))
    return 'no'

def main():
    for i in range(n):
        for j in range(n):
            if maze[i][j]==5:
                for k in range(4):
                    i_,j_=i+directions[k][0],j+directions[k][1]
                    if 0<=i_<n and 0<=j_<n and maze[i_][j_]==5:
                        print(bfs(i,j,k))
                        return

main()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![b08a48ae0f6d5a4fd6a756da94fe4ed](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\b08a48ae0f6d5a4fd6a756da94fe4ed.png)



### 27373: 最大整数

dp, http://cs101.openjudge.cn/practice/27373/

思路：



代码：

```python
def f(string):
    if string:
        return int(string)
    return 0

m=int(input())
n=int(input())
l=input().split()
for i in range(n):
    for j in range(n-1-i):
        if l[j]+l[j+1]>l[j+1]+l[j]:
            l[j],l[j+1]=l[j+1],l[j]
weight=[len(k) for k in l]
dp=[['']*(m+1) for _ in range(n+1)]
for i in range(1,n+1):
    for j in range(1,m+1):
        if weight[i - 1] > j:
            dp[i][j] = dp[i - 1][j]
        else:
            dp[i][j] = str(max(f(dp[i - 1][j]), int(l[i - 1] + dp[i - 1][j - weight[i - 1]])))
print(dp[n][m])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![3983e70606801a924d71fb3b8b458a3](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\3983e70606801a924d71fb3b8b458a3.png)



### 02811: 熄灯问题

brute force, http://cs101.openjudge.cn/practice/02811

思路：



代码：

```python
import copy
lo=[]
for _ in range(5):
    line=list(map(int,input().split()))
    lo.append(line)
for p in range(64):
    l=copy.deepcopy(lo)
    #深拷贝 初始化的同时保证不会对原输入的列表产生影响
    ans = [[0] * 6 for _ in range(4)]
    p1=bin(p)[2:]
    p2='0'*(6-len(p1))+p1
    ans1=[int(k) for k in p2]
    ans.insert(0,ans1)
    for i in range(6):
        if ans1[i]==1:
            l[1][i]=1-l[1][i]
            if i==0:
                l[0][0],l[0][1]=1-l[0][0],1-l[0][1]
            elif i==5:
                l[0][4], l[0][5] = 1-l[0][4], 1-l[0][5]
            else:
                l[0][i-1],l[0][i],l[0][i+1]=1-l[0][i-1],1-l[0][i],1-l[0][i+1]
    for i in range(4):
        for j in range(6):
            if l[i][j]==1:
                if i!=3:
                    l[i+2][j]=1-l[i+2][j]
                ans[i+1][j],l[i][j]=1,0
                if j==0:
                    l[i+1][0],l[i+1][1]=1-l[i+1][0],1-l[i+1][1]
                elif j==5:
                    l[i+1][4], l[i+1][5] = 1-l[i+1][4],1-l[i+1][5]
                else:
                    l[i+1][j-1], l[i+1][j], l[i+1][j+1] = 1-l[i+1][j-1],1-l[i+1][j],1-l[i+1][j+1]
    flag=0
    for j in range(6):
        if l[4][j]==1:
            flag=1
            break
    if flag==0:
        for j in range(5):
            out=[str(i) for i in ans[j]]
            print(' '.join(out))
        break
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![d669f29ca39b9ae3004aab8eef73800](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\d669f29ca39b9ae3004aab8eef73800.png)



### 08210: 河中跳房子

binary search, greedy, http://cs101.openjudge.cn/practice/08210/

思路：



代码：

```python
l,n,m=map(int,input().split())
rocks=[0]+[int(input()) for _ in range(n)]+[l]

def check(dis):
    flag=0
    num=0
    for i in range(1,n+2):
        if rocks[i]-flag<dis:
            num+=1
        else:
            flag=rocks[i]
    if num>m:
        return True
    return False

left,right=0,l+1
ans=0
while left<right:
    mid=(left+right)//2
    if check(mid):
        right=mid
    else:
        ans = mid
        left = mid + 1
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![3589f435d831354d55d47ebb96dd539](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\3589f435d831354d55d47ebb96dd539.png)



## 2. 学习总结和收获

进入复习状态，准备期末考试了



