# Minesweeper
#it is the mine sweeper game in python code but zeroes only semi fill you will see
#run this cone in a python editor idk what version you need ust hope 

import turtle
import random
import time
import itertools

start_time=0

SIZE = 9      # you can change the size of the board with this
MINES = 10    # you can change the number of mines with this (not acctually a constant)
over = False
flaging = False
location = (0, 0)

wn = turtle.Screen()
wn.title("minesweeper")  # 300,300
draw = turtle.Turtle()
draw.hideturtle()
draw.speed(0)
row_size = 600 / SIZE
for i in range(SIZE + 1):
    draw.penup()
    draw.goto(-300 + i * row_size, -300)
    draw.pendown()
    draw.goto(-300 + i * row_size, 300)
for i in range(SIZE + 1):
    draw.penup()
    draw.goto(-300, -300 + i * row_size)
    draw.pendown()
    draw.goto(300, -300 + i * row_size)
draw.penup()

board = []
for i in range(SIZE):
    board.append([])
    for j in range(SIZE):
        board[i].append(0)

locations = random.sample(list(itertools.product(range(SIZE), range(SIZE))), k=MINES)

draw.color("red")
draw.goto(315,20)
draw.write("f",align="center",font=("Verdana",30, "normal"))
draw.goto(305,-20)
draw.pencolor("white")
draw.write(MINES-1,align="left",font=("Verdana",30, "normal"))
draw.pencolor("black")
draw.write(MINES,align="left",font=("Verdana",30, "normal"))

for i in range(MINES):
    locations[i] = list(locations[i])
    x = locations[i][0]
    y = locations[i][1]
    board[y][x] = 1

def get_mouse_click_pos(x, y):
    global MINES
    global flaging
    global start_time
    
    if start_time==0:
        start_time=time.time()
    
    location = (x, y)
    location = list(location)
    
    if location[0]>300:
        flaging=not flaging
        draw.goto(315,20)
        if flaging==False:
            draw.pencolor("red")
        else:
            draw.pencolor("green")
        draw.write("f",align="center",font=("Verdana",30, "normal"))
        
    else:
            
        location[0] += 300
        location[1] += 300
        location[0] = int(location[0] / (600 / SIZE))
        location[1] = int(location[1] / (600 / SIZE))
        
                
        
        #print(location)
        #print(board[location[1]][location[0]])
        
        draw.goto(location[0]*(600 / SIZE)-300+(300/SIZE),location[1]*(600 / SIZE)-300+(300/SIZE)-12)
        
        if board[location[1]][location[0]]==1 and flaging==False:
            draw.pencolor("black")
            draw.goto(0,-150)
            draw.write("L",align="center",font=("Verdana",300, "normal"))
            print("you lost")
            1/0
            time.sleep(10000)
            
        if flaging==False:
            number=0
            for i in range(-1,2,1):
                for j in range(-1,2,1):
                    check=[location[0]+i,location[1]+j]
                    if check[0]>=0 and check[1]>=0 and check[0]<SIZE and check[1]<SIZE:
                        if board[check[1]][check[0]]==1:
                            number+=1
            if number==0:
                draw.pencolor("gray")
                draw.write(number,align="center",font=("Verdana",15, "normal"))
                
                for i in range(-1,2,1):
                    for j in range(-1,2,1):
                        location2=[location[0],location[1]]
                        location2[0]+=i
                        location2[1]+=j
                        number=0
                        for k in range(-1,2,1):
                            for l in range(-1,2,1):
                                check=[location2[0]+k,location2[1]+l]
                                if check[0]>=0 and check[1]>=0 and check[0]<SIZE and check[1]<SIZE:
                                    if board[check[1]][check[0]]==1:
                                        number+=1
                        
                        draw.goto(location2[0]*(600 / SIZE)-300+(300/SIZE),location2[1]*(600 / SIZE)-300+(300/SIZE)-12)
                                        
                        if number==0:
                            draw.pencolor("gray")
                        if number==1:
                            draw.pencolor("blue")
                        if number==2:
                            draw.pencolor("green")
                        if number==3:
                            draw.pencolor("red")
                        if number==4:
                            draw.pencolor("purple")
                        if number==5:
                            draw.pencolor("orange")
                        if number==6:
                            draw.pencolor("cyan")
                        if number>=7:
                            draw.pencolor("brown")
                            
                        if location2[1]>=0 and location2[0]>=0 and location2[1]<SIZE and location2[0]<SIZE:
                            draw.write(number,align="center",font=("Verdana",15, "normal"))
                        
                
            else:
                if number==1:
                    draw.pencolor("blue")
                if number==2:
                    draw.pencolor("green")
                if number==3:
                    draw.pencolor("red")
                if number==4:
                    draw.pencolor("purple")
                if number==5:
                    draw.pencolor("orange")
                if number==6:
                    draw.pencolor("cyan")
                if number>=7:
                    draw.pencolor("brown")
                draw.write(number,align="center",font=("Verdana",15, "normal"))
            
            
            
        else:
            if board[location[1]][location[0]]==1:
                draw.goto(location[0]*(600 / SIZE)-300+(300/SIZE),location[1]*(600 / SIZE)-300+(300/SIZE)-20)
                draw.pencolor("black")
                draw.write("f",align="center",font=("Verdana",20, "bold"))
                
                draw.goto(305,-20)
                draw.pencolor("white")
                draw.write(MINES,align="left",font=("Verdana",30, "normal"))
                MINES-=1
                draw.pencolor("black")
                draw.write(MINES,align="left",font=("Verdana",30, "normal"))
            else:
                draw.goto(0,-150)
                draw.pencolor("black")
                draw.write("L",align="left",font=("Verdana",300, "normal"))
                1/0
                time.sleep(10000)
        
        print("mines remaining =" , MINES)
        print("flag selected =" , flaging)
        print("\n")
        
        
        if MINES==0:
            print("you won in",time.time()-start_time,"secconds")
            
            draw.goto(0,-150)
            draw.write("W",align="left",font=("Verdana",300, "normal"))
            time.sleep(10000)
                
        turtle.update()
        
        


def swap_flag():
    global flaging
    flaging=not flaging
    draw.goto(315,20)
    if flaging==False:
        draw.pencolor("red")
    else:
        draw.pencolor("green")
    draw.write("f",align="center",font=("Verdana",30, "normal"))
    



turtle.listen()
turtle.onscreenclick(get_mouse_click_pos)
turtle.onkey(swap_flag, "f")

turtle.mainloop()

