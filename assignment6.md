# Assignment #6: Recursion and DP

Updated 2201 GMT+8 Oct 29, 2024

2024 fall, Complied by <mark>陈一匡 物理学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### sy119: 汉诺塔

recursion, https://sunnywhy.com/sfbj/4/3/119  

思路：把n个的问题转换为一步加上两个n-1步的问题



代码：

```python
i=0
def f(a,b,c,n):
    global i,ans
    i+=1
    if n==1:
        ans.append(a+'->'+c)
    else:
        f(a,c,b,n-1)
        ans.append(a+'->'+c)
        f(b,a,c,n-1)

n=int(input())
ans=[]
f('A','B','C',n)
print(i)
print('\n'.join(ans))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![bd330f134294fe4fa1a33e263e6b23c](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\bd330f134294fe4fa1a33e263e6b23c.png)



### sy132: 全排列I

recursion, https://sunnywhy.com/sfbj/4/3/132

思路：没有什么思路，看了答案才会做的



代码：

```python
def f(n,d,used,temp,ans):
    if d==n:
        ans.append(temp[:])
        return
    else:
        for i in range(n):
            if not used[i]:
                temp.append(i+1)
                used[i]=True
                f(n,d+1,used,temp,ans)
                temp.pop()
                used[i]=False

n=int(input())
ans=[]
used=[False]*n
f(n,0,used,[],ans)
for l in ans:
    print(*l)
```



代码运行截图 ==（至少包含有"Accepted"）==

![a61ad27345c866fc032b6b954d4888f](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\a61ad27345c866fc032b6b954d4888f.png)



### 02945: 拦截导弹 

dp, http://cs101.openjudge.cn/2024fallroutine/02945

思路：也是看了答案才会做的



代码：

```python
k=int(input())
l=list(map(int,input().split()))
max_l=[1]*k
for i in range(k):
    for j in range(i):
        if l[j]>=l[i]:
            max_l[i]=max(max_l[i],max_l[j]+1)
print(max(max_l))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![424aa0efb8f7591f9b7a7cc0ab58b06](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\424aa0efb8f7591f9b7a7cc0ab58b06.png)



### 23421: 小偷背包 

dp, http://cs101.openjudge.cn/practice/23421

思路：用的是算法图解的思路



代码：

```python
n,b=map(int,input().split())
p=list(map(int,input().split()))
w=list(map(int,input().split()))
v=[[0]*(b+1) for _ in range(n)]
for i in range(n):
    for j in range(b+1):
        if j>=w[i]:
            v[i][j]=max(v[i-1][j],v[i-1][j-w[i]]+p[i])
print(max(v[n-1]))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![de7df9cfac40d7b0101894091510a54](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\de7df9cfac40d7b0101894091510a54.png)



### 02754: 八皇后

dfs and similar, http://cs101.openjudge.cn/practice/02754

思路：感觉和全排列的思路很像，也是建一个二维数组表示当前一步可以选择的点，然后递推到下一步。如果整体深度到达指定要求，就返回一个列表，然后再回溯。



代码：

```python
def f(n,ans,d,allowed,temp,flag):
    if sum(allowed[d])==0 or not flag:
        flag=False
        return
    elif d==n-1:
        temp.append(allowed[d].index(1)+1)
        ans.append(temp[:])
        temp.pop()
        return
    else:
        for i in range(n):
            if allowed[d][i]==1:
                temp.append(i+1)
                allowed_new=[m[:] for m in allowed]
                for j in range(d,n):
                    allowed_new[j][i]=0
                    if i-d+j<=n-1:
                        allowed_new[j][i-d+j]=0
                    if i+d-j>=0:
                        allowed_new[j][i+d-j]=0
                f(n,ans,d+1,allowed_new,temp,flag)
                temp.pop()

n=8
ans=[]
allowed=[[1]*n for _ in range(n)]
f(n,ans,0,allowed,[],True)
t=int(input())
for i in range(t):
    m=int(input())
    print(''.join(map(str,ans[m-1])))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![24db092b674bb2ee8ecd06ef5a75e6b](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\24db092b674bb2ee8ecd06ef5a75e6b.png)



### 189A. Cut Ribbon 

brute force, dp 1300 https://codeforces.com/problemset/problem/189/A

思路：和小偷背包的思路很像，建立二维数组表示要切掉a，b，c中一段的最大段数，然后取最大值。



代码：

```python
n,a,b,c=map(int,input().split())
d=[a,b,c]
l=[[0]+[-1]*n for _ in range(3)]
for i in range(1,n+1):
    for j in range(3):
        if i>=d[j]:
            l[j][i]=max(l[0][i-d[j]],l[1][i-d[j]],l[2][i-d[j]])+1
            if l[j][i]==0:
                l[j][i]=-1
print(max(l[0][n],l[1][n],l[2][n]))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![7fbd3cef00d396f5f88d317e076c07f](E:\HuaweiMoveData\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\7fbd3cef00d396f5f88d317e076c07f.png)



## 2. 学习总结和收获

感觉现在作业真的是明显变难了，有差不多一半的题目需要看答案的思路才能自己写出来代码，另一半是根据前面一半的代码的思路想出来的。现在每日选做还尽量在跟上，希望不久之后可以掌握dp。





