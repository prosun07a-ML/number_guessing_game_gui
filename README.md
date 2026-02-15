import tkinter as tk
from tkinter import messagebox
import random

# Function to start new game
def new_game():
    global secret_number, attempts
    difficulty = difficulty_var.get()
    if difficulty == "Easy":
        secret_number = random.randint(1, 50)
    elif difficulty == "Hard":
        secret_number = random.randint(1, 200)
    else:
        secret_number = random.randint(1, 100)  # Medium default
    attempts = 0
    feedback_label.config(text="Guess the number!")
    guess_entry.delete(0, tk.END)

# Function to handle guess
def check_guess():
    global attempts
    guess = guess_entry.get()
    if not guess.isdigit():
        messagebox.showwarning("Invalid Input", "Please enter a number")
        return
    guess = int(guess)
    attempts += 1

    if guess < secret_number:
        feedback_label.config(text="Too low!")
    elif guess > secret_number:
        feedback_label.config(text="Too high!")
    else:
        messagebox.showinfo("You Won!", f"Correct! You guessed in {attempts} attempts")
        new_game()
        return

# Create main window
root = tk.Tk()
root.title("Number Guessing Game by Prosun")

# Difficulty selection
difficulty_var = tk.StringVar(value="Medium")
tk.Label(root, text="Select Difficulty:").pack()
tk.Radiobutton(root, text="Easy (1-50)", variable=difficulty_var, value="Easy").pack()
tk.Radiobutton(root, text="Medium (1-100)", variable=difficulty_var, value="Medium").pack()
tk.Radiobutton(root, text="Hard (1-200)", variable=difficulty_var, value="Hard").pack()

# Feedback label
feedback_label = tk.Label(root, text="Click Start to play!")
feedback_label.pack(pady=10)

# Entry for guess
guess_entry = tk.Entry(root)
guess_entry.pack()

# Buttons
tk.Button(root, text="Check Guess", command=check_guess).pack(pady=5)
tk.Button(root, text="Start New Game", command=new_game).pack(pady=5)

# Initialize game variables
secret_number = 0
attempts = 0

# Start the GUI loop
root.mainloop()
