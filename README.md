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

def Draw_Main (): # Subroutine for drawing the main menu
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
    if choice == 1: # Checks if the user clicked the Options button
        Display_Options() # Goes to the Options menu
    elif choice == 2: # Checks if the user clicked the start game button
        Game() # LINK START-O  # Starts the game
    elif choice == 3: # Checks if the user clicked the exit button
        pygame.quit() # Exits the game
        exit() # Exits the game

def Display_Options(): # Subroutine for displaying the options menu
    Screen.fill(colour["white"]) # fills the screen white
    Draw_Options((int(450/10)),(50),(450-int(450*2/10)),(60),"Input names",62,(int(450/10)+139)) # Draws an orange box with a black outline and Input names writen in the middle with black text
    Draw_Options((int(450/10)),(150),(450-int(450*2/10)),(60),"Change colours",162,int(450/10)+129) # Draws an orange box with a black outline and Change colours writen in the middle with black text
    Draw_Options((int(450/10)),(250),(450-int(450*2/10)),(60),"Back",262,int(450/10)+166.5) # Draws an orange box with a black outline and Back writen in the middle with black text
    pygame.display.flip() # Updates the GUI
    Option_Handle((Choose_Options()-1)) # Runs the option menu option handler with its input being from the menu input handler
    
    
def Option_Handle(buttonpress): # Subroutine for handling the button Inputs
    if buttonpress == 0: # Checks if the user clicked the names button
        names = Handle_Names() # Runs the name handling subroutine
    elif buttonpress == 1: # Checks if the user clicked the change colours button
        Change_Colours_List() # Runs the changing colours handing subroutine
    else: # Checks if the user clicked the back button
        return() # Goes back to the previous menu
        

