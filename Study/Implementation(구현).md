# ๊ตฌํ

<aside>
๐ก โ๋จธ๋ฆฟ์์ ์๋ ์๊ณ ๋ฆฌ์ฆ์ ์์ค์ฝ๋๋ก ๋ฐ๊พธ๋ ๊ณผ์ โ

ํผ์ง์ปฌ์ ์๊ตฌํ๋ ๋ฌธ์ โฆ

์์  ํ์ : ๋ชจ๋  ๊ฒฝ์ฐ์ ์๋ฅผ ์ฃผ์  ์์ด ๋ค ๊ณ์ฐํ๋ ํด๊ฒฐ ๋ฐฉ๋ฒ

100๋ง๊ฐ ์ดํ์ผ ๋ ์์  ํ์์ ์ฌ์ฉํ๋ฉด ์ ์ ํ๋ค

์๋ฎฌ๋ ์ด์ : ๋ฌธ์ ์์ ์ ์ํ ์๊ณ ๋ฆฌ์ฆ์ ํ ๋จ๊ณ์ฉ ์ฐจ๋ก๋๋ก ์ง์  ์ํ

</aside>

- ์ํ์ข์ฐ
    
    ```python
    import sys
    input = sys.stdin.readline
    
    n = int(input())
    x,y = 1,1
    plans = input().split()
    
    #(x,y)๋ผ๋ ๊ฒ์ ์ธ์งํ์ ๋จ์ํ xy์ถ ๊ทธ๋ํ๋ผ๊ณ  ์๊ฐํ๋ฉด ํท๊ฐ๋ฆด์๋...
    dx= [0,0,-1,1]
    dy=[-1,1,0,0]
    move_types = ['L', 'R', 'U', 'D']
    
    for plan in plans:
        for i in range(4):
            if plan == move_types[i]:
                nx = x +dx[i]
                ny = y +dy[i]
            
        if nx < 1 or ny < 1 or nx > n or ny > n:
            continue # ์ฆ ์ฌ๊ธฐ์ ๋ค์ for plan in plans๋ก ๋์๊ฐ ๋ฐ์ ๋ฐ๊ฟ์ฃผ์ง ์๊ณ ...
    
        x,y =nx, ny
    
    print(x,y)
    ```
    
- ์์
    
    ```python
    h = int(input())
    
    count =0
    
    for i in range(h+1): #0๋ถํฐ ์์ํ๋๊น
        for min in range(60): #๋ถ
            for sec in range(60): #์ด
                if '3' in str(i)+str(min)+str(sec):
                    count+=1
    
    print(count)
    ```
    
- ์์ค์ ๋์ดํธ
    
    ```
    input_data = input()
    row = int(input_data[1])
    column = int(ord(input_data[0])-int(ord('a')))+1
    
    steps = [(-2, -1), (-1, -2), (1, -2), (2, -1), (2,1), (1,2), (-1, 2), (-2, 1)]
    
    count=0
    
    for step in steps:
        next_row = row +step[0]
        next_column = column + step[1]
    
        if next_row >=1 and next_row <=8 and next_column >=1 and next_column <=8 :
            count +=1
    
    print(count)
    ```
    
- ๊ฒ์ ๊ฐ๋ฐ
    
    ```python
    n,m = map(int,input().split())
    
    #๊ฐ๋ ๊ณณ ์ฒดํฌํ๊ธฐ ์ํด์
    d = [[0]*m for _ in range(n)]
    
    x,y,direction = map(int,input().split())
    
    d[x][y]
    
    #๋งต
    array = []
    
    for i in range(n):
        array.append(list(map(int,input().split())))
    
    #๋ถ ๋ ์ ๋จ
    
    #(x,y) ์๋ฅผ ๋ค์ด์ 3,3์ด ๋ถ์ชฝ์ผ๋ก ๊ฐ๊ฒ๋๋ฉด 2,3์ด ๋๋๊น x๋ -1 ๋งํผ y๋ 0๋งํผ ์์ง์ด๋ฉด ๋๋ค (xy ๊ทธ๋ํ๊ฐ ์๋๋ค)
    dx = [-1,0,1,0]
    dy = [0,1,0,-1]
    
    #์ผ์ชฝ์ด๋ผ๊ณ  ์๊ฐํ๋ฉด ํท๊ฐ๋ฆผ (๋ฐ์๊ณ๋ฐฉํฅ์ผ๋ก ์๊ฐํด๋ผ)
    def t_l():
        global direction
        direction -=1
        if direction == -1: # ๋ถ์ชฝ์์ ์์ชฝ์ผ๋ก ๋๋ฉด 0 - 1 ์ด๋ผ -1์ด ๋์ค๋๋ฐ direction์ 0~3๋ฐ์ ์๊ณ  ์์ชฝ์ด 3์ด๋๊น
            direction=3
    
    count=1
    turn_time=0
    while True:
        t_l()
        nx = x+dx[direction]
        ny = y+dy[direction]
    
        if d[nx][ny] == 0 and array[nx][ny]==0:
            d[nx][ny] = 1 # ํ๋ฒ ๊ฐ๊ธฐ ๋๋ฌธ์ 1๋ก ๋ฐ๊ฟ์ค
            x = nx
            y = ny
            count += 1
            turn_time = 0
            continue
        else:
            turn_time +=1
    
            nx = x - dx[direction]
            ny = y - dy[direction]
    
            if array[nx][ny] == 0:
                x = nx
                y = ny
    
            else:
                break
    
            turn_time =0 #1๋จ๊ณ๋ก ๋์๊ฐ๋ค
    
    print(count)
    ```