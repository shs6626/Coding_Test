# 그리디

## 탐욕법

현재 상황에서 지금 당장 좋은 것만 고르는 방법

그리디 알고리즘 유형의 문제는 창의력을 요구한다

- 거스름돈 : [https://www.acmicpc.net/problem/5585](https://www.acmicpc.net/problem/5585)
    
    ```python
    import sys
    
    input =  sys.stdin.readline
    
    n= int(input())
    
    a=1000-n
    count=0
    
    coin =[500,100,50,10,5,1]
    
    for i in coin:
        count += a//i
        a = a%i
    
    print(count)
    ```
    
- 큰 수의 법칙 :
    
    ```python
    import sys
    
    input =  sys.stdin.readline
    
    n,m,k = list(map(int, input().split()))
    
    hong = list(map(int, input().split()))
    
    hong.sort()
    
    a=m%4
    b=m//4
    sum_=hong[-1]*3+hong[-2]
    
    print((b*sum_)+(a*hong[-1]))
    
    #46이 나오기는 하는데 과연 맞을지는..?
    ```
    
- 숫자 카드 게임
    
    ```python
    import sys
    input = sys.stdin.readline
    
    a,b = map(int,input().split())
    
    result=0
    
    for i in range(a):
        card=(list(map(int,input().split())))
    
        min_=min(card)
    
        result= max(result, min_)
    
    print(result)
    ```
    
- 1이 될 때까지
    
    ```python
    import sys
    input = sys.stdin.readline
    
    n,k = map(int,input().split())
    result=0
    while True:
    
        target = (n//k)*k
        result += (n-target)
        n=target
    
        print(target, result, n)
    
        if n < k:
            break
    
        result +=1
        n//=k
    
        print(n)
    ```