def Handle_Names(): # Subroutine for name handling
    playernames1 = "" # makes the player name blank
    playernames2 = "" # makes the player name blank
    Screen.fill(colour["white"]) # fills the screen white
    txt.render_to(Screen,(0,0),"Player 1 names: ", colour["black"])  # Writes on the screen "Player 1 names:" in alignment with the left margin in black
    txt.render_to(Screen,(0,50),"Player 2 names: ", colour["black"]) # Writes on the screen "Player 2 names:" in alignment with the left margin in black
    Draw_Options((int(450/10)),(250),(450-int(450*2/10)),(60),"Exit",262,int(450/10)+166.5) # Places an exit button in the bottom middle of the screen
    pygame.display.flip() # Updates the GUI
    while True:
        event = pygame.event.poll() # Stores the previous pygame event (general keyboard/mouse input) as event
        endwhile = 0 # Varible to break out of the while loops
        if event.type == "QUIT": # Checks if the user has pressed the X button in the top right and If they have, exits the game
            pygame.quit()
            exit()
        if event.type == MOUSEBUTTONDOWN: # Checks if the user has pressed their mouse button
            if pygame.mouse.get_pos()[1] in range (0,10) and pygame.mouse.get_pos()[0] in range (94,450): # Checks if the player has pressed around the Player 1 names: option
                while endwhile == 0: # Loops for as long as the user has not pressed enter
                    Screen.fill(colour["white"]) # fills the screen white
                    txt.render_to(Screen,(0,0),"Player 1 names: ", colour["orange"]) # Sets the Player 1 names: text to be orange
                    txt.render_to(Screen,(0,50),"Player 2 names: ", colour["black"]) # Writes on the screen "Player 2 names:" in alignment with the left margin in black
                    txt.render_to(Screen,(220,3),str(playernames1), colour["black"]) # Writes player 1's name next to where it says "Player 1 names:"
                    txt.render_to(Screen,(220,53),str(playernames2), colour["black"]) # Writes player 2's name next to where it says "Player 2 names:"
                    Draw_Options(45,250,360,60,"Exit",262,211.5) # Places an exit button in the bottom middle of the screen
                    pygame.display.flip() # Updates the GUI
                    endwhile,playernames1 = Input_Names(playernames1,300,14,str) # handler for keyboard inputs
            elif pygame.mouse.get_pos()[1] in range (50,60) and pygame.mouse.get_pos()[0] in range (94,450): # Checks if the player has pressed around the Player 2 names: option
                while endwhile == 0:
                    Screen.fill(colour["white"])
                    txt.render_to(Screen,(0,0),"Player 1 names: ", colour["black"]) # Writes on the screen "Player 1 names:" in alignment with the left margin in black
                    txt.render_to(Screen,(0,50),"Player 2 names: ", colour["orange"]) # Sets the Player 2 names: text to be orange
                    txt.render_to(Screen,(220,3),str(playernames1), colour["black"]) # Writes player 1's name next to where it says "Player 1 names:"
                    txt.render_to(Screen,(220,53),str(playernames2), colour["black"]) # Writes player 2's name next to where it says "Player 2 names:"
                    Draw_Options(45,250,360,60,"Exit",262,211.5) # Places an exit button in the bottom middle of the screen
                    pygame.display.flip() # Updates the GUI
                    endwhile,playernames2 = Input_Names(playernames2,300,14,str) # handler for keyboard inputs
            elif pygame.mouse.get_pos()[1] in range(250,310) and pygame.mouse.get_pos()[0] in range(45,405): # Checks if the player has pressed the exit button
                return(playernames1,playernames2)
            else:
                txt.render_to(Screen,(0,0),"Player 1 names: ", colour["black"])  # Writes on the screen "Player 1 names:" in alignment with the left margin in black
                txt.render_to(Screen,(0,50),"Player 2 names: ", colour["black"]) # Writes on the screen "Player 2 names:" in alignment with the left margin in black
                txt.render_to(Screen,(220,3),str(playernames1), colour["black"]) # Writes player 1's name next to where it says "Player 1 names:"
                txt.render_to(Screen,(220,53),str(playernames2), colour["black"]) # Writes player 2's name next to where it says "Player 2 names:"
                Draw_Options((int(450/10)),(250),(450-int(450*2/10)),(60),"Exit",262,int(450/10)+166.5) # Places an exit button in the bottom middle of the screen
                pygame.display.flip() # Updates the GUI
                
def Input_Names(value,keylimitupper,keylimitlower,Type): # Subroutine for keyboard inputs
    stop = 0 # Ends the charater inputing loop
    event = pygame.event.poll() # Checks if the user pressed the X button and if so exits the game
    if event.type == "QUIT":
        pygame.quit()
        exit()
    if event.type == KEYDOWN and event.key < keylimitupper and event.key > keylimitlower: # Checks if the user has pressed a key which is allowed in this context
        letter = event.unicode # Defines letter as the most recently keyboard Unicode charater  
        if len(value) < MaxChar: # Checks if the word the user has entered is more than 10 charaters
                if Type == int and (int(value*10) + int(letter) < 255): # Checks if the number the user has entered is less than 365         
                    value += letter # Adds a charater to the already inputed word
                elif Type == str and len(value) < 10: # Checks if the word the user has entered is more than 10 charaters 
                    value += letter # Adds a charater to the already inputed word
    elif event.type == KEYDOWN and event.key == 8 and value != "": # Checks if the user has pressed backspace and if the string is not blank
        value = value[:-1]# This removes the last charater from the string
    elif event.type == KEYDOWN and event.key == 13: # Checks if the user has pressed enter
        stop = 1 # Stops the inputing charater loop
    return stop,value

