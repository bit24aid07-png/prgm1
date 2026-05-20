# Tic-Tac-Toe Game using Minimax Algorithm (GUI Version)

import tkinter as tk
from tkinter import messagebox

# Initialize the board
board = [' ' for _ in range(9)]

HUMAN = 'X'
AI = 'O'


# Function to check for a winner
def check_winner(board, player):
    win_conditions = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8],   # Rows
        [0, 3, 6], [1, 4, 7], [2, 5, 8],   # Columns
        [0, 4, 8], [2, 4, 6]               # Diagonals
    ]
    for condition in win_conditions:
        if all(board[i] == player for i in condition):
            return True
    return False


# Function to check if the board is full (draw condition)
def is_draw(board):
    return ' ' not in board


# Minimax Algorithm
def minimax(board, depth, is_maximizing):
    if check_winner(board, AI):
        return 1
    if check_winner(board, HUMAN):
        return -1
    if is_draw(board):
        return 0

    if is_maximizing:
        best_score = -float('inf')
        for i in range(9):
            if board[i] == ' ':
                board[i] = AI
                score = minimax(board, depth + 1, False)
                board[i] = ' '
                best_score = max(best_score, score)
        return best_score
    else:
        best_score = float('inf')
        for i in range(9):
            if board[i] == ' ':
                board[i] = HUMAN
                score = minimax(board, depth + 1, True)
                board[i] = ' '
                best_score = min(best_score, score)
        return best_score


# Function to determine the best move for AI
def best_move(board):
    best_score = -float('inf')
    move = -1
    for i in range(9):
        if board[i] == ' ':
            board[i] = AI
            score = minimax(board, 0, False)
            board[i] = ' '
            if score > best_score:
                best_score = score
                move = i
    return move


# Function to handle a button click (Human move)
def on_click(index):
    if board[index] != ' ':
        return

    board[index] = HUMAN
    buttons[index].config(text=HUMAN, fg="blue")

    if check_winner(board, HUMAN):
        messagebox.showinfo("Game Over", "Congratulations! You win!")
        reset_game()
        return
    if is_draw(board):
        messagebox.showinfo("Game Over", "It's a draw!")
        reset_game()
        return

    # AI move
    ai_move = best_move(board)
    board[ai_move] = AI
    buttons[ai_move].config(text=AI, fg="red")

    if check_winner(board, AI):
        messagebox.showinfo("Game Over", "AI wins! Better luck next time.")
        reset_game()
        return
    if is_draw(board):
        messagebox.showinfo("Game Over", "It's a draw!")
        reset_game()
        return


# Function to reset the board
def reset_game():
    global board
    board = [' ' for _ in range(9)]
    for btn in buttons:
        btn.config(text=' ')


# Main GUI setup
root = tk.Tk()
root.title("Tic-Tac-Toe (AI - Minimax)")

buttons = []
for i in range(9):
    btn = tk.Button(root, text=' ', font=('Arial', 30, 'bold'),
                    width=5, height=2,
                    command=lambda i=i: on_click(i))
    btn.grid(row=i // 3, column=i % 3)
    buttons.append(btn)

reset_btn = tk.Button(root, text="Reset", font=('Arial', 14),
                     command=reset_game)
reset_btn.grid(row=3, column=0, columnspan=3, sticky="we")

root.mainloop()
