# Assignment #8: 田忌赛马来了

Updated 1021 GMT+8 Nov 12, 2024

2024 fall, Complied by <mark>陈一匡 物理学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 12558: 岛屿周⻓

matices, http://cs101.openjudge.cn/practice/12558/ 

思路：数1周围的0的个数即可



代码：

```python
n,m=map(int,input().split())
ocean=[[0]*(m+2)]
for i in range(n):
    column=list(map(int,input().split()))
    ocean.append([0]+column+[0])
ocean.append([0]*(m+2))
ans=0
for i in range(1,n+1):
    for j in range(1,m+1):
        if ocean[i][j]==1:
            ans+=4-ocean[i-1][j]-ocean[i+1][j]-ocean[i][j-1]-ocean[i][j+1]
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![3b3808cfb874db7816b6b8f7599b2c0](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\3b3808cfb874db7816b6b8f7599b2c0.png)



### LeetCode54.螺旋矩阵

matrice, https://leetcode.cn/problems/spiral-matrix/

与OJ这个题目一样的 18106: 螺旋矩阵，http://cs101.openjudge.cn/practice/18106

思路：



代码：

```python
n=int(input())
matrix=[[0]*n for i in range(n)]
direction=0
x,y=0,0
for i in range(1,n**2+1):
    matrix[x][y]=i
    if direction==0:
        if y==n-1 or matrix[x][y+1]!=0:
            direction=1
            x+=1
        else:
            y+=1
    elif direction==1:
        if x==n-1 or matrix[x+1][y]!=0:
            direction = 2
            y-=1
        else:
            x+=1
    elif direction==2:
        if y==0 or matrix[x][y-1]!=0:
            direction = 3
            x-=1
        else:
            y-=1
    elif direction==3:
        if x==0 or matrix[x-1][y]!=0:
            direction = 0
            y+=1
        else:
            x-=1
for row in matrix:
    print(*row)
```



代码运行截图 ==（至少包含有"Accepted"）==

![4be4bd312b4f269807119132c6b8953](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\4be4bd312b4f269807119132c6b8953.png)



### 04133:垃圾炸弹

matrices, http://cs101.openjudge.cn/practice/04133/

思路：



代码：

```python
d=int(input())
n=int(input())
# 最好使用动态规划
bomb=[[0]*1025 for i in range(1025)]
trashes=set()
for _ in range(n):
    x,y,i=map(int,input().split())
    trashes.add((x,y,i))
for trash in trashes:
    for x in range(max(0,trash[0]-d),min(1025,trash[0]+d+1)):
        for y in range(max(0,trash[1]-d),min(1025,trash[1]+d+1)):
            bomb[x][y]+=trash[2]
ans,m=0,0
for i in range(1025):
    if max(bomb[i])>m:
        m=max(bomb[i])
        ans=bomb[i].count(m)
    elif max(bomb[i])==m:
        ans+=bomb[i].count(m)
print(str(ans)+' '+str(m))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![070bde2a9f50770d1f25f47dd49f0e9](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\070bde2a9f50770d1f25f47dd49f0e9.png)



### LeetCode376.摆动序列

greedy, dp, https://leetcode.cn/problems/wiggle-subsequence/

与OJ这个题目一样的，26976:摆动序列, http://cs101.openjudge.cn/routine/26976/

思路：



代码：

```python
n=int(input())
l=list(map(int,input().split()))
a=[]
for i in range(1,n):
    if l[i]-l[i-1]>0:
        a.append(1)
    if l[i]-l[i-1]<0:
        a.append(-1)
if len(a)==0:
    print(1)
else:
    ans=2
    for i in range(1,len(a)):
        if a[i]!=a[i-1]:
            ans+=1
    print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![e291c479930b1a2ec8ba8df3474892d](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\e291c479930b1a2ec8ba8df3474892d.png)



### CF455A: Boredom

dp, 1500, https://codeforces.com/contest/455/problem/A

思路：



代码：

```python
from collections import Counter
n=int(input())
nums=list(map(int,input().split()))
l=[0]*max(nums)
count=Counter(nums)
for key,value in count.items():
    l[key-1]=value
dp=[0]*(len(l)+2)
for i in range(2,len(l)+2):
    dp[i]=max(dp[i-1],dp[i-2]+l[i-2]*(i-1))
print(dp[-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![b0fb334d65c8268ad24d03c8c699cbf](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\b0fb334d65c8268ad24d03c8c699cbf.png)



### 02287: Tian Ji -- The Horse Racing

greedy, dfs http://cs101.openjudge.cn/practice/02287

思路：自己没有思路，看了答案之后自己重新写的代码。



代码：

```python
while True:
    n=int(input())
    if n==0:
        break
    else:
        tian=list(map(int,input().split()))
        king=list(map(int,input().split()))
        tian.sort()
        king.sort()
        tian_i,tian_j=0,n-1
        king_i,king_j=0,n-1
        ans=0
        while tian_i<=tian_j:
            if tian[tian_i]>king[king_i]:
                ans+=1
                tian_i+=1
                king_i+=1
            elif tian[tian_j]>king[king_j]:
                ans+=1
                tian_j-=1
                king_j-=1
            else:
                if tian[tian_i]<king[king_j]:
                    ans-=1
                tian_i+=1
                king_j-=1
        print(200*ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![a339aa4265e9ab4bca45e2296554c77](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\a339aa4265e9ab4bca45e2296554c77.png)



## 2. 学习总结和收获

这次作业其他题目难度都算中等，但是田忌赛马确实需要思路理的比较清楚，我尝试了几次之后还是没有过就放弃了。这周主要还是在忙其他学科的期中考试，只能说是巩固了一下之前的基础，然后了解了一下01背包、完全背包这类动态规划的问题。