def Change_Colours_List(): # Subroutine for the menu from which the user chooses which colour they wish to change
    Screen.fill(colour["white"]) # Fills the screen white
    Draw_Options(45,24,360,24,"Change " +str(names[0]) +" token colour",27,127) # Draws a button for the change player 1's token colour option
    Draw_Options(45,71,360,24,"Change " +str(names[1]) +" token colour",74,125) # Draws a button for the change player 2's token colour option
    Draw_Options(45,118,360,24,"Change Background colour",121,129) # Draws a button for the change Background colour option
    Draw_Options(45,165,360,24,"Change Safe Tile colour",168,140) # Draws a button for the change Safe Tile colour option
    Draw_Options(45,212,360,24,"Change Unsafe Tile colour",215,130) # Draws a button for the change Unsafe Tile  colour option
    Draw_Options(45,259,360,24,"Change Outline colour",262,144.5) # Draws a button for the change Outline colour option
    Draw_Options(45,306,360,24,"Change Gametext colour",309,136) # Draws a button for the change Gametext colour option
    Draw_Options(45,353,360,24, "Back",355,212) # Draws a button for the back button
    pygame.display.flip() # Updates the GUI
    while True:
        event = pygame.event.poll() # Checks if the user pressed the X button and if so exits the game
        if event.type == "QUIT":
            pygame.quit()
            exit()
        if event.type == MOUSEBUTTONDOWN: # Checks if the user has pressed their mouse button
            if pygame.mouse.get_pos()[1] in range(24,47) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)): # Checks if the user has pressed the change player 1's token colour option button          
                colour["player1token"] = Option_Colour() # Goes to the respective menu
            elif pygame.mouse.get_pos()[1] in range(71,94) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)): # Checks if the user has pressed the change  change player 2's token colour option button  
                colour["player2token"] = Option_Colour() # Goes to the respective menu
            elif pygame.mouse.get_pos()[1] in range(118,141) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)): # Checks if the user has pressed the change Background colour option button  
                colour["background"] = Option_Colour() # Goes to the respective menu
            elif pygame.mouse.get_pos()[1] in range(165,188) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)): # Checks if the user has pressed the change Safe Tile colour option button  
                colour["safe"] = Option_Colour() # Goes to the respective menu
            elif pygame.mouse.get_pos()[1] in range(212,235) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)): # Checks if the user has pressed the change Unsafe Tile colour option button  
                colour["unsafe"] = Option_Colour() # Goes to the respective menu
            elif pygame.mouse.get_pos()[1] in range(259,282) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)): # Checks if the user has pressed the change change Outline colour option option button  
                colour["outline"] = Option_Colour() # Goes to the respective menu
            elif pygame.mouse.get_pos()[1] in range(306,329) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)): # Checks if the user has pressed the change change Gametext colour button  
                colour["gametext"] = Option_Colour() # Goes to the respective menu
            elif pygame.mouse.get_pos()[1] in range(353,376) and pygame.mouse.get_pos()[0] in range(45,45+450-int(450*2/10)): # Checks if the user has pressed the back button 
                return() # Goes to the respective menu

def Option_Colour(): # Subroutine for changing the customisable colour
    R = "" # Defines the input for red (RGB colour sytem)
    G = "" # Defines the input for Green (RGB colour sytem)
    B = "" # Defines the input for Blue (RGB colour sytem)
    Draw_Colour_Options (0,R,G,B) # Draws the menu onto the screen
    while True:
            event = pygame.event.poll() # checks if the user has inputed anything
            if event.type == "QUIT": # Checks if the user pressed the X button and if so exits the game
                pygame.quit()
                exit()
            if event.type == MOUSEBUTTONDOWN: # Checks if the user has pressed their mouse button
                if pygame.mouse.get_pos()[1] in range (50,60) and pygame.mouse.get_pos()[0] in range (0,450): # Checks if the user has clicked next to R:
                    while End == 0: # Checks if the user has pressed enter and if so breaks out of the while loop
                        Draw_Colour_Options (1,R,G,B) # Draws the menu onto the screen
                        End,R = Input_Names(R,57,48,int) # Only allows the user to input numbers into the menu and checks if the user has pressed enter
                elif pygame.mouse.get_pos()[1] in range (100,110) and pygame.mouse.get_pos()[0] in range (0,450): # Checks if the user has clicked next to G:
                    while End == 0: # Checks if the user has pressed enter and if so breaks out of the while loop
                        Draw_Colour_Options (2,R,G,B) # Draws the menu onto the screen
                        End,G = Input_Names(G,57,48,int) # Only allows the user to input numbers into the menu and checks if the user has pressed enter
                elif pygame.mouse.get_pos()[1] in range (150,160) and pygame.mouse.get_pos()[0] in range (0,450):
                    while End == 0: # Checks if the user has pressed enter and if so breaks out of the while loop
                        Draw_Colour_Options (3,R,G,B) # Draws the menu onto the screen
                        End,B = Input_Names(B,57,48,3,int) # Only allows the user to input numbers into the menu and checks if the user has pressed enter
                elif pygame.mouse.get_pos()[1] in range(250,310) and pygame.mouse.get_pos()[0] in range(0,405): # Checks if the user has clicked to go back
                    return(pygame.Color(int(R),int(G),int(B))) # Returns the RGB values of the colour as a pygame colour
                else:
                    Draw_Colour_Options (0,R,G,B) # Draws the menu onto the screen
                    End = 0 # Defines the varible that ends the while loop
                    
