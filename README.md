import time
from plyer import notification

def water_reminder():
    while True:
        # Повідомлення нагадування
        notification.notify(
            title="Нагадування: Випийте воду 💧",
            message="Пити воду важливо для здоров'я. Зробіть кілька ковтків прямо зараз!",
            timeout=10  # Тривалість показу повідомлення (в секундах)
        )
        # Чекати одну годину (3600 секунд)
        time.sleep(3600)

if __name__ == "__main__":
    print("Програма запущена. Кожну годину буде нагадувати пити воду.")
    try:
        water_reminder()
    except KeyboardInterrupt:
        print("\nПрограма завершена.")
