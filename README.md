import time
import random
import tkinter as tk
from tkinter import messagebox

# Змінні
last_drink_time = None
penalty_points = 0
achievements = []

# Функція для нагадування пити воду
def remind_to_drink():
    global last_drink_time
    last_drink_time = time.time()
    messagebox.showinfo("Нагадування", "Час пити воду! Пийте, щоб бути здоровим!")

# Функція для перевірки, чи був зроблений прихід води
def check_for_water_drink():
    global last_drink_time, penalty_points, achievements
    if last_drink_time is None:
        return  # Якщо час останнього пиття не записано
    
    elapsed_time = time.time() - last_drink_time
    # Якщо не пиття води протягом 2 годин
    if elapsed_time > 7200:  # 2 години = 7200 секунд
        # Покарання за невиконання
        penalty_points += 10
        achievements.append("Не попив води вчасно!")
        messagebox.showwarning("Штраф", "Ви не попили воду вчасно! Ви отримали 10 штрафних балів.")
    
    # Якщо набралося більше 50 балів штрафу
    if penalty_points >= 50:
        messagebox.showerror("Нагадування", "Ви отримали більше 50 штрафних балів! Негайно зверніться до коуча.")
        penalty_points = 0  # Скидання балів після попередження

# Функція для підрахунку досягнень
def check_achievements():
    global achievements
    if len(achievements) > 3:
        messagebox.showinfo("Досягнення", "Вітаємо! Ви стали здорованом, що регулярно п’є воду!")
        achievements = []  # Скидання досягнень після досягнення мети

# Створення графічного інтерфейсу
def create_gui():
    root = tk.Tk()
    root.title("Нагадувач для пиття води")

    # Створення кнопок
    remind_button = tk.Button(root, text="Нагадати пити воду", command=remind_to_drink)
    remind_button.pack(pady=10)

    check_button = tk.Button(root, text="Перевірити, чи попили воду", command=check_for_water_drink)
    check_button.pack(pady=10)

    achievements_button = tk.Button(root, text="Перевірити досягнення", command=check_achievements)
    achievements_button.pack(pady=10)

    # Запуск циклу перевірок кожні 10 хвилин
    def periodic_check():
        check_for_water_drink()
        check_achievements()
        root.after(600000, periodic_check)  # 600000 мс = 10 хвилин

    root.after(600000, periodic_check)
    root.mainloop()

# Запуск програми
if __name__ == "__main__":
    create_gui()