def Draw_Colour_Options (Colour_Int,R,G,B): # Subroutine for frawing the colour input menu
    Screen.fill(colour["white"]) # Fills the screen white
    txt.render_to(Screen,(100,0),"Please input the RGB values of the colour", colour["black"]) # Writes on to the screen "Please input the RGB values of the colour" center aligned in black
    if Colour_Int == 0: # Checks if the screen is to be updated as normal
        txt.render_to(Screen,(0,50),"R:", colour["black"]) # Writes on to the screen "R:" this is where the user will input the red value of the colour aligned left, underneath the above text in black
        txt.render_to(Screen,(0,100),"G:", colour["black"]) # Writes on to the screen "G:" this is where the user will input the green value of the colour aligned left, underneath the above text in black
        txt.render_to(Screen,(0,150),"B:", colour["black"]) # Writes on to the screen "B:" this is where the user will input the blue value of the colour aligned left, underneath the above text in black
    elif Colour_Int == 1: # Checks if the user is inputting the values for the Red code of the RGB value
        txt.render_to(Screen,(0,50),"R:", colour["orange"]) # Writes on to the screen "R:" this is where the user will input the red value of the colour aligned left, underneath the above text in orange
        txt.render_to(Screen,(0,100),"G:", colour["black"]) # Writes on to the screen "G:" this is where the user will input the green value of the colour aligned left, underneath the above text in black
        txt.render_to(Screen,(0,150),"B:", colour["black"]) # Writes on to the screen "B:" this is where the user will input the blue value of the colour aligned left, underneath the above text in black
    elif Colour_Int == 2: # Checks if the user is inputting the values for the Green code of the RGB value
        txt.render_to(Screen,(0,50),"R:", colour["black"]) # Writes on to the screen "R:" this is where the user will input the red value of the colour aligned left, underneath the above text in black
        txt.render_to(Screen,(0,100),"G:", colour["orange"]) # Writes on to the screen "G:" this is where the user will input the green value of the colour aligned left, underneath the above text in orange
        txt.render_to(Screen,(0,150),"B:", colour["black"]) # Writes on to the screen "B:" this is where the user will input the blue value of the colour aligned left, underneath the above text in black
    else: # Checks if the user is inputting the values for the Blue code of the RGB value
        txt.render_to(Screen,(0,50),"R:", colour["black"]) # Writes on to the screen "R:" this is where the user will input the red value of the colour aligned left, underneath the above text in black
        txt.render_to(Screen,(0,100),"G:", colour["black"]) # Writes on to the screen "G:" this is where the user will input the green value of the colour aligned left, underneath the above text in black
        txt.render_to(Screen,(0,150),"B:", colour["orange"]) # Writes on to the screen "B:" this is where the user will input the blue value of the colour aligned left, underneath the above text in orange 
    txt.render_to(Screen,(220,53),str(R), colour["black"]) # Writes on to the screen the inputted red value next to R: in black
    txt.render_to(Screen,(220,103),str(G), colour["black"]) # Writes on to the screen the inputted red value next to G: in black
    txt.render_to(Screen,(220,153),str(B), colour["black"]) # Writes on to the screen the inputted red value next to B: in black
    Draw_Options(45,250,360,60,"Input Values",262,211.5) # Draws the Input values option on to the screen
    pygame.display.flip() # Updates the GUI

