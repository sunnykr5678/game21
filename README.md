# game21
The "21 Number Game" is a two-player game where players take turns adding numbers between 1 and 3 to a total. The player who reaches 21 loses. This Python project simulates the game with a strategic computer opponent, showcasing key programming concepts.

# Python code to play 21 Number Game

# Returns the nearest multiple of 4
def nearestMultiple(num):
    if num >= 4:
        near = num + (4 - (num % 4))
    else:
        near = 4
    return near

# Function to display losing message and exit
def lose():
    print("\n\nYOU LOSE!")
    print("Better luck next time!")
    exit(0)

# Checks whether the numbers are consecutive
def check_consecutive(numbers):
    for i in range(1, len(numbers)):
        if (numbers[i] - numbers[i - 1]) != 1:
            return False
    return True

# Starts the game
def start_game():
    numbers = []
    last = 0
    
    while True:
        print("Enter 'F' to take the first chance.")
        print("Enter 'S' to take the second chance.")
        chance = input('> ').upper()

        # Player takes the first chance
        if chance == "F":
            while True:
                if last == 20:
                    lose()
                else:
                    print("\nYour Turn.")
                    print("How many numbers do you wish to enter?")
                    user_count = int(input('> '))

                    if 1 <= user_count <= 3:
                        comp_count = 4 - user_count
                    else:
                        print("Wrong input. You are disqualified from the game.")
                        lose()

                    print("Now enter the values:")
                    for _ in range(user_count):
                        numbers.append(int(input('> ')))
                    
                    last = numbers[-1]

                    # Check if the input numbers are consecutive
                    if check_consecutive(numbers):
                        if last == 21:
                            lose()
                        else:
                            # Computer's turn
                            for j in range(1, comp_count + 1):
                                numbers.append(last + j)
                            print("Order of inputs after computer's turn:")
                            print(numbers)
                            last = numbers[-1]
                    else:
                        print("\nYou did not input consecutive integers.")
                        lose()

        # Player takes the second chance
        elif chance == "S":
            comp_count = 1
            last = 0
            while last < 20:
                # Computer's turn
                for j in range(1, comp_count + 1):
                    numbers.append(last + j)
                print("Order of inputs after computer's turn:")
                print(numbers)

                if numbers[-1] == 20:
                    lose()
                else:
                    print("\nYour turn.")
                    print("How many numbers do you wish to enter?")
                    user_count = int(input('> '))

                    print("Enter your values:")
                    for _ in range(user_count):
                        numbers.append(int(input('> ')))
                    
                    last = numbers[-1]

                    if check_consecutive(numbers):
                        near = nearestMultiple(last)
                        comp_count = near - last
                        if comp_count == 4:
                            comp_count = 3
                    else:
                        print("\nYou did not input consecutive integers.")
                        lose()

            print("\n\nCONGRATULATIONS!!!")
            print("YOU WON!")
            exit(0)

        else:
            print("Wrong choice. Please try again.")

# Main game loop
game = True
while game:
    print("Player 2 is Computer.")
    print("Do you want to play the 21 Number Game? (Yes / No)")
    answer = input('> ').lower()
    if answer == 'yes':
        start_game()
    else:
        print("Do you want to quit the game? (yes / no)")
        next_action = input('> ').lower()
        if next_action == "yes":
            print("You are quitting the game...")
            exit(0)
        elif next_action == "no":
            print("Continuing...")
        else:
            print("Wrong choice. Please try again.")
