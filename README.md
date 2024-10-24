# 基本仕様
- プログラミング言語：Python
- GUIライブラリ：Tkinter

# 使用方法
import tkinter as tk
from tkinter import messagebox
import random

class BingoSystem:
    def __init__(self, root):
        self.root = root
        self.root.title("ビンゴの司会システム")

        self.remaining_numbers = list(range(1, 76))
        random.shuffle(self.remaining_numbers)
        self.selected_numbers = []

        self.label = tk.Label(root, text="番号がここに表示されます", font=("Arial", 24))
        self.label.pack(pady=20)

        self.history_text = tk.Text(root, height=10, width=30)
        self.history_text.pack()

        self.pick_button = tk.Button(root, text="番号を選択", command=self.pick_number, font=("Arial", 18))
        self.pick_button.pack(pady=20)

    def pick_number(self):
        if not self.remaining_numbers:
            messagebox.showinfo("終了", "すべての番号が選ばれました。")
            return

        number = self.remaining_numbers.pop(0)
        self.selected_numbers.append(number)

        self.label.config(text=f"番号: {number}")
        self.history_text.insert(tk.END, f"{number}\n")

if __name__ == "__main__":
    root = tk.Tk()
    app = BingoSystem(root)
    root.mainloop()
