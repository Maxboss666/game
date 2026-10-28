# gameboard = [' '] * 9

def show_board():
    print()
    print(f' {board[0]} | {board[1]} | {board[2]} ')
    print('---+---+---')
    print(f' {board[3]} | {board[4]} | {board[5]} ')
    print('---+---+---')
    print(f' {board[6]} | {board[7]} | {board[8]} ')
    print()


def check_win(player):
    wins = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8],  # горизонтали
        [0, 3, 6], [1, 4, 7], [2, 5, 8],  # вертикали
        [0, 4, 8], [2, 4, 6]              # диагонали
    ]
    for combo in wins:
        if board[combo[0]] == board[combo[1]] == board[combo[2]] == player:
            return True
    return False

# Функция проверки ничьей
def check_draw():
    return ' ' not in board

# Основная игра
def play():
    current_player = 'X'  # первый ходит X
    
    print('Добро пожаловать в крестики-нолики!')
    print('Номера клеток:')
    print(' 1 | 2 | 3 ')
    print('---+---+---')
    print(' 4 | 5 | 6 ')
    print('---+---+---')
    print(' 7 | 8 | 9 ')
    
    while True:
        show_board()
        
        # Просим игрока ввести номер клетки
        try:
            move = int(input(f'Игрок {current_player}, ваш ход (1-9): '))
        except ValueError:
            print('Ошибка! Введите число от 1 до 9.')
            continue
        
        # Проверяем, что число в нужном диапазоне
        if move < 1 or move > 9:
            print('Ошибка! Введите число от 1 до 9.')
            continue
        
        # Переводим в индекс (0-8)
        index = move - 1
        
        # Проверяем, свободна ли клетка
        if board[index] != ' ':
            print('Эта клетка уже занята! Выберите другую.')
            continue
        
        # Ставим символ игрока
        board[index] = current_player
        
        # Проверяем победу
        if check_win(current_player):
            show_board()
            print(f'🎉 Игрок {current_player} победил!')
            break
        
        # Проверяем ничью
        if check_draw():
            show_board()
            print('🤝 Ничья!')
            break
        
        # Меняем игрока
        if current_player == 'X':
            current_player = 'O'
        else:
            current_player = 'X'

# Запускаем игру
play()