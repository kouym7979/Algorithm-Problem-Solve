## 백준 문자열 bronze

11721번

```
word=input()

for i in range(0,len(word),10): #0부터 word의 길이까지 구간은 10
    print(word[i:i+10])
```



1110번

```
n=int(input())
check=n
count=0
temp=0
new_num=0
while True:
    temp=n//10+n%10
    new_num=(n%10)*10+temp%10
    count+=1
    n=new_num
    if n==check:
        break
print(count)
```