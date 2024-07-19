# mastermind_game
import random

def get_hint(secret, guess):
    correct_position = 0
    correct_digit = 0
    secret_digits = list(secret)
    guess_digits = list(guess)

    for i in range(len(secret_digits)):
        if guess_digits[i] == secret_digits[i]:
            correct_position += 1
            secret_digits[i] = guess_digits[i] = None

    for digit in guess_digits:
        if digit is not None and digit in secret_digits:
            correct_digit += 1
            secret_digits[secret_digits.index(digit)] = None

    return correct_position, correct_digit

def play_round(player_num):
    print(f"\nPlayer {player_num}'s turn to set the number.")
    while True:
        secret = input("Enter a multi-digit number: ")
        if secret.isdigit():
            break
        print("Please enter a valid multi-digit number.")
    
    attempts = 0
    print(f"\nPlayer {player_num % 2 + 1}'s turn to guess the number.")
    
    while True:
        guess = input("Enter your guess: ")
        if guess == secret:
            attempts += 1
            print(f"Correct! You've guessed the number in {attempts} attempts.")
            break
        elif guess.isdigit():
            attempts += 1
            correct_position, correct_digit = get_hint(secret, guess)
            print(f"Correct digits in correct positions: {correct_position}")
            print(f"Correct digits in wrong positions: {correct_digit}")
        else:
            print("Please enter a valid multi-digit number.")
    
    return attempts

def main():
    print("Welcome to the Mastermind Game!")
    
    # Player 1's round
    attempts_player1 = play_round(1)
    
    # Player 2's round
    attempts_player2 = play_round(2)
    
    # Determine winner
    if attempts_player1 < attempts_player2:
        print(f"\nPlayer 1 wins and is crowned Mastermind with {attempts_player1} attempts!")
    elif attempts_player2 < attempts_player1:
        print(f"\nPlayer 2 wins and is crowned Mastermind with {attempts_player2} attempts!")
    else:
        print("\nIt's a tie! Both players are equally matched.")

if __name__ == "__main__":
    main()
