# tictactoe
Tictactoe game

# global variables


# Game Board
board = ["-", "-", "-",
         "-", "-", "-", 
         "-", "-", "-",] 

         
# if game is still going
game_still_going = True
  
# Who won or tie?
winner = None

# Who's turn is it?
current_player = "X"


# Display board
def display_board():
  print(board[0] + " | " + board[1] + " | " + board[2])
  print(board[3] + " | " + board[4] + " | " + board[5])
  print(board[6] + " | " + board[7] + " | " + board[8])


#Play a game of tic tac toe 
def play_game():

  # Display Intial Board
  display_board()
  # While the game is stil going
  while game_still_going:
    # handle a turn to an arbitraty player
    handle_turn(current_player)
    # check if the game has ended
    check_game_over()
    # flip to the other player
    flip_player()

    if winner == "X" or  winner == "O":
      print (winner + " won.")
    elif winner == None:
      print ("Tie.")

 
# Handle a single turn to an arbitrary player
def handle_turn(player):

  print (player + "'s turn.")
  position = input("Choose a position from 1-9: ")
  
  valid = False
  while not valid:
  
    while position not in ["1","2","3","4","5","6","7","8","9"]:
      position = input("Invalid Input,choose a position from 1-9: ") 
    
    position = int(position) - 1

    if board[position] ==  "-":
      valid = True
    else:
      print ("Choose a different possition")
    
  board[position] = player
  
  display_board()


def check_game_over():
  check_for_winner()
  check_if_tie()


def check_for_winner():
# Set up global variables
  global winner

  #check rows
  row_winner = check_rows()

  # check columns
  column_winner = check_columns()
  
  #check check_diagonals
  diagonal_winner = check_diagonals()

  if row_winner:
    winner = row_winner
  #there is a win
  elif column_winner:
     winner = column_winner
   # there was a win
  elif diagonal_winner:
     winner = diagonal_winner
   #there was a win
  else: 
    winner = None
  return
  # there was no win 



def check_rows():
# Set up global variables 
  global game_still_going
  # Check if rows are all the same and is not empty

  row_1 = board[0] == board[1] == board[2] != "-"
  row_2 = board[3] == board[4] == board[5] != "-"
  row_3 = board[6] == board[7] == board[8] != "-"

#if a any row does have any match,flag that there is a win.
  if row_1 or row_2 or row_3:
    game_still_going = False
  
  #Return the winner ( X or 0)
  if row_1:
    return board[0]
  elif row_2:
    return board[3]
  elif row_3:
    return board[6]
  return

def check_columns():
  # Set up global variables 
  global game_still_going
  # Check if any of the columns are all the same and is not empty

  column_1 = board[0] == board[3] == board[6] != "-"
  column_2 = board[1] == board[4] == board[7] != "-"
  column_3 = board[2] == board[5] == board[8] != "-"

#if a any column does have any match,flag that there is a win.
  if column_1 or column_2 or column_3:
    game_still_going = False
  
  #Return the winner ( X or 0)
  if column_1:
    return board[0]
  elif column_2:
    return board[1]
  elif column_3:
    return board[2]
    return
  
def check_diagonals():
   # Set up global variables 
  global game_still_going
  # Check if any of the diagonals are all the same and is not empty
  diagonals_1 = board[0] == board[4] == board[8] != "-"
  diagonals_2 = board[6] == board[4] == board[2] != "-"

  # if any diagonals does have a match,flag that there is a win.
  if diagonals_1 or diagonals_2:
    game_still_going = False
  #Return the winner ( X or O )
  if diagonals_1:
    return board[0]
  elif diagonals_2:
    return board[6]
  return


def check_if_tie():
  if "-" not in board:
    game_still_going = False
  
  return


def flip_player():
  #Global variables we need
  global current_player
  #if the current player is X change it to O
  if current_player == "X" :
    current_player = "O"
  #if the current player is O change it to X
  elif current_player == "O":
    current_player = "X"
  return


play_game()
