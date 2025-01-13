# Assign #3: Oct Mock Exam暨选做题目满百

Updated 1537 GMT+8 Oct 10, 2024

2024 fall, Complied by 陈一匡 物理学院



**说明：**

1）Oct⽉考： AC5。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++/C（已经在Codeforces/Openjudge上AC），截图（包含Accepted, 学号），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、作业评论有md或者doc。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E28674:《黑神话：悟空》之加密

http://cs101.openjudge.cn/practice/28674/



思路：利用ascii码将字母转化，需要区分大小写。  5min



代码

```python
k=int(input())
s=input()
for i in s:
    if 65<=ord(i)<=90:
        print(chr((ord(i)-k-65)%26+65),end='')
    else:
        print(chr((ord(i)-k-97)%26+97),end='')
```



代码运行截图 ==（至少包含有"Accepted"）==

![beb9a056e4b9d7e8b86b0acad5eb8ed](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\beb9a056e4b9d7e8b86b0acad5eb8ed.png)



### E28691: 字符串中的整数求和

http://cs101.openjudge.cn/practice/28691/



思路：去掉末尾的字母之后相加即可。   5min



代码

```python
a,b=input().split()
a_=int(a[:2])
b_=int(b[:2])
print(a_+b_)
```



代码运行截图 ==（至少包含有"Accepted"）==

![ebea957dd6b5d867ffcaa9a928a5200](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\ebea957dd6b5d867ffcaa9a928a5200.png)

### M28664: 验证身份证号

http://cs101.openjudge.cn/practice/28664/



思路：照着题目的方式验证即可  20min



代码

```python
n=int(input())
l=[7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2]
a=['1','0','X','9','8','7','6','5','4','3','2']
for _ in range(n):
    s=input()
    ans=0
    for i in range(17):
        ans+=int(s[i])*l[i]
    if s[17]==a[ans%11]:
        print('YES')
    else:
        print('NO')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![d96bd230fb0bd1f36d1d540634b587a](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\d96bd230fb0bd1f36d1d540634b587a.png)



### M28678: 角谷猜想

http://cs101.openjudge.cn/practice/28678/



思路：用while循环判断是否到1   10min



代码

```python
a=int(input())
while a!=1:
    if a%2==0:
        print(str(a)+'/2='+str(a//2))
        a=a//2
    else:
        print(str(a)+'*3+1='+str(a*3+1))
        a=a*3+1
print('End')

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![f92fcf46bacbdd0d600dc5257d78df3](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\f92fcf46bacbdd0d600dc5257d78df3.png)



### M28700: 罗马数字与整数的转换

http://cs101.openjudge.cn/practice/28700/



思路：一步一步照着题目来，需要特殊判断4和9。  30min



##### 代码

```python
r={'I':1,'V':5,'X':10,'L':50,'C':100,'D':500,'M':1000}
s=input()
if s[0] in r:
    ans,i=0,0
    while i<=len(s)-1:
        if i<len(s)-1 and s[i]=='I' and ( s[i+1]=='V' or s[i+1]=='X' ):
            ans+=-1+r[s[i+1]]
            i+=2
        elif i<len(s)-1 and s[i]=='X' and ( s[i+1]=='L' or s[i+1]=='C' ):
            ans+=-10+r[s[i+1]]
            i+=2
        elif i<len(s)-1 and s[i]=='C' and ( s[i+1]=='D' or s[i+1]=='M' ):
            ans+=-100+r[s[i+1]]
            i+=2
        else:
            ans+=r[s[i]]
            i+=1
    print(ans)
else:
    n=int(s)
    a=n//1000
    print('M'*a,end='')
    b=(n-1000*a)//100
    if b<4:
        print('C'*b,end='')
    elif b==4:
        print('CD',end='')
    elif 4<b<9:
        print('D'+'C'*(b-5),end='')
    elif b==9:
        print('CM',end='')
    c=(n-1000*a-100*b)//10
    if c<4:
        print('X'*c,end='')
    elif c==4:
        print('XL',end='')
    elif 4<c<9:
        print('L'+'X'*(c-5),end='')
    elif c==9:
        print('XC',end='')
    d=n-1000*a-100*b-10*c
    if d<4:
        print('I'*d,end='')
    elif d==4:
        print('IV',end='')
    elif 4<d<9:
        print('V'+'I'*(d-5),end='')
    elif d==9:
        print('IX',end='')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![ffd5afb88aa0e1fd65aa0e06ec09de6](C:\Users\33722\Documents\WeChat Files\wxid_hmxlx6ziit6222\FileStorage\Temp\ffd5afb88aa0e1fd65aa0e06ec09de6.png)



### *T25353: 排队 （选做）

http://cs101.openjudge.cn/practice/25353/



思路：没什么思路，还在研究



代码

```python


```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





## 2. 学习总结和收获

这次考试前面五题比较简单，第六题想了半天实在是没有什么思路，还在研究。现在初步学习了一些算法，做简单和中等题目都比较得心应手。每日选做有跟进。











