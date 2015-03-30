```python
#l- means local meaning that it is confined to the function
symbols = ['`', '1', '2', '3', '4', '5', '6', '7', '8', '9', '0', '-', '=', '[', ']', ';', "'", '#', ',', '.', '/', '\\', '¬', '!', '£', '$', '%', '^', '&', '*', '(', ')', '_', '+', '{', '}', ':', '@', '~', '<', '>', '?', 'é', 'í', 'ó', 'ú', 'É', 'Í', 'Ó', 'Á', 'á', 'Ú','"']
letters = ['Q', 'W', 'E', 'R', 'T', 'Y', 'U', 'I', 'O', 'P', 'A', 'S', 'D', 'F','G','H', 'J', 'U', 'K', 'I', 'L', 'Z', 'X', 'C', 'V', 'B', 'N', 'M']
arrNo = ("no","No","Nope","nope", "0","n","N",0,"0")
arrYes = ("yes","Yes","Yep","yep","yea","Yea","ye","Ye","yeah","Yeah","Yar","yar","yarr","Yarr","Yaarr","yaarr","y","Y","aye","Aye","1",1)
def importword (file): # This Function imports words.txt and solved.txt
    wordlist = []                               
    largewordlist = []
    with open(file,"r") as file:# This opens up either words.txt or solved.txt
        for line in file: # This iterates through the file that is imported
            for word in line.split(): # This removes the new lines from the file
                for letter in word: # This iterates through the words 
                    wordlist.append(letter) # This appends each letter to a list
                largewordlist.append(wordlist) # This appends the list of letters to a larger list
                wordlist = [] # This clears the list of letters           
    return largewordlist



def importclues (): # this is be used to import the starting clues
    cluesdict = {}
    with open("clues.txt","r") as file: # this opens the file
        for line in file: # this iterates through the file accessing each line
            for letter in line.split(): # this iterates through the line accessing each character
                clue = letter
                cluesdict[clue[0]] = clue[1] # this adds the letter and symbol pairings to a dictionary in the form  letter : symbol
    print("the clues are: " + str(cluesdict)) # this prints the clues dictionary
    return cluesdict # this returns the clues dictionary allowing it to be accessed from outside of the function

def makeword(oldword,lreplacemnets): # this uses the clues that the person enters and bulid the new word with it
    lnewword = oldword # This is so that oldword's value is not changed as I had a bug which revolved around this function
    for orglist in lnewword : # This iterates through lnewword 
        countup = 0
        for orgletter in orglist: # This iterates through the letters in lnewword
            countup +=1
            for repletterkey in lreplacemnets: # This iterates through the replacments dictionary
                if lreplacemnets[repletterkey] == orgletter: # This checks if the current letter is one that the user has chosen to replace
                    orglist[countup-1] = repletterkey # This changes the value of the letter
                    
                
                

    
    return lnewword
    
                                
def checker (tanswer,aanswer,arrYes,arrNo):  # Checker checks if your answer is the same as the actual answer                                       
    if tanswer == aanswer: # Checks if the user has won
        while True:
            try:
                strinput = str(input("do you want to restart? "))
            except:
                print("please enter a string") # If the user doesn't enter a string then the system will respond with this
            if strinput in arrYes: # This checks if the user has entered a yes
                    print("okay restarting")
                    return True # This returns to the game
            elif strinput in arrNo: # This checks if the user has entered a no
                    print("well done")
                    exit() # This exits the game
            else: # This checks if neither of the above are true
                print("please enter a real  yes or no")
            
    else: # Checks if the user has not won
        print("YOU HAVE FAILED...MISERABLY")
        while True:
            try:
                strinput = str(input("do you want to forfeit? "))
            except:
                print("please enter a string") # If the user doesn't enter a string then the system will respond with this
            print("") #linebreak
            if lose in arrYes: # This checks if the user has entered a yes
                exit() # This closes the game
            elif lose in arrNo: # This checks if the user has entered a no
                print("try again")
                print("") #linebreak
                return # This returns to the game
            else: # This checks if neither of the above are true
                print("please enter a real yes or no")                 

                            
def theirdecision(currentword,ans,arrYes,arrNo,orgword,clues): # This serves as the main menu
    while True: # This allows the input to be looped if an incorrect input if inputed
        thierinp = int
        print("""please select a number
    0 is to delete a letter and symbol pairing
    1 is press add a letter and symbol pairing
    2 is to view how many times each symbol comes up
    3 is to check if you are correct """)# This presents the user with the options
        thierinp = int(input("")) # This allows the user to input their option
        if thierinp == 0: # This checks if the user wants to delete a letter and symbol pairing 
            return pairedit(False,clues,currentword,ans,arrYes,arrNo,orgword), False # This removes the pairings to the dictionary, then updates the list
        elif thierinp == 1: # This checks if the user wants to add a letter and symbol pairing
            return pairedit(True,clues,currentword,ans,arrYes,arrNo,orgword), True # This adds the pairings to the dictionary, then updates the list
        elif thierinp == 2: # This checks if the user wants to check how often a letter and symbol pairing comes up
            symbolfrequency (orgword)# This checks how often a letter and symbol pairing comes up
            return(None,None)
        elif thierinp == 3: # This checks if the user wants to check if they are correct
            hello = checker(currentword,ans,arrYes,arrNo) # This checks if the user's final solution is correct
            if hello == False: # Allows the user to exit() the code if they so desire
                exit() # Exits the code
            elif hello == True:
                return(None,None)# continues running the code
            else:
                return(None,None)

        else:
          print("please input 0,1,2 or 3") # This checks whether or not the users inputs are in the range of inputs given and tells them to try again



