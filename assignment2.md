# Assignment #2: 语法练习

Updated 0126 GMT+8 Sep 24, 2024

2024 fall, Complied by ==陈一匡 物理学院==



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知9月19日导入选课名单后启用。**作业写好后，保留在自己手中，待9月20日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 263A. Beautiful Matrix

https://codeforces.com/problemset/problem/263/A



思路：计算行和列的绝对距离即可。



##### 代码

```python
def f(a):
    for n in range(0,5):
        if int(a[n])==1:
            return n+1
    return False
m=0
for x in range(0,5):
    row=input().split()
    if f(row):
        m=x
        m1=f(row)
p=abs(m-2)+abs(m1-3)
print(p)

```



代码运行截图 ==（至少包含有"Accepted"）==

![06aa1bd1ab94f1010213dbbbdb5495a](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\06aa1bd1ab94f1010213dbbbdb5495a.png)



### 1328A. Divisibility Problem

https://codeforces.com/problemset/problem/1328/A



思路：如果整除的话输出零，如果不整除的话输出整除的最小步数。



##### 代码

```python
n=int(input())
for i in range(0,n):
    x1,x2=input().split()
    a=int(x1)
    b=int(x2)
    r=a%b
    if r==0:
        move=0
    if r!=0:
        move=b-r
    print(move)

```



代码运行截图 ==（至少包含有"Accepted"）==

![41dfe7159373aefe75e816457a09e60](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\41dfe7159373aefe75e816457a09e60.png)



### 427A. Police Recruits

https://codeforces.com/problemset/problem/427/A



思路：创建一个数i表示当前的警员数，如果输入是正的那么警员数增加，如果是负的那么消耗警员数。当i变成0时，增加案件数。



##### 代码

```python
num=int(input())
l=input().split()
list=[int(i) for i in l]
times=0
i=0
for _ in range(num):
    if list[_]>=0:
       i+=list[_]
    else:
        if i==0:
            times+=1
        else:
            i+=list[_]
print(int(times)) 
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![88e395709882c5b8426994c4301d50e](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\88e395709882c5b8426994c4301d50e.png)



### 02808: 校门外的树

http://cs101.openjudge.cn/practice/02808/



思路：创建一个列表表示树的状态，1表示树还在，0表示树被砍掉。最后求和得出总的树的数量。



##### 代码

```python
l,m=map(int,input().split())
tree=[1]*(l+1)
for _ in range(m):
    a,b=map(int,input().split())
    for j in range(a,b+1):
        tree[j]=0
print(sum(tree))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![9a3938af558e641b1d69088e4b2f9cc](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\9a3938af558e641b1d69088e4b2f9cc.png)



### sy60: 水仙花数II

https://sunnywhy.com/sfbj/3/1/60



思路：将一个给定的数转换成字符串，再将每个数分开立方之后求和。如果和等于原数的话就打印这个数，如果没有数就输出NO。



##### 代码

```python
a,b=map(int,input().split())
ans=[]
flag=0
for i in range(a,b+1):
    f=0
    for j in str(i):
        f+=int(j)**3
    if f==i:
        flag=1
        ans.append(str(i))
if flag==1:
    print(' '.join(ans))
else:
    print('NO')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

<img src="C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\1ce6888c195fe711dee6f286836ef46.png" alt="1ce6888c195fe711dee6f286836ef46" style="zoom:50%;" />



### 01922: Ride to School

http://cs101.openjudge.cn/practice/01922/



思路：这题我自己没有什么很好的思路，看了答案才发现只要找到初始时间大于零的人中到达时间最快的时间就好了。



##### 代码

```python
import math
while True:
    n=int(input())
    if n==0:
        break
    else:
        tf=float('inf')
        for _ in range(n):
            v,t=map(int,input().split())
            if t>=0:
                tf=min(tf,math.ceil(t+4500*3.6/v))
        print(tf)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![002585a682d806acbf19f06ca1f8544](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\002585a682d806acbf19f06ca1f8544.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。==

继续跟进每日选做。

做这次作业的时候学习到了float('inf')这个表达无穷大量的语法。



