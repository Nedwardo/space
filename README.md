```python
import pygame
import pygame.freetype
import random
from pygame.locals import *
global names
global nope
global colour
global event
pygame.init()
names = ["player 1","player 2"]
colour = {}
##SET A FEW RGB COLOURS
colour["black"] = pygame.Color(0,0,0)# black
colour["yellow"] = pygame.Color(255,255,0) # yellow
colour["cyan"] = pygame.Color(0,255,255) # cyan
colour["magenta"] = pygame.Color(255,0,255) # magenta
colour["red"] = pygame.Color(255,0,0) # red
colour["green"] = pygame.Color(0,255,0) # green
colour["blue"] = pygame.Color(0,0,255) # blue
colour["white"] = pygame.Color(255,255,255)#white
colour["rust"] = pygame.Color(183, 65, 14)#rust
colour["puce"] = pygame.Color(204, 136, 153)#puce
colour["orange"] = pygame.Color(255,204,0)
colour["player1token"] = colour["rust"]
colour["player2token"] = colour["puce"]
colour["background"] = colour["yellow"]
colour["safe"] = colour["green"]
colour["unsafe"] = colour["magenta"]
colour["outline"] = colour["cyan"]
colour["gametext"] = colour["red"]
##SORT OUT FONT FOR THE TEXT
txt = pygame.freetype.Font("comic.ttf",15)

nope = 0
turn = 0
def drawmain ():
    while True:
        global Screen
        Screen = pygame.display.set_mode((450,400))
        Screen.fill(colour["white"])
        drawoptions((int(450/10)),(50),(450-int(450*2/10)),(60),"Options",62,(int(450/10)+int((450-int(450*2/10))*20/45)))
        drawoptions((int(450/10)),(150),(450-int(450*2/10)),(60),"Game",150+(60/5),int(450/10)+int(int(450-int(450*2/10))*7/15))
        drawoptions((int(450/10)),(250),(450-int(450*2/10)),(60),"Exit",250+(60/5),((int(450/10))+int((450-int(450*2/10))*7/15)))
        pygame.display.update()
        main_choice(chooseoption())

drawoptions(boardHeight/2,boardWidth/2,(450-int(450*2/10)),(60),"exit" ,boardHeight/2,boardWidth/2)
        
def chooseoption():
    while True:
        event = pygame.event.poll()
        if event.type == "QUIT":
            pygame.quit()
            exit()
            
        if event.type == MOUSEBUTTONDOWN:
            if pygame.mouse.get_pos()[1] in range(50,110) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)):            
                return(1)
            elif pygame.mouse.get_pos()[1] in range(150,210) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)):
                return(2)
            elif pygame.mouse.get_pos()[1] in range(250,310) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)):
                return(3)
                
def main_choice (choice):
    if choice == 1:
        options()
    elif choice == 2:
        Game() # LINK START-O
    elif choice == 3:
        pygame.quit()
        exit()

    
def options():
    displayoptions()
    optionhandle((chooseoption()-1))

def displayoptions():
    Screen.fill(colour["white"])
    drawoptions((int(450/10)),(50),(450-int(450*2/10)),(60),"Input names",62,(int(450/10)+139))
    drawoptions((int(450/10)),(150),(450-int(450*2/10)),(60),"Change colours",162,int(450/10)+129)
    drawoptions((int(450/10)),(250),(450-int(450*2/10)),(60),"Back",262,int(450/10)+166.5)
    pygame.display.flip()
    
    
def optionhandle(buttonpress):
    if buttonpress == 0:
        names = handle_names()
    elif buttonpress == 1:
        changecolourslist()
    else:
        return()
        

def handle_names():
    playernames1 = ""
    playernames2 = ""
    Screen.fill(colour["white"])
    txt.render_to(Screen,(0,0),"Player 1 names: ", colour["black"])
    txt.render_to(Screen,(0,50),"Player 2 names: ", colour["black"])
    drawoptions((int(450/10)),(250),(450-int(450*2/10)),(60),"Exit",262,int(450/10)+166.5)
    pygame.display.flip()
    while True:
        event = pygame.event.poll()
        pygame.display.flip()
        endwhile = 0
        if event.type == "QUIT":
            pygame.quit()
            exit()
        if event.type == MOUSEBUTTONDOWN:
            if pygame.mouse.get_pos()[1] in range (0,10) and pygame.mouse.get_pos()[0] in range (94,450):
                while endwhile == 0:
                    Screen.fill(colour["white"])
                    txt.render_to(Screen,(0,0),"Player 1 names: ", colour["orange"])
                    txt.render_to(Screen,(0,50),"Player 2 names: ", colour["black"])
                    txt.render_to(Screen,(220,3),str(playernames1), colour["black"])
                    txt.render_to(Screen,(220,53),str(playernames2), colour["black"])
                    drawoptions(45,250,360,60,"Exit",262,211.5)
                    pygame.display.flip()
                    endwhile,playernames1 = inputnames(playernames1,300,14)
            elif pygame.mouse.get_pos()[1] in range (50,60) and pygame.mouse.get_pos()[0] in range (94,450):
                while endwhile == 0:
                    Screen.fill(colour["white"])
                    txt.render_to(Screen,(0,0),"Player 1 names: ", colour["black"])
                    txt.render_to(Screen,(0,50),"Player 2 names: ", colour["orange"])
                    txt.render_to(Screen,(220,3),str(playernames1), colour["black"])
                    txt.render_to(Screen,(220,53),str(playernames2), colour["black"])
                    drawoptions(45,250,360,60,"Exit",262,211.5)
                    pygame.display.flip()
                    endwhile,playernames2 = inputnames(playernames2,300,14)
            elif pygame.mouse.get_pos()[1] in range(250,310) and pygame.mouse.get_pos()[0] in range(45,405):
                return[playernames1,playernames2]


def inputnames(value,keylimitupper,keylimitlower):
    ValueList = []
    stop = 0
    event = pygame.event.poll()
    if event.type == "QUIT":
        pygame.quit()
        exit()
    if event.type == KEYDOWN and event.key < keylimitupper and event.key > keylimitlower:
        letter = event.unicode  
        if len(value) < 10:  
            value += letter
    elif event.type == KEYDOWN and event.key == 8:    
        for i in value:
            ValueList += i
        if ValueList != []:
            ValueList.pop()
        value = ""
        for i in range(0, len(ValueList)):
            value += ValueList[i]
        ValueList = []
    elif event.type == KEYDOWN and event.key == 13:
        stop = 1
    return stop,value

def changecolourslist():
    Screen.fill(colour["white"])
    drawoptions(45,(27),360,27,"Change " +str(names[0]) +" token colour",30,127)
    drawoptions(45,(80),360,27,"Change " +str(names[1]) +" token colour",85,125)
    drawoptions(45,(133),360,27,"Change Background colour",138,129)
    drawoptions(45,(187),360,27,"Change Safe Tile colour",192,120)
    drawoptions(45,(240),360,27,"Change Unsafe Tile colour",245,130)
    drawoptions(45,(293),360,27,"Change Outline colour",298,144.5)
    drawoptions(45,(347),360,27,"Change Gametext colour",352,136)
    pygame.display.flip()
    while True:
        event = pygame.event.poll()
        if event.type == MOUSEBUTTONDOWN:
            if pygame.mouse.get_pos()[1] in range(27,54) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)):            
                colour["player1token"] = optioncolour()
            elif pygame.mouse.get_pos()[1] in range(80,107) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)):
                colour["player2token"] = optioncolour()
            elif pygame.mouse.get_pos()[1] in range(133,160) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)):
                colour["background"] = optioncolour()
            elif pygame.mouse.get_pos()[1] in range(187,214) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)):
                colour["safe"] = optioncolour()
            elif pygame.mouse.get_pos()[1] in range(240,267) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)):
                colour["unsafe"] = optioncolour()
            elif pygame.mouse.get_pos()[1] in range(293,320) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)):
                colour["outline"] = optioncolour()
            elif pygame.mouse.get_pos()[1] in range(347,374) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)):
                colour["gametext"] = optioncolour()

def optioncolour():
    R = ""
    G = ""
    B = ""
    End = 1
    Screen.fill(colour["white"])
    txt.render_to(Screen,(100,0),"Please input the RGB values of the colour", colour["black"])
    txt.render_to(Screen,(0,50),"R:", colour["black"])
    txt.render_to(Screen,(0,100),"G:", colour["black"])
    txt.render_to(Screen,(0,150),"B:", colour["black"])
    while True:
            event = pygame.event.poll()
            pygame.display.flip()
            endwhile = 0
            if event.type == "QUIT":
                pygame.quit()
                exit()
            if event.type == MOUSEBUTTONDOWN:
                if pygame.mouse.get_pos()[1] in range (50,60) and pygame.mouse.get_pos()[0] in range (94,450):
                    while End == 0:
                        Screen.fill(colour["white"])
                        txt.render_to(Screen,(100,0),"Please input the RGB values of the colour", colour["black"])
                        txt.render_to(Screen,(0,50),"R:", colour["orange"])
                        txt.render_to(Screen,(0,100),"G:", colour["black"])
                        txt.render_to(Screen,(0,150),"B:", colour["black"])
                        txt.render_to(Screen,(220,53),str(R), colour["black"])
                        txt.render_to(Screen,(220,103),str(G), colour["black"])
                        txt.render_to(Screen,(220,153),str(B), colour["black"])
                        drawoptions(45,250,360,60,"Input Values",262,211.5)
                        pygame.display.flip()
                        End,R = inputnames(R,57,48)
                elif pygame.mouse.get_pos()[1] in range (100,110) and pygame.mouse.get_pos()[0] in range (94,450):
                    while End == 0:
                        Screen.fill(colour["white"])
                        txt.render_to(Screen,(100,0),"Please input the RGB values of the colour", colour["black"])
                        txt.render_to(Screen,(0,50),"R:", colour["black"])
                        txt.render_to(Screen,(0,100),"G:", colour["orange"])
                        txt.render_to(Screen,(0,150),"B:", colour["black"])
                        txt.render_to(Screen,(220,53),str(R), colour["black"])
                        txt.render_to(Screen,(220,103),str(G), colour["black"])
                        txt.render_to(Screen,(220,153),str(B), colour["black"])
                        drawoptions(45,250,360,60,"Input Values",262,211.5)
                        pygame.display.flip()
                        End,G = inputnames(G,57,48)
                elif pygame.mouse.get_pos()[1] in range (150,160) and pygame.mouse.get_pos()[0] in range (94,450):
                    while endwhile == 0:
                        Screen.fill(colour["white"])
                        txt.render_to(Screen,(100,0),"Please input the RGB values of the colour", colour["black"])
                        txt.render_to(Screen,(0,50),"R:", colour["black"])
                        txt.render_to(Screen,(0,100),"G:", colour["black"])
                        txt.render_to(Screen,(0,150),"B:", colour["orange"])
                        txt.render_to(Screen,(220,53),str(R), colour["black"])
                        txt.render_to(Screen,(220,103),str(G), colour["black"])
                        txt.render_to(Screen,(220,153),str(B), colour["black"])
                        drawoptions(45,250,360,60,"Input Values",262,211.5)
                        pygame.display.flip()
                        End,B = inputnames(B,57,48)
                elif pygame.mouse.get_pos()[1] in range(250,310) and pygame.mouse.get_pos()[0] in range(45,405):
                    return(pygame.Color(int(R),int(G),int(B)))
#        inputnames(playernames,57,48):

###########GAME##########################
def Game():
    pygame.init()
    ##start UP PYGAME
    global counterinfo
    counterinfo = [0,0,0,0]
    turn_number = 1
    

    ##LETS DEFINE SOME SIZES
    boardWidth = 1000
    boardHeight = 550 # defult 550
    rowheight = 50
    tokencolumwidth = 500
    infocolumwidth = 100
    circleradi = 15
    circle_x_pos_limits = []
    circle_y_pos_limits = []
    for countup in range (0,4):
        circle_y_pos_limits += [[int(10.5*rowheight),int((10.5*rowheight)-circleradi),int((10.5*rowheight)+circleradi)]]



    ##GIVE THE WINDOW A names
    Screen = pygame.display.set_mode((boardWidth,boardHeight))
    def define_circle_x_pos_limits(infocolumwidth,lcountup):
        if lcountup%2 == 0:
            temp_store =[(infocolumwidth+int(((lcountup+2)/2)*80)),((infocolumwidth+int(((lcountup+2)/2)*80))-circleradi),((infocolumwidth+int(((lcountup+2)/2)*80))+circleradi)]
        else:
            temp_store =[(infocolumwidth+int(((lcountup+5)/2)*80)),((infocolumwidth+int(((lcountup+5)/2)*80))-circleradi),((infocolumwidth+int(((lcountup+5)/2)*80))+circleradi)]
        return temp_store
    circle_x_pos_limits = [define_circle_x_pos_limits(infocolumwidth,iterate) for iterate in range (0,4)]

        
    def drawcolums(rownumber): # this draws all the colums that the user sees (inculding the text)
        row = 525 - 50 * rownumber
        if rownumber+1 == 11:
            txt.render_to(Screen,(10,row) ,str(rownumber+1)+ " - FINISH", colour["gametext"])
        elif rownumber+1 == 1:
            txt.render_to(Screen,(10,row) ,str(rownumber+1) + " - START", colour["gametext"])
        else:
            txt.render_to(Screen,(10,row) ,str(rownumber+1), colour["gametext"])
        pygame.draw.rect(Screen,colour["outline"],(0,(10-rownumber)*rowheight,infocolumwidth,rowheight),5)
        if rownumber == 0 or rownumber == 4 or rownumber == 10:
            pygame.draw.rect(Screen,colour["safe"],(infocolumwidth,(10-rownumber)*rowheight,tokencolumwidth,rowheight))
        else:
            pygame.draw.rect(Screen,colour["unsafe"],(infocolumwidth,(10-rownumber)*rowheight,tokencolumwidth,rowheight))
        pygame.draw.rect(Screen,colour["outline"],(infocolumwidth,(10-rownumber)*rowheight,tokencolumwidth,rowheight),5)

    def diceroll(sides):
        diceroll = random.randrange(0,sides)
        if diceroll ==  0:
            print("you can move one of your pieces up one")
        elif diceroll == 1:
            print("you can move one of your pieces up two")
        elif diceroll == 2:
            print("you can move one of your pieces up three")
        elif diceroll == 3:
            print("you can move one of your pieces back one")
        else:
            print("you can move one of pieces to the next empty space")
        return diceroll
        

    def drawcounter(counternumber,counterlist):#this draws the users counters on the board
        if counternumber%2 == 0:
            pygame.draw.circle(Screen,colour["player1token"],(int(circle_x_pos_limits[counternumber][0]),int(circle_y_pos_limits[counternumber][0])),circleradi)
        else:
            pygame.draw.circle(Screen,colour["player2token"],(int(circle_x_pos_limits[counternumber][0]),int(circle_y_pos_limits[counternumber][0])),circleradi)


    def press_counter(roll,turnno):
        print("please select the counter you wish to move")
        while True:
            event = pygame.event.poll()
            if event.type == MOUSEBUTTONDOWN:
                if pygame.mouse.get_pos()[1] in range(int(circle_y_pos_limits[turnno%2][1]),int(circle_y_pos_limits[turnno%2][2])) and pygame.mouse.get_pos()[0] in range(circle_x_pos_limits[turnno%2][1],circle_x_pos_limits[turnno%2][2]):            
                    return(turnno%2)
                elif pygame.mouse.get_pos()[1] in range(int(circle_y_pos_limits[turnno%2+2][1]),int(circle_y_pos_limits[turnno%2+2][2])) and pygame.mouse.get_pos()[0] in range(circle_x_pos_limits[turnno%2+2][1],circle_x_pos_limits[turnno%2+2][2]):
                    return((turnno%2)+2)
            if event.type == "QUIT":
                drawmain()

    def movecounter(dice_roll,counter_number,turn_count):
        if dice_roll < 3 and (counterinfo[counter_number]+ dice_roll+1) > 10:
            counterinfo[counter_number] = 10
            circle_y_pos_limits[counter_number][0] = 0.5*rowheight
            circle_y_pos_limits[counter_number][1] = 0.5*rowheight - circleradi
            circle_y_pos_limits[counter_number][2] = 0.5*rowheight + circleradi
        else:
            if dice_roll < 3:
                counterinfo[counter_number] += dice_roll+1
                circle_y_pos_limits[counter_number][0] -= (dice_roll+1)*rowheight
                circle_y_pos_limits[counter_number][1] -= (dice_roll+1)*rowheight
                circle_y_pos_limits[counter_number][2] -= (dice_roll+1)*rowheight
            elif dice_roll == 3:
                counterinfo[counter_number] -= 1
                circle_y_pos_limits[counter_number][0] += rowheight
                circle_y_pos_limits[counter_number][1] += rowheight
                circle_y_pos_limits[counter_number][2] += rowheight
        moveback(turn_number)
                
    def choosecounter(dice,turn):
        validmoves = []
        validmoves =(vaildmove(dice,turn))

        if validmoves == [True,True]:
            movecounter(dice,press_counter(dice,turn),turn)

        elif validmoves == [True,False]:
            movecounter(dice,turn%2,turn)

        elif validmoves == [False,True]:                         
            movecounter(dice,turn%2+2,turn)
        else:
            print("no valid moves")

    def vaildmove(dice_roll,turn_number):
        counters = [counterinfo[(turn_number%2)],counterinfo[(turn_number%2+2)]]
        possible_moves = [False,False]
        if dice_roll < 3:
            for counter_countup in range(0,2):
                if counters[counter_countup] != counters[1-counter_countup]-(dice_roll+1):
                    possible_moves[counter_countup] = True    
                if counters[1-counter_countup] == 4 or counters[1-counter_countup] == 10:
                    possible_moves[counter_countup] = True
                if counters[counter_countup] == 10:
                    possible_moves[counter_countup] = False

        elif dice_roll == 3:
            for counter_countup in range(0,2):
                if counters[counter_countup] != counters[1-counter_countup]+1: 
                    possible_moves[counter_countup] = True
                if counters[1-counter_countup] == 4 or counters[1-counter_countup] == 0:
                    possible_moves[counter_countup] = True
                if counters[counter_countup] == 0:
                    possible_moves[counter_countup] = False
        
        return possible_moves
    
    def moveback (turn_number):
        if counterinfo[(turn_number%2)] == counterinfo[((turn_number+1)%2)] and not (counterinfo[(turn_number%2)] == 0 | counterinfo[(turn_number%2)] == 4  | counterinfo[(turn_number%2)] == 10):
            counterinfo[((turn_number+1)%2)] = 0
            circle_y_pos_limits[((turn_number+1)%2)] = [int(10.5*rowheight),int((10.5*rowheight)-circleradi),int((10.5*rowheight)+circleradi)]
            
        if counterinfo[(turn_number%2)] == counterinfo[((turn_number+1)%2)+2] and not (counterinfo[(turn_number%2)] == 0 | counterinfo[(turn_number%2)] == 4  | counterinfo[(turn_number%2)] == 10):
            counterinfo[((turn_number+1)%2)+2] = 0
            circle_y_pos_limits[((turn_number+1)%2)+2] = [int(10.5*rowheight),int((10.5*rowheight)-circleradi),int((10.5*rowheight)+circleradi)]
            
        if counterinfo[(turn_number%2)+2] == counterinfo[((turn_number+1)%2)] and not (counterinfo[(turn_number%2)] == 0 | counterinfo[(turn_number%2)] == 4  | counterinfo[(turn_number%2)] == 10):
            counterinfo[((turn_number+1)%2)] = 0
            circle_y_pos_limits[((turn_number+1)%2)] = [int(10.5*rowheight),int((10.5*rowheight)-circleradi),int((10.5*rowheight)+circleradi)]
            
        if counterinfo[(turn_number%2)+2] == counterinfo[(((turn_number+1)%2)+2)] and not (counterinfo[(turn_number%2)] == 0 | counterinfo[(turn_number%2)] == 4  | counterinfo[(turn_number%2)] == 10):
            counterinfo[(((turn_number+1)%2)+2)] = 0
            circle_y_pos_limits[(((turn_number+1)%2)+2)] = [int(10.5*rowheight),int((10.5*rowheight)-circleradi),int((10.5*rowheight)+circleradi)]
           
    ##START OUR GAME LOOP
    while True:
    ##HANDLE PEOPLE QUITING THE GAME
        for event in pygame.event.get():
            if event.type == pygame.QUIT: #Event handler for pygame
                return()
            ##FILL THE WINDOW BACKGROUND yellow   
        Screen.fill(colour["background"])
        for rownum in range (0,11): # iterates through the values for the rows this allows 
            drawcolums(rownum) 
        for counternum in range (0,4):
            drawcounter(counternum,counterinfo)
        pygame.display.flip()
        
        if counterinfo[turn_number%2]== 10 and counterinfo[turn_number%2+2] == 10:
            Screen.fill(colour["white"])
            txt.render_to(Screen,(boardWidth/2,boardHeight/2) ,"player " +str(turn_number%2+1)+ " wins", colour["black"])
            drawoptions(boardHeight/2,boardWidth/2,(450-int(450*2/10)),(60),"exit" ,boardHeight/2,boardWidth/2)
            
            while True:
                for event in pygame.event.get(): #Event handler for pygame
                    if event.type == "MOUSEDOWN":
                        break
                        return()
        choosecounter(diceroll(maxsides),turn_number)
        turn_number += 1
        pygame.event.wait()
        
        pygame.display.flip()



maxsides = 4
## I can't even
##names = inputnames(importnames ())
##mainScreen(int(input("""
##~~~~~MAIN Screen~~~~~
##1. Options
##2. Start the game
##3. Exit
##~~~~~~~~~~~~~~~~~~~
##""")))  #to be changed to buttons at a later date
## http://images2.wikia.nocookie.net/__cb20121218000738/saofanon/images/3/38/Tumblr_mct8fgNyYL1rixie3o1_500.gif

drawmain()

```
