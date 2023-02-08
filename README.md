Тестовое задание Python-разработчик (Junior)  

Общая информация.

В тестовом задании 2 практических задания. 
Для рассмотрения вашей кандидатуры необходимо выполнить оба практических задания. 



Задания: 

Напишите код программы на Python, которая будет в реальном времени (с максимально возможной скоростью) считывать текущую цену фьючерса XRP/USDT на бирже Binance. 
В случае, если цена упала на 1% от максимальной цены за последний час, программа должна вывести сообщение в консоль. 
При этом программа должна продолжать работать дальше, постоянно считывая актуальную цену.

Опишите, как бы вы доработали данную программу, чтобы она обрабатывала все пары, а не только XRP/USDT (код писать не нужно, просто текстом)

```Python
from binance.spot import Spot
import time


"""Остановка цикла Ctrl + C , необходима библиотека binance-connector,
команда установки библиотеки: pip install binance-connector. Для быстрого обхода 
всех остальных пар, нужно использовать (асинхроность, многопоточность)."""
def check_xpr_usdt():
    while True:
        try:
            client = Spot()
            data_in_sec = client.klines("XRPUSDT", "1s", limit=1)
            data_in_hour = client.klines("XRPUSDT", "1h", limit=1)
            result = (f'Open price: {data_in_sec[0][1]}'
                    f'\t High price in hour: {data_in_hour[0][2]}'
                    f'\t Kline open time: {data_in_sec[0][0]}'
            )
            one_percent = float(data_in_hour[0][2]) - (float(data_in_hour[0][2]) / 100)
            if one_percent > float(data_in_sec[0][1]):
                print('[INFO] Attention!!! The price fell by more than 1 percent')
            print(result)
            time.sleep(1)
        except KeyboardInterrupt:
            print('\nFinish!Good bye)')
            break


if __name__ == "__main__":
    check_xpr_usdt()
```