###########GAME##########################
def Game(): # Subroutine for running the game
    pygame.init() #Start up pygame
    global counterinfo
    counterinfo = [0,0,0,0] # Stores the postions of the counters on the board as a global varible
    turn_number = 1 # Sets the turn counter to 1
    

    ##LETS DEFINE SOME SIZES
    boardWidth = 1000 # Sets the board to be 1000 pixels wide
    boardHeight = 550 # Sets the board to be 550 pixels high
    rowheight = 50 # sets the rows to be 50 pixels high
    tokencolumwidth = 500 # Sets the token coloum to be 500 pixels wide
    infocolumwidth = 100 # Sets the info coloum to be 100 pixels wide
    circleradi = 15 # Sets the radius of the circle to be 15 pixels 
    circle_x_pos_limits = [] # Defines the array which stores the postion of the counters in the x dimension
    circle_y_pos_limits = [] # Defines the array which stores the postion of the counters in the y dimension
    for countup in range (0,4): # Beacuse the y values of the counters are all the same at the start this iterates between 0 and 4 and add the same thing to a list each time   
        circle_y_pos_limits += [[int(10.5*rowheight),int((10.5*rowheight)-circleradi),int((10.5*rowheight)+circleradi)]] # Defines the y co-ordiantes of the counters
    circle_x_pos_limits = [Define_Circle_x_Pos_Limits(infocolumwidth,iterate) for iterate in range (0,4)] # Defines the x co-ordiantes of the counters
    ##GIVE THE WINDOW A names
    Screen = pygame.display.set_mode((boardWidth,boardHeight)) # Draws a screen 1000 x 450 pixels
    
def Define_Circle_x_Pos_Limits(infocolumwidth,lcountup): # Subroutine for defining the x co-ordiantes of the counters
    if lcountup%2 == 0: # As my counters are stored as [player2's first counter,player1's first counter,player2's second counter,player1's second counter] it checks whose counter it is defingin the postions of 
        temp_store =[(infocolumwidth+int(((lcountup+2)/2)*80)),((infocolumwidth+int(((lcountup+2)/2)*80))-circleradi),((infocolumwidth+int(((lcountup+2)/2)*80))+circleradi)] # Defines the x co-ordiantes of the respective counters
    else: # As my counters are stored as [player2's first counter,player1's first counter,player2's second counter,player1's second counter] it checks whose counter it is defingin the postions of 
        temp_store =[(infocolumwidth+int(((lcountup+5)/2)*80)),((infocolumwidth+int(((lcountup+5)/2)*80))-circleradi),((infocolumwidth+int(((lcountup+5)/2)*80))+circleradi)] # Defines the x co-ordiantes of the respective counters
    return temp_store
    

    
