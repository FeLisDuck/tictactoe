# tictactoe
my first program))))

import random
board = list(range(1,10))

print("TicTacToe (v1.1)")
print("=" * 80)
print("""Правила гри
Гравці по черзі ставлять на вільні клітини поля 3х3 знаки (один завжди хрестики,
інший завжди нулики). Перший, хто зумів побудувати в ряд 3 своїх фігури по верт-
икалі, горизонталі або діагоналі, виграє. Перший хід робить гравець, що ставить
хрестики.""")
print("=" * 80)
print("""Оберіть режим:
1 - Гравець1 проти гравця2
2 - Гравець проти компютера""")

def draw_board(board):
    for i in range(3):
        print ("[", board[0+i*3], "][", board[1+i*3], "][", board[2+i*3], "]")

def menu():
  while True:
     us2 = input("Ваш вибір > ")
     if us2 == "1":
       main0(board)
     elif us2 == "2":
        main1(board)
     else:
       continue

def ifu1():
    valid = False
    while not valid:
        player_answer = input("Куди поставимо  X ? > ")
        try:
            player_answer = int(player_answer)
        except:
            print ("Неправильний символ. Ви впевнені, що ввели число?")
            continue
        if player_answer >= 1 and player_answer <= 9:
            if (str(board[player_answer-1]) not in "XO"):
                board[player_answer-1] = "X"
                valid = True
            else:
                print ("Ця клітинка вже зайнята")
        else:
            print ("Введіть число в діапазоні від 1 до 9.")

def take_input(player_token):
    valid = False
    while not valid:
        player_answer = input("Куди поставимо " + player_token+"? ")
        try:
            player_answer = int(player_answer)
        except:
            print ("Неправильний символ. Ви впевнені, що ввели число?")
            continue
        if player_answer >= 1 and player_answer <= 9:
            if (str(board[player_answer-1]) not in "XO"):
                board[player_answer-1] = player_token
                valid = True
            else:
                print ("Ця клітинка вже зайнята")
        else:
            print ("Введіть число в діапазоні від 1 до 9.")
            
def ifc():
    print("Хід компютера:")
    valid = False
    while not valid:
        player_answer = random.randint(1, 9)
        if player_answer >= 1 and player_answer <= 9:
            if (str(board[player_answer-1]) not in "XO"):
                board[player_answer-1] = "O"
                valid = True
            else:
                continue
            
def check_win(board):
    win_coord = ((0,1,2),(3,4,5),(6,7,8),(0,3,6),(1,4,7),(2,5,8),(0,4,8),(2,4,6))
    for each in win_coord:
        if board[each[0]] == board[each[1]] == board[each[2]]:
            return board[each[0]]
    return False

def main0(board):
    counter = 0
    win = False
    while not win:
        draw_board(board)
        if counter % 2 == 0:
            take_input("X")
        else:
            take_input("O")
        counter += 1
        if counter > 4:
            tmp = check_win(board)
            if tmp:
                print (tmp, "виграв!")
                win = True 
                thinn = input("Бажаєте ще зіграти[Y/N]? ")
                if thinn == "Y":
                 menu()
                else:
                 break
        if counter == 9:
            print ("Нічия!")
            thinn = input("Бажаєте ще зіграти[Y/N]? ")
            if thinn == "Y":
             menu()
            else:
             break
            draw_board(board)

def main1(board):
    counter = 0
    win = False
    while not win:
        draw_board(board)
        if counter % 2 == 0:
            ifu1()
        else:
            ifc()
        counter += 1
        if counter > 4:
            tmp = check_win(board)
            if tmp:
                print (tmp, "Виграв!")
                win = True
                break
        if counter == 9:
            print ("Нічия!")
            break
draw_board(board)

menu()
