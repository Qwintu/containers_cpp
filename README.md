# s21_containers

## Реализация части библиотеки s21_containers.h.
<br>

### Introduction

В рамках данного проекта надо написать собственную библиотеку, реализующую стандартные контейнерные классы языка С++: `array` (массив) и `vector` (вектор). Реализации должны предоставлять весь набор стандартных методов и атрибутов для работы с элементами, проверкой заполненности контейнера и итерирования. В качестве дополнительного задания предлагается реализовать еще несколько не так часто используемых, но отличающихся деталями реализации контейнерных классов из контейнерной библиотеки C++.

## Chapter I

- Программа должна быть разработана на языке C++ стандарта C++17 с использованием компилятора gcc
- Код программы должен находиться в папке src
- При написании кода необходимо придерживаться Google Style
- Обязательно использовать итераторы
- Классы обязательно должны быть шаблонными
- Классы должны быть реализованы внутри пространства имен `s21`
- Подготовить полное покрытие unit-тестами методов контейнерных классов c помощью библиотеки GTest
- Запрещено копирование реализации стандартной библиотеки шаблонов (STL)
- Необходимо соблюсти логику работы стандартной библиотеки шаблонов (STL) (в части проверок, работы с памятью и поведения в нештатных ситуациях)

### Part 1. Реализация библиотеки s21_containers.h

Необходимо реализовать классы библиотеки `s21_containers.h` (спецификации указаны в соответствующих разделах материалов, см. пункт **"Основные контейнеры"**). \
Список классов: `array` (массив), `vector` (вектор).
- Оформить решение в виде заголовочного файла `s21_containers.h`, который включает в себя другие заголовочные файлы с реализациями необходимых контейнеров (`s21_array.h`, `s21_vector.h`)
- Предусмотреть Makefile для тестов написанной библиотеки (с целями clean, test)
- За основу стоит рассматривать классическую реализацию контейнеров, но конечный выбор реализаций остается свободным. За исключением списка - его необходимо реализовывать через структуру списка, а не через массив.
- Предусмотреть Makefile для тестов написанной библиотеки (с целями clean, test)
- За основу стоит рассматривать классическую реализацию контейнеров, но конечный выбор алгоритма остается свободным

### Part 2. Дополнительно. Реализация методов `insert_many`

Необходимо дополнить классы соответствующими методами, согласно таблице:

| Modifiers      | Definition                                      | Containers |
|----------------|-------------------------------------------------| -------------------------------------------|
| `iterator insert_many(const_iterator pos, Args&&... args)`          | inserts new elements into the container directly before `pos`  | Vector |
| `void insert_many_back(Args&&... args)`          | appends new elements to the end of the container  | Vector |


Обратите внимание, что в качестве аргументов передаются уже созданные элементы соответствующего контейнера, которые необходимо вставить в этот контейнер.

*Подсказка 1*: обратите внимание, что каждый из этих методов использует конструкцию Args&&... args - Parameter pack. Эта конструкция позволяет передавать переменное число параметров в функцию или метод. То есть при вызове метода, определенного как `iterator insert_many(const_iterator pos, Args&&... args)`, можно написать как `insert_many(pos, arg1, arg2)`, так и `insert_many(pos, arg1, arg2, arg3)`.
<br><br>

## Chapter II

### Information

Каждый вид контейнеров должен предоставить пользователю следующие методы:

- стандартные конструкторы (конструктор по умолчанию, конструктор копирования, конструктор перемещения, конструктор со списком инициализации, см. материалы);

- методы доступа к элементам контейнера (например, осуществление доступа к элементу с индексом i);

- методы проверки наполненности контейнера (например, количество элементов в контейнере, проверка на пустоту контейнера);

- методы изменения контейнера (удаление и добавление новых элементов, очистка контейнера);

- методы для работы с итератором контейнера.

Итераторы обеспечивают доступ к элементам контейнера. Для каждого контейнера конкретный тип итератора будет отличаться. Это связано с различным видом организации наборов объектов в контейнерных классах, а также с фактической реализацией контейнера. Итераторы реализуются в таком виде, чтобы они работали схожим образом с указателем на элемент массива языка Си. Именно такой подход через использование итераторов и позволяет взаимодействовать с любыми контейнерами одинаковым образом. Контейнеры предоставляют через методы `begin()` и `end()` итераторы, которые указывают на первый и следующий после последнего элементы контейнера соответственно.

Над итератором `iter` определены следующие операции:

- `*iter`: получение элемента, на который указывает итератор;

- `++iter`: перемещение итератора вперед для обращения к следующему элементу;

- `--iter`: перемещение итератора назад для обращения к предыдущему элементу;

- `iter1 == iter2`: два итератора равны, если они указывают на один и тот же элемент;

- `iter1 != iter2`: два итератора не равны, если они указывают на разные элементы.

Помимо особой организации объектов и предоставления необходимых методов, реализация контейнерных классов требует шаблонизации объектов. 

