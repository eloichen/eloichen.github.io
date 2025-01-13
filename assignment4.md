# Assignment #4: T-primes + 贪心

Updated 0337 GMT+8 Oct 15, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知9月19日导入选课名单后启用。**作业写好后，保留在自己手中，待9月20日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 34B. Sale

greedy, sorting, 900, https://codeforces.com/problemset/problem/34/B



思路：按题目做即可



代码

```python
n,m=map(int,input().split())
l=list(map(int,input().split()))
l.sort()
i=0
money=0
for _ in range(n):
    if l[_]>0:
        i=_
        break
    else:
        i=n
for _ in range(min(m,i)):
    money+=l[_]
print(-money)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![6595f572e6423fd4d83c9f9d4c37705](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\6595f572e6423fd4d83c9f9d4c37705.png)



### 160A. Twins

greedy, sortings, 900, https://codeforces.com/problemset/problem/160/A

思路：按题目要求做



代码

```python
n=int(input())
values=list(map(int,input().split()))
values.sort(reverse=True)
t=0
l1=0
l2=sum(values)
while l1<=l2:
    l1+=values[t]
    l2-=values[t]
    t+=1
print(t)
```



代码运行截图 ==（至少包含有"Accepted"）==

![647e1807d7437a634c2375a4e4c3911](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\647e1807d7437a634c2375a4e4c3911.png)



### 1879B. Chips on the Board

constructive algorithms, greedy, 900, https://codeforces.com/problemset/problem/1879/B

思路：最小的一定是某一行最小的乘n加上对应列之和或者某一列最小乘n加上对应之行之和。



代码

```python
num=int(input())
ans=[]
for _ in range(num):
    n=int(input())
    x=list(map(int,input().split()))
    y=list(map(int,input().split()))
    ans.append(min(n*min(x)+sum(y),n*min(y)+sum(x)))
for _ in range(num):
    print(ans[_])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![b8ae6456c4286b633df5fd9ec919c86](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\b8ae6456c4286b633df5fd9ec919c86.png)



### 158B. Taxi

*special problem, greedy, implementation, 1100, https://codeforces.com/problemset/problem/158/B

思路：3和2剩下的可以塞1



代码

```python
from collections import Counter
import math
n=int(input())
l=list(map(int,input().split()))
a=Counter(l)
ans=a[4]+a[3]+math.ceil(a[2]/2)
r=max(a[1]-a[3]-(a[2]%2)*2,0)
ans+=math.ceil(r/4)
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![04f2e248f7ad631a0cb76d6a864d229](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\04f2e248f7ad631a0cb76d6a864d229.png)



### *230B. T-primes（选做）

binary search, implementation, math, number theory, 1300, http://codeforces.com/problemset/problem/230/B

思路：研究了一下欧拉线性筛的思路。



代码

```python
from math import sqrt
n=int(input())
def find_primes(x):
    flag=[0]*(x+1)
    ans=[]
    for i in range(2,x+1):
        if flag[i]==0:
            ans.append(i)
        for j in ans:
            if j*i>x:
                break
            flag[j*i]=1
            if j%i==0:
                break
    return ans
primes=set(find_primes(10**6))
 
nums=list(map(int,input().split()))
for i in nums:
    if sqrt(i)%1!=0:
        print('NO')
    elif sqrt(i) in primes:
        print('YES')
    else:
        print('NO')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![3c1cb5fb3f424d5b154d470ae0811ac](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\3c1cb5fb3f424d5b154d470ae0811ac.png)



### *12559: 最大最小整数 （选做）

greedy, strings, sortings, http://cs101.openjudge.cn/practice/12559

思路：没什么思路，看了答案才会做的。学习到了cmp_to_key的用法



代码

```python


```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





## 2. 学习总结和收获

每日选做还在一直跟进。这次学会了欧拉筛的筛法，和二分查找的代码实现。





