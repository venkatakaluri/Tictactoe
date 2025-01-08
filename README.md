# Tic-Tac-Toe Game Implementation
# # Game Board and Initial Setup
board = [' ' for _ in range(9)]  # Initialize the board with empty spaces

# Function to Display the Board
def display_board():
    print("\n")
    for row in [board[i:i + 3] for i in range(0, 9, 3)]:
        print(" | ".join(row))
        print("-" * 5)
    print("\n")

# Function to Check if a Player Has Won
def check_winner(player):
    win_combinations = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8],  # Rows
        [0, 3, 6], [1, 4, 7], [2, 5, 8],  # Columns
        [0, 4, 8], [2, 4, 6]              # Diagonals
    ]
    for combo in win_combinations:
        if all(board[pos] == player for pos in combo):
            return True
    return False

# Function to Check for a Tie
def check_tie():
    return ' ' not in board

# Function to Make a Move
def make_move(position, player):
    if board[position] == ' ':
        board[position] = player
        return True
    return False

# Main Function for Game Logic
def tic_tac_toe():
    print("Welcome to Tic-Tac-Toe!")
    print("Player 1: X | Player 2: O\n")
    display_board()
    
    current_player = 'X'
    
    while True:
        try:
            move = int(input(f"Player {current_player}, choose a position (1-9): ")) - 1
            if move < 0 or move >= 9:
                print("Invalid input. Please choose a number between 1 and 9.")
                continue
            
            if make_move(move, current_player):
                display_board()
                
                if check_winner(current_player):
                    print(f"Player {current_player} wins! 🎉")
                    break
                
                if check_tie():
                    print("It's a tie! 🤝")
                    break
                
                # Switch Player
                current_player = 'O' if current_player == 'X' else 'X'
            else:
                print("This position is already occupied. Try again.")
        except ValueError:
            print("Invalid input. Please enter a number between 1 and 9.")
            
# Run the Game
tic_tac_toe()
