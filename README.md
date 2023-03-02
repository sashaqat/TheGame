# TheGame
Game 
import curses
import random

def main(stdscr):
    # Инициализация экрана curses
    curses.curs_set(0)
    stdscr.nodelay(1)
    stdscr.clear()
    stdscr.refresh()

    # Установка начальной позиции игрока
    player_position = 10

    # Создание монет на экране
    coins = []
    for i in range(20):
        coin = {
            'x': random.randint(0, 30),
            'y': random.randint(1, 10),
            'value': random.randint(1, 5)
        }
        coins.append(coin)

    # Основной цикл игры
    while True:
        stdscr.clear()

        # Отображение монет на экране
        for coin in coins:
            stdscr.addstr(coin['y'], coin['x'], 'O')

        # Отображение игрока на экране
        stdscr.addstr(11, player_position, 'X')

        # Отображение счета на экране
        score = sum([coin['value'] for coin in coins if coin['y'] == 11 and coin['x'] == player_position])
        stdscr.addstr(0, 0, f'Score: {score}')

        # Обработка пользовательского ввода
        key = stdscr.getch()
        if key == curses.KEY_LEFT:
            player_position = max(player_position - 1, 0)
        elif key == curses.KEY_RIGHT:
            player_position = min(player_position + 1, 30)
        elif key == ord('q'):
            break

        # Обновление позиции монет на экране
        for coin in coins:
            coin['y'] += 1
            if coin['y'] > 10:
                coin['x'] = random.randint(0, 30)
                coin['y'] = 1

        stdscr.refresh()

curses.wrapper(main)