def Draw_Colums(rownumber): # Subroutine for this drawing the columns in the game
    row = 525 - 50 * rownumber # Sets the top left co-ordiante of the box
    if rownumber == 10: # Checks if the box is the top one
        txt.render_to(Screen,(10,row) ,str(rownumber+1)+ " - FINISH", colour["gametext"]) # If the box is the top one it writes 11-FINISH in the info coloum
    elif rownumber == 0: # Checks if the box is the bottom one
        txt.render_to(Screen,(10,row) ,str(rownumber+1) + " - START", colour["gametext"]) # If the box is the bottom one it writes 1-START in the info coloum
    else: # Checks if the box is neither the top nor the bottom one 
        txt.render_to(Screen,(10,row) ,str(rownumber+1), colour["gametext"]) # If the box isn't the top or the bottom one it writes the number of it in the info coloum
    pygame.draw.rect(Screen,colour["outline"],(0,(10-rownumber)*rowheight,infocolumwidth,rowheight),5) # Draws the outline of the boxes in the designated colour
    if rownumber == 0 or rownumber == 4 or rownumber == 10: # Checks if the tile is a safe one
        pygame.draw.rect(Screen,colour["safe"],(infocolumwidth,(10-rownumber)*rowheight,tokencolumwidth,rowheight)) # Colours it appropiratly 
    else: # Checks if the tile is an unsafe one
        pygame.draw.rect(Screen,colour["unsafe"],(infocolumwidth,(10-rownumber)*rowheight,tokencolumwidth,rowheight)) # Colours it appropiratly 
    pygame.draw.rect(Screen,colour["outline"],(infocolumwidth,(10-rownumber)*rowheight,tokencolumwidth,rowheight),5) # Draws the outline of the boxes in the designated colour

def Dice_Roll(sides): # Subroutine for the dice rolls
    Dice_Roll = random.randrange(0,sides) # Rolls either a d4 or d5 based on the previous input of the user
    if Dice_Roll ==  0: # Checks if it rolled a one
        print("you can move one of your pieces up one") # Displays an apporpirate message
    elif Dice_Roll == 1: # Checks if it rolled a two
        print("you can move one of your pieces up two") # Displays an apporpirate message
    elif Dice_Roll == 2: # Checks if it rolled a three
        print("you can move one of your pieces up three") # Displays an apporpirate message
    elif Dice_Roll == 3: # Checks if it rolled a four
        print("you can move one of your pieces back one") # Displays an apporpirate message
    else: # Checks if it rolled a five
        print("you can move one of pieces to the next empty space") # Displays an apporpirate message
    return Dice_Roll
    

def Draw_Counter(counternumber,counterlist): # Subroutine for drawing the counters onto the board
    if counternumber%2 == 0:
        pygame.draw.circle(Screen,colour["player1token"],(int(circle_x_pos_limits[counternumber][0]),int(circle_y_pos_limits[counternumber][0])),circleradi)
    else:
        pygame.draw.circle(Screen,colour["player2token"],(int(circle_x_pos_limits[counternumber][0]),int(circle_y_pos_limits[counternumber][0])),circleradi)


def Press_Counter(roll,turnno): # Subroutine for pressing the counter
    print("please select the counter you wish to move") # Asks the user to click on the counter they wish to move
    while True:
        event = pygame.event.poll() # Defines event as the most recent pygame event
        if event.type == MOUSEBUTTONDOWN: # Checks if the user pressed his mouse button
            if pygame.mouse.get_pos()[1] in range(int(circle_y_pos_limits[turnno%2][1]),int(circle_y_pos_limits[turnno%2][2])) and pygame.mouse.get_pos()[0] in range(circle_x_pos_limits[turnno%2][1],circle_x_pos_limits[turnno%2][2]): # Checks if the user pressed his/her first counter           
                return(turnno%2) # Returns the number of the players first counter
            elif pygame.mouse.get_pos()[1] in range(int(circle_y_pos_limits[turnno%2+2][1]),int(circle_y_pos_limits[turnno%2+2][2])) and pygame.mouse.get_pos()[0] in range(circle_x_pos_limits[turnno%2+2][1],circle_x_pos_limits[turnno%2+2][2]): # Checks if the user pressed his/her second counter 
                return((turnno%2)+2) # Returns the number of the players second counter
        if event.type == "QUIT": # If the user presses the X button it goes back to the previous menu
            Draw_Main()

