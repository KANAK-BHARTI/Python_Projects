import random


def choose_word():
    words = ["python", "hangman", "programming", "computer", "game", "developer"]
    return random.choice(words)


def display_word(word, guessed_letters):
    display = ""
    for letter in word:
        if letter in guessed_letters:
            display += letter
        else:
            display += "_"
    return display


def hangman():
    word = choose_word()
    guessed_letters = []
    attempts = 6

    print("Welcome to Hangman!")
    print("You have 6 attempts to guess the word.")

    while attempts > 0:
        print("\n" + display_word(word, guessed_letters))
        guess = input("Guess a letter: ").lower()

        if len(guess) != 1 or not guess.isalpha():
            print("Please enter a single letter.")
            continue

        if guess in guessed_letters:
            print("You already guessed that letter.")
            continue

        guessed_letters.append(guess)

        if guess not in word:
            attempts -= 1
            print("Incorrect guess. You have {} attempts left.".format(attempts))
            if attempts == 0:
                print("Sorry, you ran out of attempts. The word was '{}'.".format(word))
                break
        else:
            print("Correct guess!")

        if all(letter in guessed_letters for letter in word):
            print("Congratulations! You guessed the word '{}'!".format(word))
            break

    play_again = input("Do you want to play again? (yes/no): ").lower()
    if play_again == "yes":
        hangman()
    else:
        print("Thanks for playing!")


if __name__ == "__main__":
    hangman()
