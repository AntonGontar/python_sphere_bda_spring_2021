# A. Минимальная подстрока

На вход вашей программе подается две строки: _s_1_ и _s_2_. Напишите программу, которая найдет минимальную подстроку в строке _s_1_, которая содержит все символы из _s_2_. Гарантируется, что все символы в строке _s_2_ уникальны и их не менее одного.

## Формат входных данных

В первой строке задается _s_1_, во второй - _s_2_.

## Формат результата

Выведите подстроку, которая удовлетворяет условию.

Если такой подстроки нет, ничего выводить не надо.

Если таких подстрок несколько, выведите первую (чье начало ближе к началу строки).

## Примеры

Входные данные
```
radioactive
aio
```
Результат работы
```
ioa
```

Входные данные
```
radioactive
aiob
```
Результат работы
```
```

Входные данные
```
ccc
aiob
```
Результат работы
```
```

Входные данные
```
flag glaf flga
glaf
```
Результат работы
```
flag
```

## Примечания

Можно завести два индекса, указывающие на начало и конец подстроки. Далее эти два индекса можно поочередно двигать в поиске подходящей минимальной подстроки.

В данном задании удобно использовать генератор подходящих пар индексов.

## Решение
    A.py

# B. Грань будущего

При обкачивании некоторого сайта нередко сталкиваются с проблемой, что страница может не скачаться с первого раза. Это может быть вызвано разными причинами, например, проблемами с сетью или слишком частой обкачкой (сайт вас таймаутит).

Напишите декоратор `@retry(check, n_attempts=5)`, где `check` - функция, которая проверяет корректность результат (возвращаемое значение) декорируемой функции, `n_attempts` - число попыток, сколько раз нужно вызвать декорируемую функцию пока не будет получен корректный результат. Если число попыток `None` или не положительно, то число попыток считается бесконечным.

В случае, если число попыток исчерпано, нужно бросить исключение: `RuntimeError('Expired number of retries')`.

## Примеры

Входные данные
```python
@retry(check=bool)
def func(a):
    return a

try:
    print(func(3))
except RuntimeError as e:
    print(e)
```
Результат работы
```
3
```

Входные данные
```python
gen = iter(range(100))

@retry(check=lambda x: x >= 5, n_attempts=6)
def func():
    return next(gen, -1)

try:
    print(func())
except RuntimeError as e:
    print(e)
```
Результат работы
```
5
```

Входные данные
```python
gen = iter(range(2))

@retry(check=lambda x: x >= 5, n_attempts=6)
def func():
    return next(gen, -1)

try:
    print(func())
except RuntimeError as e:
    print(e)
```
Результат работы
```
Expired number of retries
```

Входные данные
```python
gen = iter(range(1000))

@retry(check=lambda x: x < 0, n_attempts=-1)
def func():
    return next(gen, -1)

try:
    print(func())
except RuntimeError as e:
    print(e)
```
Результат работы
```
-1
```

## Примечания

Не забудьте перекрыть имя декорируемой функции через декоратор из модуля `functools`.

Функция, обернутая в декоратор, должна возвращать то же значение, что и функция без декоратора. В задаче НЕ гарантируется, что оборачиваемая функция не принимает на вход аргументов.

## Решение
    B.py

# C. Отладка сортировки слиянием

Напишите генератор-функцию `merge_sort`, которая принимает на вход итерируемый объект и возвращает промежуточные частично отсортированные списки. Первое значение итератора соответствует последовательно отсортированным двойкам, второе - четверкам и т.д. Последнее значение - полностью отсортированный список.

## Примеры

Входные данные
```python
for item in merge_sort([5, 3, 4, 6]):
    print(item)
```
Результат работы
```
[3, 5, 4, 6]
[3, 4, 5, 6]
```

Входные данные
```python
for item in merge_sort(reversed(range(14))):
    print(item)
```
Результат работы
```
[12, 13, 10, 11, 8, 9, 6, 7, 4, 5, 2, 3, 0, 1]
[10, 11, 12, 13, 6, 7, 8, 9, 2, 3, 4, 5, 0, 1]
[6, 7, 8, 9, 10, 11, 12, 13, 0, 1, 2, 3, 4, 5]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13]
```

## Примечания

**Запрещается** хранить все промежуточные значения списка. В любой момент можно хранить только 2 списка: состояние списка на предыдущем и на текущем состояниях.

**Запрещается** использовать встроенные сортировки: `sorted`, `list.sort` и т.п.

## Решение
    C.py
