# Convert
Импорт библиотеки:

import requests
Здесь мы импортируем библиотеку requests, которая используется для выполнения HTTP-запросов к API.

Получение курса валют:

def get_exchange_rate():
    try:
        response = requests.get("https://api.exchangerate-api.com/v4/latest/RUB")
        data = response.json()
        return data['rates']['USD']
    except Exception as e:
        print("Ошибка при получении курса валют:", e)
        return None
Функция get_exchange_rate отправляет GET-запрос к API для получения актуального курса рубля к доллару. Если запрос успешен, курс возвращается, иначе выводится сообщение об ошибке, и функция возвращает None.

Конвертация рублей в доллары:

def convert_rub_to_usd(rubles, exchange_rate):
    return rubles * exchange_rate
Функция convert_rub_to_usd принимает сумму в рублях и курс валюты, затем возвращает эквивалентную сумму в долларах.

Основная логика программы:

def main():
    print("Добро пожаловать в конвертер валют!")
    exchange_rate = get_exchange_rate()

    if exchange_rate is None:
        print("Не удалось получить курс валют. Закрытие программы.")
        return

    print(f"Актуальный курс: 1 RUB = {exchange_rate:.2f} USD")

    while True:
        try:
            rubles = float(input("Введите сумму в рублях (или 'exit' для выхода): "))
            dollars = convert_rub_to_usd(rubles, exchange_rate)
            print(f"{rubles} RUB = {dollars:.2f} USD")
        except ValueError:
            print("Ввод завершен. Выход из программы.")
            break
В функции main происходит следующее:

Приветствие пользователя.
Получение обменного курса. Если курс не удалось получить, программа завершает работу.
Вывод актуального курса.
Бесконечный цикл, в котором пользователь может вводить сумму в рублях для конвертации. Если пользователь вводит некорректное значение (например, текст), программа завершает работу.
Запуск программы:

if __name__ == "__main__":
    main()
Эта конструкция позволяет запустить функцию main, только если скрипт выполняется как основной модуль.
