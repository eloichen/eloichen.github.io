# Assignment #1: 自主学习

2024 fall, Complied by ==陈一匡 物理学院==





## 1. 题目

### 02733: 判断闰年

http://cs101.openjudge.cn/practice/02733/



思路：按照题目给的判断方式一行一行判断 大致花费10min



##### 代码

```python
a=input()
a=int(a)
if a%4!=0:
    print('N')
elif a%100!=0:
    print('Y')
elif a%100==0:
    if a%400!=0:
        print('N')
    elif a%400==0:
        if a%3200==0:
            print('N')
        if a%3200!=0:
            print('Y')   


```



代码运行截图 ==（至少包含有"Accepted"）==



![8466c82ac97163722b426a123f1672a](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\8466c82ac97163722b426a123f1672a.png)

### 02750: 鸡兔同笼

http://cs101.openjudge.cn/practice/02750/



思路：最大除以2，最小除以4，奇数的话不符合要求。 大致花费5min



##### 代码

```python
a=int(input())
if a%4==0:
    min=int(a/4)
    max=int(a/2)
else:
    if a%2==0:
        min=int((a-2)/4+1)
        max=int(a/2)
    else:
        min=0
        max=0   
print(str(min)+" "+str(max))

```



代码运行截图 ==（至少包含有"Accepted"）==



![c5357ab57bcb7d13ac8f83c0a608fb1](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\c5357ab57bcb7d13ac8f83c0a608fb1.png)

### 50A. Domino piling

greedy, math, 800, http://codeforces.com/problemset/problem/50/A



思路：最多排列的话，偶数格全部排满，奇数格剩1格。 大致花费5min



##### 代码

```python
m,n=int(input().split())
a=m*n
if a%2==0:
    c=int(a/2)
elif a%2!=0:
    c=int((a-1)/2)
print(c)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![f0a87d3a131724ca549292f51aea644](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\f0a87d3a131724ca549292f51aea644.png)



### 1A. Theatre Square

math, 1000, https://codeforces.com/problemset/problem/1/A



思路：横竖需要的格数相乘。 大致花费5min



##### 代码

```python
A=input().split()
n=int(A[0])
m=int(A[1])
a=int(A[2])
if m%a==0:
    M=m/a
else:
    M=int(m/a)+1
if n%a==0:
    N=n/a
else:
    N=int(n/a)+1
d=M*N
print(str(int(d)))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![71b36c0ed9a9555e9d09cd607db3e1a](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\71b36c0ed9a9555e9d09cd607db3e1a.png)



### 112A. Petya and Strings

implementation, strings, 1000, http://codeforces.com/problemset/problem/112/A



思路：将字符串全部转换为小写形式之后直接比较字符串大小即可。 大致花费7min



##### 代码

```python
a=input()
b=input()
a_1=a.lower()
b_1=b.lower()
if a_1<b_1:
    print("-1")
elif a_1==b_1:
    print("0")
elif a_1>b_1:
    print("1")
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![ff7e23ded4d121d34b70d8d22e1561c](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\ff7e23ded4d121d34b70d8d22e1561c.png)



### 231A. Team

bruteforce, greedy, 800, http://codeforces.com/problemset/problem/231/A



思路：每行和大于2的话就计数+1。 大致花费5min



##### 代码

```python
number=int(input())
n=0
for k in range(0,number):
    q=input().split()
    s=int(q[0])+int(q[1])+int(q[2])
    if s>=2:
        n+=1
    else:
        continue
print(n)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![fc4f06ad5ede6848fad158633038635](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\fc4f06ad5ede6848fad158633038635.png)



## 2. 学习总结和收获

熟悉了python的基本语法。

做了计概的每日选做题目。