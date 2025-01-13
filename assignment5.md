# Assignment #5: Greedy穷举Implementation

Updated 1939 GMT+8 Oct 21, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 04148: 生理周期

brute force, http://cs101.openjudge.cn/practice/04148

思路：找到循环周期



代码：

```python
time=1
while True:
    b,c,d,a=map(int,input().split())
    if a==-1:
        break
    else:
        j=min(b,c,d)
        ini,dis=[b,c,d],[23,28,33]
        p=0
        for i in range(3):
            if j==ini[i]:
                p=dis[i]
        while (j-b)%23!=0 or (j-c)%28!=0 or (j-d)%33!=0 or j<=a:
            j+=p
        print('Case '+str(time)+': the next triple peak occurs in '+str(j-a)+' days.')
        time+=1
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![0d1c30db3a633ffed537c32782f6393](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\0d1c30db3a633ffed537c32782f6393.png)



### 18211: 军备竞赛

greedy, two pointers, http://cs101.openjudge.cn/practice/18211

思路：

先从小到大排序，再用双指针

代码：

```python
p=int(input())
l=list(map(int,input().split()))
l.sort()
i,j,ans=0,len(l)-1,0
while j-i>0:
    if p>=l[i]:
        p-=l[i]
        i+=1
        ans+=1
    elif ans>0:
        p+=l[j]
        j-=1
        ans-=1
    else:
        break
if j==i and p>=l[i]:
    ans+=1
print(ans)
```



代码运行截图 ==（至少包含有"Accepted"）==

![5afc04ac5452fb1cc68b8069aea5090](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\5afc04ac5452fb1cc68b8069aea5090.png)



### 21554: 排队做实验

greedy, http://cs101.openjudge.cn/practice/21554

思路：按学生要做时间的大小排序即可



代码：

```python
n=int(input())
stu_time=list(map(int,input().split()))
stu=[(stu_time[i],i+1) for i in range(n)]
stu.sort()
t=0
for i in range(n):
    t+=stu[i][0]*(n-1-i)
t/=n
ans=[str(i[1]) for i in stu]
print(' '.join(ans))
print(f'{t:.{2}f}')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![be3e0681376259336e59ef0e9da1cc0](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\be3e0681376259336e59ef0e9da1cc0.png)



### 01008: Maya Calendar

implementation, http://cs101.openjudge.cn/practice/01008/

思路：按题目表述做



代码：

```python
h={'pop':1,'no':2,'zip':3,'zotz':4,'tzec':5,'xul':6,'yoxkin':7,
            'mol':8,'chen':9,'yax':10,'zac':11,'ceh':12,'mac':13,'kankin':14,
            'muan':15,'pax':16,'koyab':17,'cumhu':18,'uayet':19}
t=['imix','ik', 'akbal', 'kan', 'chicchan', 'cimi', 'manik', 'lamat', 'muluk', 'ok',
   'chuen', 'eb', 'ben', 'ix', 'mem', 'cib', 'caban', 'eznab', 'canac', 'ahau']
n=int(input())
print(n)
for _ in range(n):
    h_day,e=input().split('.')
    h_month,h_year=e.split()
    date=int(h_day)+1+(h[h_month]-1)*20+365*int(h_year)
    t_year=(date-1)//260
    t_date=date%260
    t_day1,t_day2=str((t_date-1)%13+1),t[(t_date-1)%20]
    print(t_day1+' '+t_day2+' '+str(t_year))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![3a6b9cbe41427da6729717ae1591575](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\3a6b9cbe41427da6729717ae1591575.png)



### 545C. Woodcutters

dp, greedy, 1500, https://codeforces.com/problemset/problem/545/C

思路：优先往左倒，不能往左倒就往右倒，然后更新允许的长度



代码：

```python
from math import inf
n=int(input())
x,h,d=[],[],[inf]
ans=0
for _ in range(n):
    x_,h_=map(int,input().split())
    x.append(x_)
    h.append(h_)
for i in range(1,n):
    d.append(x[i]-x[i-1])
for i in range(n-1):
    if h[i]<d[i]:
        ans+=1
    elif h[i]<d[i+1]:
        ans+=1
        d[i+1]-=h[i]
ans+=1
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![42930f7deed7c25ae1c066f28914624](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\42930f7deed7c25ae1c066f28914624.png)



### 01328: Radar Installation

greedy, http://cs101.openjudge.cn/practice/01328/

思路：先将x，y坐标转换成在x轴上允许的雷达范围，然后用贪心算法即可。



代码：

```python
from math import sqrt
time=1
while True:
    n,d=map(int,input().split())
    if n==d==0:
        break
    else:
        island=[]
        flag=True
        for _ in range(n):
            x,y=map(int,input().split())
            if y>d:
                flag=False
            # 不能提前break 要等数据都接收完
            else:
                island.append((x-sqrt(d**2-y**2),x+sqrt(d**2-y**2)))
        input()
        if not flag:
            print('Case '+str(time)+': -1')
        else:
            island.sort()
            r,k=0,0
            while k<=n-1:
                r+=1
                end=island[k][1]
                while k<=n-1 and island[k][0]<=end:
                    end=min(island[k][1],end)
                    k+=1
            print('Case '+str(time)+': '+str(r))
        time+=1
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![ae197cce76289501d30efc0f4610493](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\ae197cce76289501d30efc0f4610493.png)



## 2. 学习总结和收获

每日选做现在开始上强度了，有的时候想半天都做不出来还是得看答案，但是还是在努力跟进。优化算法的能力稍微得到了一些锻炼。





