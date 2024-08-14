def print_board(board):
    print("  " + " ".join([str(i) for i in range(15)]))
    for i, row in enumerate(board):
        print(i, " ".join(row))

def check_winner(board, player):
    def check_line(line):
        count = 0
        for cell in line:
            if cell == player:
                count += 1
                if count == 5:
                    return True
            else:
                count = 0
        return False

    # Check rows and columns
    for i in range(15):
        if check_line(board[i]) or check_line([board[j][i] for j in range(15)]):
            return True

    # Check diagonals
    for i in range(11):
        if check_line([board[i+k][k] for k in range(15-i)]) or check_line([board[k][i+k] for k in range(15-i)]):
            return True
        if check_line([board[i+k][14-k] for k in range(15-i)]) or check_line([board[k][14-i-k] for k in range(15-i)]):
            return True

    return False

def is_full(board):
    return all(cell != '.' for row in board for cell in row)

def main():
    board = [['.' for _ in range(15)] for _ in range(15)]
    current_player = 'X'

    while True:
        print_board(board)
        print(f"Player {current_player}'s turn")
        try:
            row = int(input("Enter row (0-14): "))
            col = int(input("Enter column (0-14): "))
            if row < 0 or row >= 15 or col < 0 or col >= 15:
                print("Invalid coordinates. Try again.")
                continue
            if board[row][col] != '.':
                print("Cell is already taken. Try again.")
                continue
            board[row][col] = current_player
            if check_winner(board, current_player):
                print_board(board)
                print(f"Player {current_player} wins!")
                break
            if is_full(board):
                print_board(board)
                print("It's a draw!")
                break
            current_player = 'O' if current_player == 'X' else 'X'
        except ValueError:
            print("Invalid input. Please enter a number.")

if __name__ == "__main__":
    main()
代码说明：
print_board(board): 打印棋盘的函数。
check_winner(board, player): 检查当前玩家是否获胜。它会检查所有行、列和对角线。
is_full(board): 检查棋盘是否已满。
main(): 游戏的主函数，处理玩家的输入，更新棋盘状态，切换玩家，并检查游戏是否结束。
运行代码：
将上述代码保存为一个 Python 文件（例如 gomoku.py），然后在终端或命令行中运行该文件
python gomoku.py
在命令行中，玩家将被提示输入棋盘上的位置，并轮流进行游戏。游戏会在某一方获胜或棋盘满时结束。
