# tictactoe
python game
import  random

def display_board(board):

    print(board[7]+'|'+board[8]+'|'+board[9])

    print(board[4]+'|'+board[5]+'|'+board[6])

    print(board[1]+'|'+board[2]+'|'+board[3])

#testcase=['x','x','o','x','o','x','o','x','o','x','0']
#display_board(testcase)

def player():
    marker=''
    while marker!='x' and marker!='o':
        marker=input("player1,choose x or o")
    player1=marker
    if marker=='x':
        player1='x'
        player2='o'
    else:
        player2='x'
    return(player1,player2)


def place_marker(board,marker,position):
    board[position]=marker
#place_marker(testcase,'@',8)
#display_board(testcase)

def win_check(board,mark):
    return ((board[1]==board[2]==board[3]==mark)or(board[4] == board[5] == board[6] == mark)or(board[7] == board[8] == board[9] == mark)or(board[1] == board[7] == board[4] == mark)or(board[5] == board[2] == board[8] == mark)or(board[9] == board[6] == board[3] == mark)or(board[7] == board[5] == board[3] == mark)or(board[1] == board[5] == board[9] == mark))
#win_check(testcase,'x')

def space_check(board,position):
    return(board[position]=='')

def is_board_full(board):
    for i in range(1,10):
        if space_check(board,i):
            return  False#board not full
        #board is full
    return  True

def player_choice(board):
    position=0
    if position not in range(1,10) or not(space_check(board,position)):
        position=int(input("enter a valid position(1-9)"))
    return position

def replay():
    choice=input("do u want to play again? yes or no")
    return choice=="yes"

def choose_turn():
    flip=random.randint(0,1)
    if flip==0:
        return  ("player1")
    else:
        return ("player2")


print("Welcome to TIC TAC TOE")

while True:

    the_board=['']*10
    player1,player2=player()

    turn=choose_turn()
    print(turn+" will play first")

    play_game=input("ready to play? yes or no")
    if play_game=='yes':
        game_on=True
    else:
        game_on=False

    while game_on:
        if turn == 'player1':
            display_board(the_board)
            position = player_choice(the_board)
            place_marker(the_board, player1, position)

            if win_check(the_board, player1):
                display_board(the_board)
                print("player1 won!!!")
                game_on = False
            else:
                if is_board_full(the_board):
                    display_board(the_board)
                    print("tie game!!!")
                    game_on = False
                else:
                    turn = player2
        else:
            display_board(the_board)
            position = player_choice(the_board)
            place_marker(the_board, player2, position)

            if win_check(the_board, player2):
                display_board(the_board)
                print("player2 won!!!")
                game_on = False
            else:
                if is_board_full(the_board):
                    display_board(the_board)
                    print("tie game!!!")
                    game_on = False
                else:
                    turn = "player1"
    if not replay():
        break;