def Move_Counter(dice_roll,counter_number,turn_count): # Subroutine for updating the definitions of the counters' postions
    if dice_roll < 3 :
        counterinfo[counter_number] += dice_roll+1 # Sets the counter on next up tile
        circle_y_pos_limits[counter_number][0] -= (dice_roll+1)*rowheight # Sets the mid point of the token
        circle_y_pos_limits[counter_number][1] -= (dice_roll+1)*rowheight # Sets the top point point of the token
        circle_y_pos_limits[counter_number][2] -= (dice_roll+1)*rowheight # Sets the bottom point of the token
    elif dice_roll == 3:
        counterinfo[counter_number] -= 1 # Sets the counter on pior tile
        circle_y_pos_limits[counter_number][0] += rowheight # Sets the mid point of the token
        circle_y_pos_limits[counter_number][1] += rowheight # Sets the top point point of the token
        circle_y_pos_limits[counter_number][2] += rowheight # Sets the bottom point of the token
    Move_Back(turn_number) # Checks if any counters can be moved back and if so acts accordingly 
            
def Choose_Counter(dice,turn): # Subroutine for acting on which counters can be moved
    validmoves = [] # Defines the list that will store which moves are vaild
    validmoves = (Vaild_Move(dice,turn)) # Checks which moves are vaild

    if validmoves == [True,True]: # Checks if both of the users counters have vaild moves
        Move_Counter(dice,Press_Counter(dice,turn),turn) # Allows the user to choose which counter they wish to move

    elif validmoves == [True,False]: # Checks if only the users first counter has a vaild move 
        Move_Counter(dice,turn%2,turn) # Moves the respective counter

    elif validmoves == [False,True]: # Checks if only the users second counter has a vaild move                         
        Move_Counter(dice,turn%2+2,turn) # Moves the respective counter
    else: # Checks if the user cannot make vaild moves
        print("no valid moves") # Tells the user that there are no moves that he can make

def Vaild_Move(dice_roll,turn_number): # Subroutine for checking which counters movement is valid
    counters = [counterinfo[(turn_number%2)],counterinfo[(turn_number%2+2)]] # Defines counters as a list containing the current players counters
    possible_moves = [False,False] # Defines the possible moves as both false
    if dice_roll < 3: # If the dice roll would allow them to move forward
        for counter_countup in range(0,2): # Iterates through both of the users counters
            if counters[counter_countup] != counters[1-counter_countup]-(dice_roll+1): # Checks if the users counter is not in front of the place where the counter would move to
                possible_moves[counter_countup] = True # If the above is true then it means the movement is a possiblity    
            elif counters[1-counter_countup] == 4 or counters[1-counter_countup] == 10: # Checks if the other counter is on a safe tile
                possible_moves[counter_countup] = True # If the above is true then it means the movement is a possiblity  
            if counters[counter_countup] == 10: # Checks if the movement would put the counter past the final tile
                possible_moves[counter_countup] = False # If the above is true then it means the movement is not a possiblity  

    elif dice_roll == 3: # Checks if the dice roll is for a backwards movement
        for counter_countup in range(0,2): # Iterates through both of the users counters
            if counters[counter_countup] != counters[1-counter_countup]+1:  # Checks if the users counter is not in front of the place where the counter would move to
                possible_moves[counter_countup] = True # If the above is true then it means the movement is a possiblity  
            if counters[1-counter_countup] == 4 or counters[1-counter_countup] == 0: # Checks if the other counter is on a safe tile
                possible_moves[counter_countup] = True # If the above is true then it means the movement is a possiblity  
            if counters[counter_countup] == 0: # Checks if the movement would put the counter behind the start tile
                possible_moves[counter_countup] = False # If the above is true then it means the movement is not a possiblity  
    
    return possible_moves

