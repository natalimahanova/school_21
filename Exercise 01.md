### Exercise 01. Transforming JSON to CSV

- Turn-in directory: `ex01/`.
- Files to turn in: `filter.jq`, `json_to_csv.sh`, `hh.csv`.
- Allowed functions: jq.

In the previous exercise, you received a JSON file. Although it is a popular format for APIs, it is inconvenient for actual data analysis. Therefore, you will need to convert it into a CSV file, which is more convenient.

Write a shell script called `json_to_csv.sh` that:
- executes jq with a filter written in a separate file `filter.jq`;
- filters the following 5 columns corresponding to the vacancies: "id," "created_at," "name," "has_test," and "alternate_url";
- save the result to the CSV file `hh.csv`.

See the example below:

![1](misc/images/1.png)

The CSV file must have headers in the first row.

Your script must be executable. The interpreter to use is `/bin/sh`.

Place the filter file that converts JSON to CSV, as well as the result of the conversion, in the `ex01` folder in the `src` directory of your repository.


## Заметки

Создать два файла:

filter.jq - фильтр для jq, который выбирает нужные поля

json_to_csv.sh - shell-скрипт, который применяет фильтр

hh.csv - результат преобразования

A, (B | C) = "сделай A, затем сделай B и передай результат в C"

A, B | C = "сделай A и B, затем весь результат передай в C"

["headers"],           # 1. Вывести заголовки
(                     # 2. Начало группы
  .items[] |          #    Взять каждый элемент массива items
  [.id, .name, ...]   #    Создать для него массив полей
)                     # Конец группы
| @csv                # Применить @csv к РЕЗУЛЬТАТУ группы


1. Создать ["headers"] → передать дальше
2. Для каждого .items[] создать массив → собрать все массивы
3. Объединить результат шага 1 и шага 2
4. Применить @csv ко всему

#### Если бы было иначе, то есть неправильно, то получилось бы так

["headers"],
.items[] | 
[.id, .name, ...]
| @csv

1. Создать ["headers"] и развернуть .items[] → странный смешанный поток
2. Применить [.id, .name, ...] к КАЖДОМУ элементу потока
3. Применить @csv

#### Визуализация Скобки есть
Вход: {items: [{id:1}, {id:2}]}

Шаг 1: ["headers"] → ["id", "name"]
Шаг 2: (.items[] | [.id]) → [1], [2]
Шаг 3: Объединить: ["id", "name"], [1], [2]
Шаг 4: @csv → "id,name"\n"1"\n"2"

#### Визуализация скобок нет
Вход: {items: [{id:1}, {id:2}]}

Шаг 1: ["headers"], .items[] → ["id","name"], {id:1}, {id:2}
Шаг 2: | [.id] → ОШИБКА! У ["id","name"] нет поля .id!


#### Пример

# Правильно: вывести 1, затем 2+3
1, (2 + 3)
# Результат: 1, 5

# Неправильно: вывести 1 и 2, затем сложить с 3
1, 2 + 3
# Результат: 1, 2, 3? Нет! Это: (1, 2) + 3 = 4, 5
# Потому что + применяется к (1,2) и 3

####  Пример в jq
# Хотим: взять .items, отфильтровать, выбрать поля
.items[] | select(.salary > 100000) | [.name, .salary]

# Альтернатива со скобками (менее читаемо):
(.items[] | select(.salary > 100000)) | [.name, .salary]


###  Объяснение для файла .sh

# Проверяем, установлен ли jq
if ! command -v jq &> /dev/null; then

Проверка наличия программы jq:

command -v jq - проверяет, доступна ли команда jq в системе

&> /dev/null - перенаправляет весь вывод (stdout и stderr) в /dev/null (в никуда)

! - если команда НЕ выполнена успешно (jq не найден)