def symbolfrequency (orgword): # This tells the user how many times the individual symbols come up
    dictsymbols = {} 
    for word in orgword:    # These for loops break down the final solution into letters, stored in the varible letter
        for letter in word: # ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
            if letter in dictsymbols: # This checks if the symbol has already occured in this iteration
                dictsymbols[letter] += 1 # Adds one to its frequency 
            else: # This checks if the symbol has not already occured in this iteration
                dictsymbols[letter] = 1 # Makes it's frequency 1

    for letterfrequency in dictsymbols:
        print("there are " + str(dictsymbols[letterfrequency]) + " " + str(letterfrequency) +"'s") # This prints out how many of each symbol there is
        print("")                                                                   #linebreak

def pairedit (replacing,clues,currentword,ans,arrYes,arrNo,orgword): # This allows the user to add or remove a letter and symbol paring
    listofcountup = []
    replacers = []
    line = [""]
    key = ""
    nocountasupsp = 0
    nocountasup = 0
    bob = False
    print("the pairings are ")          # This prints out all the current pairing
    for countup in clues:               # ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
        print(countup , clues[countup]) # ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
        nocountasupsp += 1              # ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
        listofcountup += countup        # ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
        replacers += clues[countup]     # ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
    for countasup in orgword: # This prints out the user's word that they started off with
        line += countasup     # ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
    print("The current word is")    # This prints out the user's current word
    presentlistolists (currentword) # ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
    if nocountasupsp == 3 and replacing != True : # This checks if the user has added no clues and is chosing to remove a clue
        return() # This returns the user to the menu
    while bob == False:
        try:
            
            key = str(input("what symbol do you want to replace/remove replacment of "))
            if replacing == True and key not in replacers and len(key) == 1 and key in line and  key in symbols and key not in letters: # This checks if the user is adding a symbol replacement, if it is 1 charater long and if it not already a replaced symbol and if it is in the list of letters                                                            
                bob = True # Breaks out of the loop
            if replacing != True and key in replacers: # Checks if the user is removing a replacement and if that is a replacement
                bob = True # Breaks out of the loop
        except:
            print("please enter a one charater long string")
        
    if replacing == True: # Checks if the user is replacing a symbol
        lreplacmentdict = {}
        replacer = ""
        while True:
            try:
                replacer = str(input("what letter do you want to replace it with "))
                replacer = replacer.upper() # Capalitises the user's input
                if replacer not in listofcountup and len(replacer) == 1 and replacer not in symbols and replacer in letters:  # Checks if the letter has not already been added, that it is one charater long and that it is not a symbol
                    lreplacmentdict[replacer] = key # Adds the pairing to a dictionary
                    return lreplacmentdict
                else:
                    print("please enter a letter")
            except:
                print("please enter a one charater string")
    else:
        return key # If the user is removing a pairing then it will return the key, which is removed from the dictionary in the try1 function

def presentlistolists (present):# This displays the list of words that the user has to decypt 
    linestr = ""
    word = ""
    line = []
    for line in present:
        for word in line:
            linestr += word
        print(linestr)
        linestr = ""
                            
def start (arrYes,arrNo):# This subroutine defines the major varibles
    orgword = importword ("words.txt") # This imports the starting word
    ans = importword ("solved.txt") # This imports the solved word
    clues = importclues () # This imports the clues
    input("Press Enter") # Pause in order for the user to read the clues
    print() # linebreak                         
    print("the orignal words were ")
    presentlistolists(orgword) # Presents the orginal words
    input("Press Enter") # Pause in order for the user to read the orginal words
    currentword = makeword(importword("words.txt"),clues) # This generates the word list that the user will work with
    print() #linebreak
    print("the new word is ")
    presentlistolists(currentword) # Presents the current words
    input("Press Enter") # Pause in order for the user to read the current words
    print("")#linebreak
    try1(currentword,ans,arrYes,arrNo,orgword,clues)


def try1(currentword,ans,arrYes,arrNo,orgword,clues):# This subroutine it takes a new pairing adds it to the clues dictionary and updates the word
    while True:
        addontoclues , replacings = theirdecision(currentword,ans,arrYes,arrNo,orgword,clues)
        tempclues = []
        for lcountups in clues:    # This generates a list of keys that the dictionary has
            tempclues += lcountups # ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
        if replacings == False: # Checks if the user is removing a pairing
            for lcountups in tempclues: # iterates through the list of keys
                if clues[lcountups] == addontoclues: # Checks if that key is the one being removed
                    del clues[lcountups] # Removes Respective key
                    
        elif replacings == True: # Checks if the user is adding a pairing
            for lcountups in addontoclues: # Iterates through the new pairing being added
                clues[lcountups] = addontoclues[lcountups] # adds the new pairing
        else: # Checks if the user is neither adding nor removing a symbol pairing 
            continue # returns to the start of the while loop
        currentword = makeword(importword ("words.txt"),clues) # Build up the new word
        presentlistolists (currentword) # This presents the new words
        

while True:              # This loops the game       
    start (arrYes,arrNo) # ^^^^^^^^^^^^^^^^^^^

```
