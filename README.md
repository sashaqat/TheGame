# TheGame
Game 
import random

def move_player():
    global player_position, score
    player_move = input("Enter 'l' to move left, 'r' to move right: ")
    if player_move == "l":
        player_position -= 1
    elif player_move == "r":
        player_position += 1
    else:
        print("Invalid input. Try again.")
        return
    
    # генерируем случайные препятствия
    obstacle_position = random.randint(0, WIDTH-1)
    if obstacle_position == player_position:
        # если препятствие находится на позиции игрока, то игрок сталкивается с ним
        print("Game over! Your score:", score)
        return
    else:
        print("Good move!")
    
    score += 1
