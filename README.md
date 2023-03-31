import playsound
from pygame import mixer
import random
import time
# Initial Steps to invite in the game:
mixer.init()
mixer.music.load(r"C:\Users\bsahi\OneDrive\Desktop\pyhon project\Gaming Background Music Electronic No Copyright Free Energetic (mp3cut.net).mp3")
mixer.music.play()
print("\nWelcome to Hangman game by rubez,sahil bansal, sahil saharan and krishna\n")
name = input("Enter your name: ")
print("Hello " + name + "! Best of Luck!")
time.sleep(2)
print("The game is about to start!\n Let's play Hangman!")
time.sleep(1)


# The parameters we require to execute the game:
def main():
    global count
    global word_
    global display
    global word
    global already_guessed
    global length
    global play_game
    words_to_guess = ["rohit","shikhar","virat","surya","rishabh","hardik","jadeja","yuzi","arshdeep"
                   ,"jasprit","shami"]
    print('/n"HINT: INDIAN CRICKET TEAM"')
    word = random.choice(words_to_guess)
    word_=word
    length = len(word)
    count = 0
    display = '_' * length
    print('the length of letters to guess',len(display))
    already_guessed = []
    play_game = ""
    hangman()

# A loop to re-execute the game when the first round ends:

def play_loop():
    global play_game
    playsound.playsound(r"C:\Users\bsahi\OneDrive\Desktop\pyhon project\1671001181174ij20d2cd-voicemaker.in-speech (1).mp3")
    play_game = input("Do You want to play again? y = yes, n = no \n")
    while play_game not in ["y", "n","Y","N"]:
        play_game = input("Do You want to play again? y = yes, n = no \n")
    if play_game == "y":
        main()
    elif play_game == "n":
        print("Thanks For Playing! We expect you back again!")
        mixer.music.pause()
        exit()

# Initializing all the conditions required for the game:
def hangman():
    global count
    global display
    global word
    global already_guessed
    global play_game
    limit = 5
    guess = input("This is the Hangman Word: " + display + " Enter your guess: \n")
    if len(guess) == 0 or len(guess) >= 2 or guess <= "9":
        print("Invalid Input, Try a letter\n")
        hangman()
    elif guess in word:
        already_guessed.extend([guess])
        index = word.find(guess)
        word = word[:index] + "_" + word[index + 1:]
        display = display[:index] + guess + display[index + 1:]
        print(display + "\n")

    elif guess in already_guessed:
        print("Try another letter.\n")

    else:
        count += 1
        if count == 1:
            time.sleep(1)
            print("  ___ \n"
                  " |      \n"
                  " |      \n"
                  " |      \n"
                  " |      \n"
                  " |      \n"
                  " |      \n"
                  "_|_\n")
            playsound.playsound(r"C:\Users\bsahi\OneDrive\Desktop\pyhon project\oh no sound effect-[AudioTrimmer.com].mp3")
            print("Wrong guess. " + str(limit - count) + " guesses remaining\n")

        elif count == 2:
            time.sleep(1)
            print("  ___ \n"
                  " |   | \n"
                  " |   |\n"
                  " |      \n"
                  " |      \n"
                  " |      \n"
                  " |      \n"
                  "_|_\n")
            playsound.playsound(r"C:\Users\bsahi\OneDrive\Desktop\pyhon project\oh no sound effect-[AudioTrimmer.com].mp3")
            print("Wrong guess. " + str(limit - count) + " guesses remaining\n")

        elif count == 3:
            time.sleep(1)
            print("  ___ \n"
                 "  |   | \n"
                 "  |   |\n"
                 "  |   | \n"
                 "  |      \n"
                 "  |      \n"
                 "  |      \n"
                 " _|_\n")
            playsound.playsound(r"C:\Users\bsahi\OneDrive\Desktop\pyhon project\oh no sound effect-[AudioTrimmer.com].mp3")
            print("Wrong guess. " + str(limit - count) + " guesses remaining\n")

        elif count == 4:
            time.sleep(1)
            print("   ___ \n"
                  "  |   | \n"
                  "  |   |\n"
                  "  |   | \n"
                  "  |   O \n"
                  "  |      \n"
                  "  |      \n"
                  " _|_\n")
            playsound.playsound(r"C:\Users\bsahi\OneDrive\Desktop\pyhon project\oh no sound effect-[AudioTrimmer.com].mp3")
            print("Wrong guess. " + str(limit - count) + " last guess remaining\n")

        elif count == 5:
            time.sleep(1)
            print("   ___ \n"
                  "  |   | \n"
                  "  |   |\n"
                  "  |   | \n"
                  "  |   O \n"
                  "  |  /|\ \n"
                  "  |  / \ \n"
                  " _|_\n")
            print("Wrong guess. You are hanged!!!\n")
            playsound.playsound(r"C:\Users\bsahi\OneDrive\Desktop\pyhon project\oh no sound effect-[AudioTrimmer.com].mp3")
            print("The word was:",word_)
            play_loop()

    if word == '_' * length:
        print("Congrats! You have won the game!")
        playsound.playsound(r"C:\Users\bsahi\Downloads\Audience Clapping - Sound Effect (1).mp3")
        play_loop()

    elif count != limit:
        hangman()
main()