def Move_Back (turn_number): # Subroutine for checking if any counters can be moved back and if so acts accordingly 
    if counterinfo[(turn_number%2)] == counterinfo[((turn_number+1)%2)] and not (counterinfo[(turn_number%2)] == 0 | counterinfo[(turn_number%2)] == 4  | counterinfo[(turn_number%2)] == 10): # Checks if the players first counter is on the same space as the other players first counter and that it is not a safe tile
        counterinfo[((turn_number+1)%2)] = 0 # Moves the other players couter back to the start
        circle_y_pos_limits[((turn_number+1)%2)] = [int(10.5*rowheight),int((10.5*rowheight)-circleradi),int((10.5*rowheight)+circleradi)] # Defines the other players counter diemsions as at the start
        
    if counterinfo[(turn_number%2)] == counterinfo[((turn_number+1)%2)+2] and not (counterinfo[(turn_number%2)] == 0 | counterinfo[(turn_number%2)] == 4  | counterinfo[(turn_number%2)] == 10): # Checks if the players first counter is on the same space as the other players second counter and that it is not a safe tile
        counterinfo[((turn_number+1)%2)+2] = 0 # Moves the other players couter back to the start
        circle_y_pos_limits[((turn_number+1)%2)+2] = [int(10.5*rowheight),int((10.5*rowheight)-circleradi),int((10.5*rowheight)+circleradi)] # Defines the other players counter diemsions as at the start
        
    if counterinfo[(turn_number%2)+2] == counterinfo[((turn_number+1)%2)] and not (counterinfo[(turn_number%2)] == 0 | counterinfo[(turn_number%2)] == 4  | counterinfo[(turn_number%2)] == 10): # Checks if the players second counter is on the same space as the other players first counter and that it is not a safe tile
        counterinfo[((turn_number+1)%2)] = 0 # Moves the other players couter back to the start
        circle_y_pos_limits[((turn_number+1)%2)] = [int(10.5*rowheight),int((10.5*rowheight)-circleradi),int((10.5*rowheight)+circleradi)] # Defines the other players counter diemsions as at the start
        
    if counterinfo[(turn_number%2)+2] == counterinfo[(((turn_number+1)%2)+2)] and not (counterinfo[(turn_number%2)] == 0 | counterinfo[(turn_number%2)] == 4  | counterinfo[(turn_number%2)] == 10): # Checks if the players second counter is on the same space as the other players seccond counter and that it is not a safe tile
        counterinfo[(((turn_number+1)%2)+2)] = 0 # Moves the other players couter back to the start
        circle_y_pos_limits[(((turn_number+1)%2)+2)] = [int(10.5*rowheight),int((10.5*rowheight)-circleradi),int((10.5*rowheight)+circleradi)] # Defines the other players counter diemsions as at the start
           
    ##START OUR GAME LOOP
    while True:
    ##HANDLE PEOPLE QUITING THE GAME
        for event in pygame.event.get(): # Checks if the user has pressed the X button and if so exits the game
            if event.type == pygame.QUIT:
                return()  
        Screen.fill(colour["background"]) # Fills the background with the defined colour
        for rownum in range (0,11): # Iterates through the values for the rows drawing each of them
            Draw_Colums(rownum) # Draws the rows
        for counternum in range (0,4): # Iterates through the number of counters
            Draw_Counter(counternum,counterinfo) # Draws the counters on to the board
        pygame.display.flip() # Updates the GUI
        
        if counterinfo[turn_number%2]== 10 and counterinfo[turn_number%2+2] == 10: # Checks if the user has both their counters on the final row
            Screen.fill(colour["white"]) # Fills the screen white
            txt.render_to(Screen,(boardWidth/2,boardHeight/2), str(names[turn_number%2+1])+ " wins", colour["black"]) # Writes on the screen that the player has won

            while True: # Loops the game until someone wins or they press the X button
                for event in pygame.event.get(): # Checks if the user has pressed a mouse button and if so exits the game
                    if event.type == "MOUSEDOWN":
                        break
                        return()
        Choose_Counter(Dice_Roll(maxsides),turn_number) # Runs the main game loop
        turn_number += 1 # Changes the turn
        pygame.display.flip() # Updates the GUI



Draw_Main() # Starts the main menu

```
