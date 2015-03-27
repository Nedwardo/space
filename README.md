```python
import pygame # Imports my GUI maker module
import pygame.freetype # Imports my text to screen module
import random # Imports my random generater module
from pygame.locals import * # Import the module which alows me to refer to keyboard inputs by the button pressed and not a number

global names # Makes the names dictonary a global vairble
global colour # Makes the colour dictionary a global vairble
global event # Makes event

pygame.init() # Starts the pygame GUI handler
names = ["player 1","player 2"] # Defines the users names as player 1 and player 2
maxsides = 4 # Defines the dice to be a d4

colour = {} 
##SET A FEW RGB COLOURS
colour["black"] = pygame.Color(0,0,0)# Black
colour["yellow"] = pygame.Color(255,255,0) # Yellow
colour["cyan"] = pygame.Color(0,255,255) # Cyan
colour["magenta"] = pygame.Color(255,0,255) # Magenta
colour["red"] = pygame.Color(255,0,0) # Red
colour["green"] = pygame.Color(0,255,0) # Green
colour["blue"] = pygame.Color(0,0,255) # Blue
colour["white"] = pygame.Color(255,255,255)# White
colour["rust"] = pygame.Color(183, 65, 14)# Rust
colour["puce"] = pygame.Color(204, 136, 153)# Puce
colour["orange"] = pygame.Color(255,204,0) # Orange
colour["player1token"] = colour["rust"] # Defines the colour of player 1's tokens as rust
colour["player2token"] = colour["puce"] # Defines the colour of player 2's tokens as puce
colour["background"] = colour["yellow"] # Defines the in game background as yellow
colour["safe"] = colour["green"] # Defines the safe tile colour as green
colour["unsafe"] = colour["magenta"] # Defines the unsafe tile colour as magenta
colour["outline"] = colour["cyan"] # Defines the outline colour of the tiles as cyan
colour["gametext"] = colour["red"] # Defines the gametext colour as red

txt = pygame.freetype.Font("comic.ttf",15) # Sets the default text to be size 15 comic sans
turn = 0 # Sets the turn counter to zero

def Draw_Main () # Subroutine for drawing the main menu
    while True:
        global Screen
        Screen = pygame.display.set_mode((450,400)) # Sets the screen as 400 pixels by 450 pixles
        Screen.fill(colour["white"]) # Fills the screen white
        Draw_Options((int(450/10)),(50),(450-int(450*2/10)),(60),"Options",62,(int(450/10)+int((450-int(450*2/10))*20/45))) # Draws the Options button
        Draw_Options((int(450/10)),(150),(450-int(450*2/10)),(60),"Game",150+(60/5),int(450/10)+int(int(450-int(450*2/10))*7/15)) # Draws the start game button
        Draw_Options((int(450/10)),(250),(450-int(450*2/10)),(60),"Exit",250+(60/5),((int(450/10))+int((450-int(450*2/10))*7/15))) # Draws the exit button
        pygame.display.update() # Updates the screen
        Main_Choice(Choose_Options()) # Runs the main menu option handler with its input being from the menu input handler

def Draw_Options(xlocation,yheight,width,height,Text,Texth,Textx): # Subroutine for drawing Options 
    pygame.draw.rect(Screen,colour["black"],(xlocation-2,yheight-2,width+4,height+4)) # Draws the ouline for the box as 2 pixels around it in black
    pygame.draw.rect(Screen,colour["orange"],(xlocation,yheight,width,height)) # Draws the box in orange
    txt.render_to(Screen,(Textx,Texth) ,Text, colour["black"]) # Writes the text in the box
        
def Choose_Options(): # Subroutine for inputs handling in the menus
    while True: # Checks if the user has pressed the X button in the top right and If they have, exits the game
        event = pygame.event.poll()
        if event.type == "QUIT":
            pygame.quit()
            exit()
            
        if event.type == MOUSEBUTTONDOWN: # Checks if the user has pressed a mouse button
            if pygame.mouse.get_pos()[1] in range(50,110) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)): # Checks if the user has pressed the Options button           
                return(1) # Goes to the Options menu
            elif pygame.mouse.get_pos()[1] in range(150,210) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)): # Checks if the user has pressed the start game button
                return(2) # Starts the game
            elif pygame.mouse.get_pos()[1] in range(250,310) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)): # Checks if the user has pressed the exit /button
                return(3) # Exits the game
                
def Main_Choice (choice): # Subroutine for option handling in the main menu
    if choice == 1: # checks if the user clicked the Options button
        Options() # goes to the Options menu
    elif choice == 2: # checks if the user clicked the start game button
        Game() # LINK START-O  # Starts the game
    elif choice == 3: # checks if the user clicked the exit button
        pygame.quit() # exits the game
        exit() # exits the game

    
def Options(): # Subroutine for drawing the Options menu
    Display_Options() # displays the Options 
    Option_Handle((Choose_Options()-1)) # runs the option menu option handler with its input being from the menu input handler

def Display_Options(): # Subroutine for 
    Screen.fill(colour["white"]) # fills the screen white
    Draw_Options((int(450/10)),(50),(450-int(450*2/10)),(60),"Input names",62,(int(450/10)+139)) # draws an orange box with a black outline and Input names writen in the middle with black text
    Draw_Options((int(450/10)),(150),(450-int(450*2/10)),(60),"Change colours",162,int(450/10)+129) # draws an orange box with a black outline and Change colours writen in the middle with black text
    Draw_Options((int(450/10)),(250),(450-int(450*2/10)),(60),"Back",262,int(450/10)+166.5) # draws an orange box with a black outline and Back writen in the middle with black text
    pygame.display.flip() # updates the GUI
    
    
def Option_Handle(buttonpress): # Subroutine for 
    if buttonpress == 0:
        names = Handle_Names() # runs the name handling subroutine
    elif buttonpress == 1:
        Change_Colours_List() # runs the changinh colours handing subroutine
    else:
        return() # goes back to the previous menu
        

def Handle_Names(): # Subroutine for name handling
    playernames1 = "" # makes the player name blank
    playernames2 = "" # makes the player name blank
    Screen.fill(colour["white"]) # fills the screen white
    txt.render_to(Screen,(0,0),"Player 1 names: ", colour["black"])  # Writes on the screen "Player 1 names:" in alignment with the left margin in black
    txt.render_to(Screen,(0,50),"Player 2 names: ", colour["black"]) # Writes on the screen "Player 2 names:" in alignment with the left margin in black
    Draw_Options((int(450/10)),(250),(450-int(450*2/10)),(60),"Exit",262,int(450/10)+166.5) # Places an exit button in the bottom middle of the screen
    pygame.display.flip() # updates the GUI
    while True:
        event = pygame.event.poll() # Stores the previous pygame event (general keyboard/mouse input) as event
        endwhile = 0 # varible to break out of the while loops
        if event.type == "QUIT": #checks if the user has pressed the X button in the top right and If they have, exits the game
            pygame.quit()
            exit()
        if event.type == MOUSEBUTTONDOWN: # checks if the user has pressed their mouse button
            if pygame.mouse.get_pos()[1] in range (0,10) and pygame.mouse.get_pos()[0] in range (94,450): # checks if the player has pressed around the Player 1 names: option
                while endwhile == 0: # loops for as long as the user has not pressed enter
                    Screen.fill(colour["white"]) # fills the screen white
                    txt.render_to(Screen,(0,0),"Player 1 names: ", colour["orange"]) # sets the Player 1 names: text to be orange
                    txt.render_to(Screen,(0,50),"Player 2 names: ", colour["black"]) # Writes on the screen "Player 2 names:" in alignment with the left margin in black
                    txt.render_to(Screen,(220,3),str(playernames1), colour["black"]) # Writes player 1's name next to where it says "Player 1 names:"
                    txt.render_to(Screen,(220,53),str(playernames2), colour["black"]) # Writes player 2's name next to where it says "Player 2 names:"
                    Draw_Options(45,250,360,60,"Exit",262,211.5) # Places an exit button in the bottom middle of the screen
                    pygame.display.flip() # updates the GUI
                    endwhile,playernames1 = Input_Names(playernames1,300,14) # handler for keyboard inputs
            elif pygame.mouse.get_pos()[1] in range (50,60) and pygame.mouse.get_pos()[0] in range (94,450): # checks if the player has pressed around the Player 2 names: option
                while endwhile == 0:
                    Screen.fill(colour["white"])
                    txt.render_to(Screen,(0,0),"Player 1 names: ", colour["black"]) # Writes on the screen "Player 1 names:" in alignment with the left margin in black
                    txt.render_to(Screen,(0,50),"Player 2 names: ", colour["orange"]) # sets the Player 2 names: text to be orange
                    txt.render_to(Screen,(220,3),str(playernames1), colour["black"]) # Writes player 1's name next to where it says "Player 1 names:"
                    txt.render_to(Screen,(220,53),str(playernames2), colour["black"]) # Writes player 2's name next to where it says "Player 2 names:"
                    Draw_Options(45,250,360,60,"Exit",262,211.5) # Places an exit button in the bottom middle of the screen
                    pygame.display.flip() # updates the GUI
                    endwhile,playernames2 = Input_Names(playernames2,300,14) # handler for keyboard inputs
            elif pygame.mouse.get_pos()[1] in range(250,310) and pygame.mouse.get_pos()[0] in range(45,405): # checks if the player has pressed the exit button
                return(playernames1,playernames2)
            else:
                txt.render_to(Screen,(0,0),"Player 1 names: ", colour["black"])  # Writes on the screen "Player 1 names:" in alignment with the left margin in black
                txt.render_to(Screen,(0,50),"Player 2 names: ", colour["black"]) # Writes on the screen "Player 2 names:" in alignment with the left margin in black
                txt.render_to(Screen,(220,3),str(playernames1), colour["black"]) # Writes player 1's name next to where it says "Player 1 names:"
                txt.render_to(Screen,(220,53),str(playernames2), colour["black"]) # Writes player 2's name next to where it says "Player 2 names:"
                Draw_Options((int(450/10)),(250),(450-int(450*2/10)),(60),"Exit",262,int(450/10)+166.5) # Places an exit button in the bottom middle of the screen
                pygame.display.flip() # Updates the GUI
                
def Input_Names(value,keylimitupper,keylimitlower): # Subroutine for keyboard inputs
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

def Change_Colours_List(): # Subroutine for 
    Screen.fill(colour["white"])
    Draw_Options(45,24,360,24,"Change " +str(names[0]) +" token colour",27,127)
    Draw_Options(45,71,360,24,"Change " +str(names[1]) +" token colour",74,125)
    Draw_Options(45,118,360,24,"Change Background colour",121,129)
    Draw_Options(45,165,360,24,"Change Safe Tile colour",168,140)
    Draw_Options(45,212,360,24,"Change Unsafe Tile colour",215,130)
    Draw_Options(45,259,360,24,"Change Outline colour",262,144.5)
    Draw_Options(45,306,360,24,"Change Gametext colour",309,136)
    Draw_Options(45,353,360,24, "Back",355,212)
    pygame.display.flip() # Updates the GUI
    while True:
        event = pygame.event.poll()
        if event.type == "QUIT":
            pygame.quit()
            exit()
        if event.type == MOUSEBUTTONDOWN:
            if pygame.mouse.get_pos()[1] in range(24,47) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)):            
                colour["player1token"] = Option_Colour()
            elif pygame.mouse.get_pos()[1] in range(71,94) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)):
                colour["player2token"] = Option_Colour()
            elif pygame.mouse.get_pos()[1] in range(118,141) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)):
                colour["background"] = Option_Colour()
            elif pygame.mouse.get_pos()[1] in range(165,188) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)):
                colour["safe"] = Option_Colour()
            elif pygame.mouse.get_pos()[1] in range(212,235) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)):
                colour["unsafe"] = Option_Colour()
            elif pygame.mouse.get_pos()[1] in range(259,282) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)):
                colour["outline"] = Option_Colour()
            elif pygame.mouse.get_pos()[1] in range(306,329) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)):
                colour["gametext"] = Option_Colour()
            elif pygame.mouse.get_pos()[1] in range(353,376) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)):
                return()

def Option_Colour(): # Subroutine for 
    R = ""
    G = ""
    B = ""
    End = 0
    Screen.fill(colour["white"])
    txt.render_to(Screen,(100,0),"Please input the RGB values of the colour", colour["black"])
    txt.render_to(Screen,(0,50),"R:", colour["black"])
    txt.render_to(Screen,(0,100),"G:", colour["black"])
    txt.render_to(Screen,(0,150),"B:", colour["black"])
    while True:
            event = pygame.event.poll()
            pygame.display.flip() # Updates the GUI
            endwhile = 0
            if event.type == "QUIT":
                pygame.quit()
                exit()
            if event.type == MOUSEBUTTONDOWN:
                if pygame.mouse.get_pos()[1] in range (50,60) and pygame.mouse.get_pos()[0] in range (0,450):
                    while End == 0:
                        print("ayy lmao")
                        Screen.fill(colour["white"])
                        txt.render_to(Screen,(100,0),"Please input the RGB values of the colour", colour["black"])
                        txt.render_to(Screen,(0,50),"R:", colour["orange"])
                        txt.render_to(Screen,(0,100),"G:", colour["black"])
                        txt.render_to(Screen,(0,150),"B:", colour["black"])
                        txt.render_to(Screen,(220,53),str(R), colour["black"])
                        txt.render_to(Screen,(220,103),str(G), colour["black"])
                        txt.render_to(Screen,(220,153),str(B), colour["black"])
                        Draw_Options(45,250,360,60,"Input Values",262,211.5)
                        pygame.display.flip() # Updates the GUI
                        End,R = Input_Names(R,57,48)
                elif pygame.mouse.get_pos()[1] in range (100,110) and pygame.mouse.get_pos()[0] in range (0,450):
                    while End == 0:
                        Screen.fill(colour["white"])
                        txt.render_to(Screen,(100,0),"Please input the RGB values of the colour", colour["black"])
                        txt.render_to(Screen,(0,50),"R:", colour["black"])
                        txt.render_to(Screen,(0,100),"G:", colour["orange"])
                        txt.render_to(Screen,(0,150),"B:", colour["black"])
                        txt.render_to(Screen,(220,53),str(R), colour["black"])
                        txt.render_to(Screen,(220,103),str(G), colour["black"])
                        txt.render_to(Screen,(220,153),str(B), colour["black"])
                        Draw_Options(45,250,360,60,"Input Values",262,211.5)
                        pygame.display.flip() # Updates the GUI
                        End,G = Input_Names(G,57,48)
                elif pygame.mouse.get_pos()[1] in range (150,160) and pygame.mouse.get_pos()[0] in range (0,450):
                    while endwhile == 0:
                        Screen.fill(colour["white"])
                        txt.render_to(Screen,(100,0),"Please input the RGB values of the colour", colour["black"])
                        txt.render_to(Screen,(0,50),"R:", colour["black"])
                        txt.render_to(Screen,(0,100),"G:", colour["black"])
                        txt.render_to(Screen,(0,150),"B:", colour["orange"])
                        txt.render_to(Screen,(220,53),str(R), colour["black"])
                        txt.render_to(Screen,(220,103),str(G), colour["black"])
                        txt.render_to(Screen,(220,153),str(B), colour["black"])
                        Draw_Options(45,250,360,60,"Input Values",262,211.5)
                        pygame.display.flip() # Updates the GUI
                        End,B = Input_Names(B,57,48)
                elif pygame.mouse.get_pos()[1] in range(250,310) and pygame.mouse.get_pos()[0] in range(0,405):
                    return(pygame.Color(int(R),int(G),int(B)))
                if event.type == "QUIT":
                    pygame.quit()
                    exit()
#        Input_Names(playernames,57,48):

###########GAME##########################
def Game(): # Subroutine for 
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
    def Define_Circle_x_Pos_Limits(infocolumwidth,lcountup): # Subroutine for 
        if lcountup%2 == 0:
            temp_store =[(infocolumwidth+int(((lcountup+2)/2)*80)),((infocolumwidth+int(((lcountup+2)/2)*80))-circleradi),((infocolumwidth+int(((lcountup+2)/2)*80))+circleradi)]
        else:
            temp_store =[(infocolumwidth+int(((lcountup+5)/2)*80)),((infocolumwidth+int(((lcountup+5)/2)*80))-circleradi),((infocolumwidth+int(((lcountup+5)/2)*80))+circleradi)]
        return temp_store
    circle_x_pos_limits = [Define_Circle_x_Pos_Limits(infocolumwidth,iterate) for iterate in range (0,4)]

        
    def Draw_Colums(rownumber): # Subroutine for this drawing the columns in the game
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

    def Dice_Roll(sides): # Subroutine for 
        Dice_Roll = random.randrange(0,sides)
        if Dice_Roll ==  0:
            print("you can move one of your pieces up one")
        elif Dice_Roll == 1:
            print("you can move one of your pieces up two")
        elif Dice_Roll == 2:
            print("you can move one of your pieces up three")
        elif Dice_Roll == 3:
            print("you can move one of your pieces back one")
        else:
            print("you can move one of pieces to the next empty space")
        return Dice_Roll
        

    def Draw_Counter(counternumber,counterlist): # Subroutine for drawing the counters onto the board
        if counternumber%2 == 0:
            pygame.draw.circle(Screen,colour["player1token"],(int(circle_x_pos_limits[counternumber][0]),int(circle_y_pos_limits[counternumber][0])),circleradi)
        else:
            pygame.draw.circle(Screen,colour["player2token"],(int(circle_x_pos_limits[counternumber][0]),int(circle_y_pos_limits[counternumber][0])),circleradi)


    def Press_Counter(roll,turnno): # Subroutine for 
        print("please select the counter you wish to move")
        while True:
            event = pygame.event.poll()
            if event.type == MOUSEBUTTONDOWN:
                if pygame.mouse.get_pos()[1] in range(int(circle_y_pos_limits[turnno%2][1]),int(circle_y_pos_limits[turnno%2][2])) and pygame.mouse.get_pos()[0] in range(circle_x_pos_limits[turnno%2][1],circle_x_pos_limits[turnno%2][2]):            
                    return(turnno%2)
                elif pygame.mouse.get_pos()[1] in range(int(circle_y_pos_limits[turnno%2+2][1]),int(circle_y_pos_limits[turnno%2+2][2])) and pygame.mouse.get_pos()[0] in range(circle_x_pos_limits[turnno%2+2][1],circle_x_pos_limits[turnno%2+2][2]):
                    return((turnno%2)+2)
            if event.type == "QUIT":
                Draw_Main()

    def Move_Counter(dice_roll,counter_number,turn_count): # Subroutine for 
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
        Move_Back(turn_number)
                
    def Choose_Counter(dice,turn): # Subroutine for 
        validmoves = []
        validmoves =(Vaild_Move(dice,turn))

        if validmoves == [True,True]:
            Move_Counter(dice,Press_Counter(dice,turn),turn)

        elif validmoves == [True,False]:
            Move_Counter(dice,turn%2,turn)

        elif validmoves == [False,True]:                         
            Move_Counter(dice,turn%2+2,turn)
        else:
            print("no valid moves")

    def Vaild_Move(dice_roll,turn_number): # Subroutine for 
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
    
    def Move_Back (turn_number): # Subroutine for 
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
        for event in pygame.event.get(): # Checks if the user has pressed the X button and if so exits the game
            if event.type == pygame.QUIT:
                return()
            ##FILL THE WINDOW BACKGROUND yellow   
        Screen.fill(colour["background"])
        for rownum in range (0,11): # Iterates through the values for the rows this allows 
            Draw_Colums(rownum) 
        for counternum in range (0,4):
            Draw_Counter(counternum,counterinfo)
        pygame.display.flip()
        
        if counterinfo[turn_number%2]== 10 and counterinfo[turn_number%2+2] == 10:
            Screen.fill(colour["white"])
            txt.render_to(Screen,(boardWidth/2,boardHeight/2) ,"player " +str(turn_number%2+1)+ " wins", colour["black"])
            Draw_Options(boardHeight/2,boardWidth/2,(450-int(450*2/10)),(60),"exit" +str(turn_number%2+1)+ " wins",boardWidth/2,boardHeight/2)
            
            while True:
                for event in pygame.event.get(): # Checks if the user has pressed a mouse button and if so exits the game
                    if event.type == "MOUSEDOWN":
                        break
                        return()
        Choose_Counter(Dice_Roll(maxsides),turn_number)
        turn_number += 1
        pygame.event.wait()
        
        pygame.display.flip()

Draw_Main()


```
