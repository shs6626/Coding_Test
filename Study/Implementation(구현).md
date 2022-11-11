# 구현

<aside>
💡 ‘머릿속에 있는 알고리즘을 소스코드로 바꾸는 과정’

피지컬을 요구하는 문제…

완전 탐색 : 모든 경우의 수를 주저 없이 다 계산하는 해결 방법

100만개 이하일 때 완전 탐색을 사용하면 적절하다

시뮬레이션 : 문제에서 제시한 알고리즘을 한 단계씩 차례대로 직접 수행

</aside>

- 상하좌우
    
    ```python
    import sys
    input = sys.stdin.readline
    
    n = int(input())
    x,y = 1,1
    plans = input().split()
    
    #(x,y)라는 것을 인지하자 단순히 xy축 그래프라고 생각하면 헷갈릴수도...
    dx= [0,0,-1,1]
    dy=[-1,1,0,0]
    move_types = ['L', 'R', 'U', 'D']
    
    for plan in plans:
        for i in range(4):
            if plan == move_types[i]:
                nx = x +dx[i]
                ny = y +dy[i]
            
        if nx < 1 or ny < 1 or nx > n or ny > n:
            continue # 즉 여기서 다시 for plan in plans로 돌아감 밑에 바꿔주지 않고...
    
        x,y =nx, ny
    
    print(x,y)
    ```
    
- 시작
    
    ```python
    h = int(input())
    
    count =0
    
    for i in range(h+1): #0부터 시작하니까
        for min in range(60): #분
            for sec in range(60): #초
                if '3' in str(i)+str(min)+str(sec):
                    count+=1
    
    print(count)
    ```
    
- 왕실의 나이트
    
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
    
- 게임 개발
    
    ```python
    n,m = map(int,input().split())
    
    #갔던 곳 체크하기 위해서
    d = [[0]*m for _ in range(n)]
    
    x,y,direction = map(int,input().split())
    
    d[x][y]
    
    #맵
    array = []
    
    for i in range(n):
        array.append(list(map(int,input().split())))
    
    #북 동 서 남
    
    #(x,y) 예를 들어서 3,3이 북쪽으로 가게되면 2,3이 되닌까 x는 -1 만큼 y는 0만큼 움직이면 된다 (xy 그래프가 아니다)
    dx = [-1,0,1,0]
    dy = [0,1,0,-1]
    
    #왼쪽이라고 생각하면 헷갈림 (반시계방향으로 생각해라)
    def t_l():
        global direction
        direction -=1
        if direction == -1: # 북쪽에서 서쪽으로 돌면 0 - 1 이라 -1이 나오는데 direction은 0~3밖에 없고 서쪽이 3이니까
            direction=3
    
    count=1
    turn_time=0
    while True:
        t_l()
        nx = x+dx[direction]
        ny = y+dy[direction]
    
        if d[nx][ny] == 0 and array[nx][ny]==0:
            d[nx][ny] = 1 # 한번 갔기 때문에 1로 바꿔줌
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
    
            turn_time =0 #1단계로 돌아간다
    
    print(count)
    ```