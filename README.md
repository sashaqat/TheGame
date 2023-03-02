# TheGame
Game 
import random

def move_player():
    global player_position, score, speed, coins_collected
    player_move = input("Enter 'l' to move left, 'r' to move right: ")
    if player_move == "l":
        player_position -= 1
    elif player_move == "r":
        player_position += 1
    else:
        print("Invalid input. Try again.")
        return
    
    # генерируем случайные препятствия и бонусы
    obstacle_position = random.randint(0, WIDTH-1)
    coin_position = random.randint(0, WIDTH-1)
    speed_bonus_position = random.randint(0, WIDTH-1)
    
    if obstacle_position == player_position:
        # если препятствие находится на позиции игрока, то игрок сталкивается с ним
        print("Game over! Your score:", score)
        return
    else:
        print("Good move!")
    
    if coin_position == player_position:
        # если монета находится на позиции игрока, то игрок собирает ее
        coins_collected += 1
        score += 10
        print("You collected a coin! Score +10")
    
    if speed_bonus_position == player_position:
        # если бонус ускорения находится на позиции игрока, то игрок получает ускорение на 5 ходов
        speed += 1
        print("You got a speed bonus! Speed +1 for 5 turns")
    
    # уменьшаем скорость игрока, если бонус ускорения истек
    if speed > 1:
        speed -= 1
    
    score += 1
