# Практическое занятие №2. Менеджеры пакетов

Разобраться, что представляет собой менеджер пакетов, как устроен пакет, как читать версии стандарта semver. Привести примеры программ, в которых имеется встроенный пакетный менеджер.

## Задача 1

Вывести служебную информацию о пакете matplotlib (Python). Разобрать основные элементы содержимого файла со служебной информацией из пакета. Как получить пакет без менеджера пакетов, прямо из репозитория?

### C менеджером пакетов

```
pip show matplotlib
```

![image](https://github.com/user-attachments/assets/b3792aa5-750a-4633-9c8c-9bc25980987c)

### Без менеджера пакетов

```
git clone https://github.com/matplotlib/matplotlib.git
```
```
cd matplotlib
```
```
pip install -r requirements.txt
```
```
python setup.py install
```

## Задача 2

Вывести служебную информацию о пакете express (JavaScript). Разобрать основные элементы содержимого файла со служебной информацией из пакета. Как получить пакет без менеджера пакетов, прямо из репозитория?

### C менеджером пакетов

```
npm show express
```

![image](https://github.com/user-attachments/assets/3cd2ed73-0495-4b50-af14-4991c7cbcc20)


### Без менеджера пакетов

```
git clone https://github.com/expressjs/express.git
```
```
cd express
```
```
npm install
```
```
npm link
```

## Задача 3

Сформировать graphviz-код и получить изображения зависимостей matplotlib и express.

### Зависимости для matplotlib (Python)

```
digraph G {
    "matplotlib" -> "numpy";
    "matplotlib" -> "pyparsing";
    "matplotlib" -> "cycler";
    "matplotlib" -> "pillow";
    "matplotlib" -> "kiwisolver";
    "matplotlib" -> "python-dateutil";

    "cycler" -> "six";
    "python-dateutil" -> "six";
}
```

![graph](https://github.com/user-attachments/assets/9a4919df-eb9f-4296-81a0-479ff4ab2ba9)

### Зависимости для express (JavaScript)

```
digraph G {
    "express" -> "accepts";
    "express" -> "array-flatten";
    "express" -> "body-parser";
    "express" -> "content-disposition";
    "express" -> "content-type";
    "express" -> "cookie";
    "express" -> "cookie-signature";
    "express" -> "debug";
    "express" -> "depd";
    "express" -> "encodeurl";
    "express" -> "escape-html";
    "express" -> "etag";
    "express" -> "finalhandler";
    "express" -> "fresh";
    "express" -> "merge-descriptors";
    "express" -> "methods";
    "express" -> "on-finished";
    "express" -> "parseurl";
    "express" -> "path-to-regexp";
    "express" -> "proxy-addr";
    "express" -> "qs";
    "express" -> "range-parser";
    "express" -> "safe-buffer";
    "express" -> "send";
    "express" -> "serve-static";
    "express" -> "setprototypeof";
    "express" -> "statuses";
    "express" -> "type-is";
    "express" -> "utils-merge";
    "express" -> "vary";

    "accepts" -> "mime-types";
    "accepts" -> "negotiator";
    "body-parser" -> "bytes";
    "body-parser" -> "http-errors";
    "body-parser" -> "iconv-lite";
    "body-parser" -> "on-finished";
    "body-parser" -> "qs";
    "body-parser" -> "raw-body";
}
```

![graph (1)](https://github.com/user-attachments/assets/f64a0da3-f60d-48eb-b97c-d188973059cd)
## Задача 4

Изучить основы программирования в ограничениях. Установить MiniZinc, разобраться с основами его синтаксиса и работы в IDE.

Решить на MiniZinc задачу о счастливых билетах. Добавить ограничение на то, что все цифры билета должны быть различными (подсказка: используйте all_different). Найти минимальное решение для суммы 3 цифр.
```
include "globals.mzn";

array[1..6] of var 0..9: digits;
constraint all_different(digits);

var int: sum_first = sum(digits[1..3]);
var int: sum_last = sum(digits[4..6]);

constraint sum_first = sum_last;
solve minimize sum_first;
```
## Задача 5

Решить на MiniZinc задачу о зависимостях пакетов для рисунка, приведенного ниже.

![pubgrub](https://github.com/user-attachments/assets/99f96aca-9308-4396-967f-2d2416c47663)
```
set of int: MenuVersion = {100, 110, 120, 130, 150};
set of int: DropdownVersion = {230, 220, 210, 200, 180};
set of int: IconsVersion = {100, 200};

var MenuVersion: menu;
var DropdownVersion: dropdown;
var IconsVersion: icons;

constraint if menu >= 110 then dropdown >= 200 else dropdown = 180 endif;

constraint if dropdown <= 200 /\ dropdown > 180 then icons = 200 else icons = 100 endif;

solve satisfy;
```
