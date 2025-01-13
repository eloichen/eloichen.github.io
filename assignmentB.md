# Assignment #B: Dec Mock Exam大雪前一天

Updated 1649 GMT+8 Dec 5, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）⽉考： AC6<mark>（请改为同学的通过数）</mark> 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E22548: 机智的股民老张

http://cs101.openjudge.cn/practice/22548/

思路：



代码：

```python
ans=0
a=list(map(int,input().split()))
max_so_far=[0]*len(a)
max_so_far[-1]=a[-1]
for i in range(len(a)-2,-1,-1):
    max_so_far[i]=max(max_so_far[i+1],a[i])
for i in range(len(a)-1):
    ans=max(ans,max_so_far[i+1]-a[i])
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![98010ce87257fcc33d93646e1d0cf2d](E:\HuaweiMoveData\Users\33722\Desktop\计算概论\assgingment 11\98010ce87257fcc33d93646e1d0cf2d.png)



### M28701: 炸鸡排

greedy, http://cs101.openjudge.cn/practice/28701/

思路：



代码：

```python
n,k=map(int,input().split())
a=list(map(int,input().split()))
a.sort()
s=sum(a)
while a[-1]>s/k:
    s-=a.pop()
    k-=1
print("{:.3f}".format(s/k))
```



代码运行截图 ==（至少包含有"Accepted"）==

![fc7d5bc1898442988189374fd41ed26](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\fc7d5bc1898442988189374fd41ed26.png)



### M20744: 土豪购物

dp, http://cs101.openjudge.cn/practice/20744/

思路：



代码：

```python
v=list(map(int,input().split(',')))
max_include=[v[0]]
for i in range(1,len(v)):
    max_include.append(max(v[i],v[i]+max_include[-1]))
max_include_reverse=[0]*(len(v)-1)+[v[-1]]
for i in range(len(v)-2,-1,-1):
    max_include_reverse[i]=max(v[i],v[i]+max_include_reverse[i+1])
ans=max(max_include)
for i in range(1,len(v)-1):
    ans=max(ans,max_include[i-1]+max_include_reverse[i+1])
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![204fd5bc197f986629a7a0d84b7b835](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\204fd5bc197f986629a7a0d84b7b835.png)



### T25561: 2022决战双十一

brute force, dfs, http://cs101.openjudge.cn/practice/25561/

思路：



代码：

```python
ans=float('inf')
def lowest_cost(m,coupons,cost):
    t_cost=sum(cost)
    t_cost-=50*(t_cost//300)
    for i in range(m):
        d=0
        for limit,discount in coupons[i]:
            if cost[i]>=limit:
                d=max(d,discount)
        t_cost-=d
    return t_cost

def dfs(n,m,prices,coupons,cost):
    global ans
    if not prices:
        ans=min(ans,lowest_cost(m,coupons,cost))
    else:
        price_now=prices.pop()
        for i1,p1 in price_now:
            cost[i1-1]+=p1
            dfs(n,m,prices,coupons,cost)
            cost[i1-1]-=p1
        prices.append(price_now)
        return

n,m=map(int,input().split())
prices=[]
for i in range(n):
    price_i0=list(map(str,input().split()))
    price_i=[]
    for j in range(len(price_i0)):
        (s,p)=map(int,price_i0[j].split(':'))
        price_i.append((s,p))
    prices.append(price_i)
coupons=[]
for i in range(m):
    coupon_i0=list(map(str,input().split()))
    coupon_i = []
    for j in coupon_i0:
        a,b=map(int,j.split('-'))
        coupon_i.append((a,b))
    coupons.append(coupon_i)

dfs(n,m,prices,coupons,[0]*m)
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![a7d60e8524908420710aa32d79278b9](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\a7d60e8524908420710aa32d79278b9.png)



### T20741: 两座孤岛最短距离

dfs, bfs, http://cs101.openjudge.cn/practice/20741/

思路：

dfs+bfs

代码：

```python
from collections import deque

def dfs(x, y, grid, n, queue, directions):
    grid[x][y] = 2 
    queue.append((x, y))
    for dx, dy in directions:
        nx, ny = x + dx, y + dy
        if 0 <= nx < n and 0 <= ny < n and grid[nx][ny] == 1:
            dfs(nx, ny, grid, n, queue, directions)

def bfs(grid, n, queue, directions):
    distance = 0
    while queue:
        for _ in range(len(queue)):
            x, y = queue.popleft()
            for dx, dy in directions:
                nx, ny = x + dx, y + dy
                if 0 <= nx < n and 0 <= ny < n:
                    if grid[nx][ny] == 1:
                        return distance
                    elif grid[nx][ny] == 0:
                        grid[nx][ny] = 2
                        queue.append((nx, ny))
        distance += 1
    return distance

def main():
    n = int(input())
    grid = [list(map(int, input())) for _ in range(n)]
    directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]
    queue = deque()

    for i in range(n):
        for j in range(n):
            if grid[i][j] == 1:
                dfs(i, j, grid, n, queue, directions)
                return bfs(grid, n, queue, directions)

if __name__ == "__main__":
    print(main())
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![cc21b5da07abd230fa59323f6d1827a](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\cc21b5da07abd230fa59323f6d1827a.png)



### T28776: 国王游戏

greedy, http://cs101.openjudge.cn/practice/28776

思路：



代码：

```python
n=int(input())
a,b=map(int,input().split())
l=[]
for i in range(n):
    ai,bi=map(int,input().split())
    l.append((ai*bi,ai,bi))
l.sort()
ans=a//l[0][2]
m=a
for i in range(1,n):
    m*=l[i-1][1]
    ans=max(ans,m//l[i][2])
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![335a2cad8912f2b05eb14b6696db54b](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\335a2cad8912f2b05eb14b6696db54b.png)



## 2. 学习总结和收获

这周一直在写各种论文，没什么时间管计概。下周准备一下笔试内容。



