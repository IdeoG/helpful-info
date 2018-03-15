# Курс по Python от МФТИ и Mail.ru по асинхронному программированию

## Декораторы

``` python
def logger(filename):
    def decorator(func):
        def wrapped(*args, **kwargs):
            result = func(*args, **kwargs):
            with open(filename, 'a') as f:
                f.write(result)
            return result

@logger("new_log.txt")
def summator(num_list):
    return sum(num_list)

# In  [ ]: summator([1, 2, 3, 4, 5])
# Out [ ]: 15
# Также число 15 было записано в файл new_log.txt
```

## Генераторы

``` python
def accumulator():
    total = 0
    while True:
        value = yield total
        print('Got: {}'.format(value))

        if not value: break
        total += value

generator = accumulator()

# Инициализируем генератор
# In  [ ]: next(generator)
# Out [ ]: 0

# Отправляем генератору 1
# In  [ ]: print('Accumulated: {}'.format(generator.send(1)))
# Out [ ]: Got: 1
#          Accumulated: 1

# Отправляем генератору 1
# In  [ ]: print('Accumulated: {}'.format(generator.send(1)))
# Out [ ]: Got: 1
#          Accumulated: 2

# Выходим 
# In  [ ]: next(generator)
# Out [ ]: Got None
# ----------------
# StopIteration
```

- Хранит только текущее положение

## Magic method

Это методы, которые начинаются и заканчиваются двумя подчеркиваниями "__"

- init - метод, вызываемый при инициализации объекта класса
- new - метод, вызываемый при инициализации класса
- str - метод, вызываемый при print(obj)
- call - метод, вызываемый при каждом вызове объекта
- add - перегрузка оператора "+"


## Контекстные менеджеры

``` python
import time

class timer():
    def __init__(self):
        self.start = time.time()

    def current_time(self):
        return time.time() - self.start

    def __enter__(self):
        return self

    def __exit__(self):
        print("Elapsed: {}".format(current_time()))


with timer() as t:
    time.sleep(1)
    time.sleep(1)

# Out [ ]: Elapsed: 2.006608009338379
```

- Автоматическое открытие и закрытие сокета

## Дескрипторы

- Стандартный пример

``` python
import time

class ImportantValue:
    def __init__(self, amount):
        self.amount = amount

    def __get__(self, obj, obj_type):
        return None

    def __set__(self, obj, value):
        with open('log.txt', 'a') as f:
            f.write(str(time.time()), + ',' \
                + str(value) + "\n")

        self.amount = value

class Account:
    amount = ImportantValue(100)

bobs_accont = Account()
bobs_accont.amount = 120
```

- Реализация декоратора @property

``` python
class Property:
    def __init__(self, getter):
        self.getter = getter

    def __get__(self, obj, obj_type=None):
        if obj is None:
            return self

        return self.getter(obj)
```

- Позволяют переопределять поведение атрибутов при обращении к ним внутри классов

---
---

## Непонятые темы

- Метаклассы
- Отладка и тестирование
