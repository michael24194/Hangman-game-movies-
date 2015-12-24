print("Welcome to hangman game...in order to win you have to guess the dashed")
print("word by guessing its letters...if you make 6 wrong guesses then you will")
print("lose...to give you a hint , this word is a name of a movie...let's start")
playAgain = "y"
f = open('words.txt','r')
words = f.readlines()
sizeOfWords = len(words) - 1
while playAgain == "y":
    from random import randint
    ind = randint(0,sizeOfWords)
    selectedWord = words[ind]
    sWord = list(selectedWord)
    guessedWord = ""
    gW = list(guessedWord)
    len = 0
    space = " "
    for i in selectedWord:
        len = len + 1
    if ind != sizeOfWords:
        len = len - 1
    for i in range(0,len):
        if selectedWord[i] is space:
            guessedWord = guessedWord + " "
            gW.append(" ")
        else :
            guessedWord = guessedWord + "-"
            gW.append("-")
    print(guessedWord)
    trials = 6
    missed = []
    outMissed = []
    wrongMissed = []
    outWrongMissed = []
    while trials > 0:
        x = input("Enter a letter : ")
        x = str(x)
        xC = x.capitalize()
        xs = x.lower()
        if  not x.isalpha():
            print("Letters only !")
            print("________________________________")
            continue
        if (missed.count(xC) != 0 or missed.count(xs) != 0):
            print("Chosen before !")
            print("________________________________")
            continue
        if (sWord.count(xC) > 0 or sWord.count(xs) > 0):
            for i in range(0,len):
                if (sWord[i] == xC):
                    gW[i] = xC
                if (sWord[i] == xs):
                    gW[i] = xs
        else :
            print("Wrong Choice !")
            trials = trials - 1
            wrongMissed.append(xC)
            wrongMissed.append(xs)
            outWrongMissed.append(x)
        missed.append(xC)
        missed.append(xs)
        outMissed.append(x)
        g = ""
        for i in range(0,len):
            g = g + gW[i]
        if trials == 6:
            print("missed letters : None")
        else:
            print("missed letters : " , outWrongMissed)
        print("chances left : " , trials)
        print("")
        print(g)
        print("________________________________")
        if gW.count("-") == 0:
            break
    if trials == 0:
        print ("Game over !")
        print ("The correct answer is " + selectedWord)
    else:
        print("You Win !")
    playAgain = input("To play again Enter 'y' : ")
    
