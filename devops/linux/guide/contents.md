# Linux. Справочник
## Содержание
- Об авторе
- Посвящение
- Благодарности к первому изданию (2005 г.)
- Благодарности ко второму изданию (2015 г.) 15
- От издательства 1б
- Введение 18
- На кого рассчитана эта книга 19
- 0 втором издании 21
- Основные соглашения 23
1. Общие сведения о работе с командной строкой 25
    - Файлы, и ничего, кроме файлов 25
    - Максимальная длина имени файла 2б
    - Регистр символов в именах файлов 27
    - Специальные символы в именах файлов 28
    - Символы групповых операций 31
    - Специальные файлы, на которые влияет командная строка 36
    - Если на экране слишком много информации, сделайте перезагрузку 39
    - Выводы 40
1. [Основные команды](basic-commands.md)
    - [Вывод списка файлов и каталогов]()
    - [Вывод содержимого произвольного каталога]()
    - [Использование символов групповых операций при определении содержимого каталога]()
    - [Просмотр содержимого подкаталогов]()
    - [Вывод содержимого каталога в один столбец]()
    - [Вывод содержимого каталога с запятыми в качестве разделителей]()
    - [Отображение скрытых файлов и каталогов]()
    - [Отображение информации о типах файлов]()
    - [Отображение информации в цвете]()
    - [Информация о правах доступа и владельцах файпов]()
    - [Вывод информации в обратном порядке]()
    - [Сортировка по дате и времени]()
    - [Сортировка содержимого каталога по размеру файлов]()
    - [Представление размеров файлов в кило-, мега- и гигабайтах]()
    - [Определение пути к текущему каталогу]()
    - [Переход в другой каталог]()
    - [Переход в рабочий каталог]()
    - [Переход в предыдущий каталог]()
    - [Выводы]()
1. Создание и уничтожение 65
    - Изменение сведений о времени 65
    - Установка произвольного времени для файла 67
    - Создание нового пустого файла 69
    - Создание нового каталога 69
    - Создание нового каталога и необходимых подкаталогов 70
    - Копирование файлов 71
    - Копирование файлов с использованием символов групповых операцийКопирование файлов 73
    - Вывод подробной информации о копировании файлов 75
    - Как предотвратить копирование поверх важных файлов 7б
    - Копирование каталогов 78
    - Использование команды ср для создания резервных копий 79
    - Перемещение и переименование файлов 80
    - Переименование файлов и каталогов 83
    - Как Linux хранит файлы 84
    - Создание ссылки на другой файл или каталог 86
    - Удаление файлов 93
    - Удаление нескольких файлов с помощью символов групповых операций 95
    - Как предотвратить удаление важных файлов 95
    - Удаление пустого каталога 96
    - Удаление файлов и каталогов, содержащих данные 97
    - Удаление проблемных файлов 98
    - Выводы 100
1. Получение информации о командах 101
    - Получение информации о командах с помощью команды глап 102
    - Получение кратких сведений о команде 105
    - Поиск команды по выполняемым ею действиям 106
    - Просмотр страницы справочной системы, посвященной конкретной команде 109
    - Получение информации о командах с помощью info 111
    - Навигация в системе 1по 112
    - Определение путей к исполняемым, исходным файлам и страницам справочного руководства 115
    - Сведения об экземпляре программы для запуска 116
    - Выяснение интерпретации команды 118
    - Выводы 120
1. Объединение команд 121
    - Последовательное вы полиение нескольких команд 121
    - Выполнение команды при условии успешного завершения предыдущих 123
    - Выполнение команды при условии, что предыдущая завершилась с ошибкой 126
    - Использование выходных данных одной команды при вызове другой 127
    - Входной и выходной потоки 128
    - Передача выходных данных одной команды на вход другой 130
    - Перенаправление выходных данных в файл 132
    - Как предотвратить перезапись файла при перенаправлении 133
    - Перенаправление выходных данных и запись их в конец файла 134
    - Использование содержимого файпа в качестве входных данных 135
    - Сочетание перенаправления ввода и вывода 136
    - Одновременный вывод данных в файл и поток stdout 138
    - Выводы 140
1. Просмотр содержимого файлов (как правило, текстовых) 141
    - Распознавание типа файла 141
    - Вывод содержимого файла в stdout 144
    - Конкатенация файлов и вывод их в 1оо 145
    - Конкатенация файлов и запись результатов в другой файл 146
    - Конкатенация файлов и нумерация строк 147
    - Постраничный вывод текста 148
    - Поиск с помощью программы постраничного просмотра 151
    - Редактирование файлов, отображаемых средствами постраничного просмотра 152
    - Просмотр первых десяти строк файла 153
    - Просмотр первых десяти строк нескольких файлов 154
    - Просмотр произвольного числа строк из файлов 155
    - Просмотр указанного количества байтов из начала файла 155
    - Просмотр последних десяти строк файла 158
    - Просмотр последних десяти строк нескольких файлов 158
    - Просмотр произвольного числа последних строк из файлов 160
    - Просмотр обновляемых строк в конце файла 161
    - Выводы 162
1. Обработка текстовых файлов с помощью фильтров .... 165
    - Подсчет количества слов, строк и символов в файле 166
    - Количество строк в файле 168
    - Выбор отдельного столбца данных в размеченном файле 170
    - Сортировка содержимого файла 173
    - Числовая сортировка содержимого файла 175
    - Удаление из файла строк-дубликатов 177
    - Замена заданных символов другими 180
    - Замена повторяющихся символов одним экземпляром 181
    - Удаление заданных символов 183
    - Преобразование текста в файле 187
    - Вывод на печать конкретных полей из файла 192
    - Выводы 196
1. Владельцы файлов и права доступа 199
    - Вход под другим именем 199
    - Вход под другим именем и с другими переменными окружения 200
    - Вход под именем пользователя гоо 202
    - Вход под именем пользователя гоо с его переменными окружения 202
    - Изменение групп для файлов и каталогов 203
    - Рекурсивное изменение принадлежности каталога группе 205
    - Изменение владельцев файлов и каталогов 206
    - Изменение владельца и группы для файлов и каталогов 208
    - Общие сведения о правах доступа 210
    - Изменения прав доступа к файлам и каталогам с использованием символьных обозначений 213
    - Изменения прав доступа к файлам и каталогам с использованием числовых обозначений 215
    - Рекурсивное изменение прав 219
    - Установка и сброс параметра Ы1 221
    - Установка и сброс признака sgid 224
    - Установка и сброс признака "sticky ЫС 227
    - Выводы 230
Глава 9. Архивирование и сжатие данных 231
    - Архивирование и сжатие файлов посредством программы zip 233
    - Повышение уровня сжатия с помощью программы zip 235
    - Архивирование и сжатие файлов конкретного типа в каталогах и подкаталогах 237
    - Защита zip-архивов паролем 239
    - Разархивирование файпов 241
    - Проверка файлов, предназначенных для разархивирования 242
    - Сжатие файлов посредством программы gzip 243
    - Рекурсивная обработка файпов посредством программы gzip 244
    - Распаковка файпов, сжатых с помощью программы gzip 246
    - Проверка файлов, предназначенных для распаковки с помощью программы gunzip 247
    - Сжатие файпов посредством программы bzip2 248
    - Распаковка файлов, сжатых с помощью программы bzip2 249
    - Проверка файлов, предназначенных для разархивирования с помощью программы bunzip2 250
    - Архивирование файлов с помощью программы аг 250
    - Создание архивов и сжатие файлов посредством программ аг и gzip 252
    - Проверка файлов, предназначенных для распаковки и разархивирования 254
    - Распаковка и разархивирование файлов 256
    - Выводы 257
1. Поиск файлов, каталогов, слов и фраз 259
    - Поиск в базе имен файпов 260
    - Поиск в базе имен файлов без учета регистра 262
    - Обновление базы, используемой программой locate 263
    - Поиск фрагментов текстового файла 265
    - Общие сведения о шаблонах поиска 266
    - Рекурсивный поиск фрагментов текста в файлах 271
    - Поиск слов и выделение результатов 272
    - Поиск фрагментов текста в файлах без учета регистра 273
    - Поиск слов в файлах 274
    - Отображение номеров строк, в которых слово содержится в файле 275
    - Поиск слов в выходных данных других команд 275
    - Просмотр контекста для слов, имеющихся в файлах 278
    - Отображение строк, не содержащих указанных слов 280
    - Отображение списка файлов, содержащих указанное слово 281
    - Поиск слов среди результатов 282
    - Выводы 283
1. Команда find 285
    - Поиск файлов по имени 285
    - Поиск файлов по имени владельца 287
    - Поиск файлов по размеру 288
    - Поиск файлов по типу 291
    - Поиск файлов по времени 292
    - Отображение результатов при выполнении всех выражений (АШ) 295
    - Отображение результатов при выполнении любого из выражений (ОВ) 296
    - Отображение результатов, если выражение не выполняется ООТ) 299
    - Выполнение действий над каждым найденным файлом 301
    - Более эффективный поиск файлов 304
    - Поиск файлов, имена которых содержат пробелы 307
    - Выводы 308
1. Оболочка 309
    - Просмотр списка предыстории 309
    - Повторное выполнение последней команды 311
    - Вызов предыдущей команды путем указания ее номера 313
    - Вызов предыдущей команды путем указания строки символов 313
    - Поиск и выполнение предыдущей команды 315
    - Отображение псевдонимов команд 320
    - Просмотр псевдонима конкретной команды 321
    - Создание нового временного псевдонима 321
    - Создание нового постоянно действующего псевдонима 322
    - Удаление всех псевдонимов 324
    - Создание новой временной функции 325
    - Создание новой постоянной функции 327
    - Вывод на экран списка всех функций 330
    - Удаление функции 331
    - Когда следует использовать псевдоним, а когда функцию? 332
    - Выводы 334
    - Глава 13. Контроль использования системных ресурсов 337
    - Выяснение того, как долго работает компьютер 338
    - Вывод информации о процессах, выполняемых в системе 338
    - Просмотр дерева процессов 341
    - Отображение процессов, принадлежащих конкретному пользователю 343
    - Завершение выполняющегося процесса 343
    - Отображение динамически обновляемого списка выполняющихся процессов 347
    - Получение списка открытых файлов 349
    - Отображение файлов, открытых конкретным пользователем 351
    - Получение списка пользователей для конкретного файла 353
    - Отображение сведений о процессах, соответствующих конкретной программе 354
    - Отображение информации о6 оперативной памяти системы 356
    - Отображение информации об использовании дискового пространства 357
    - Определение размера области, занятой содержимым каталога 359
    - Ограничение вывода общим размером пространства, занятого каталогом 361
    - Выводы 361
1. Инсталляция программного обеспечения 363
    - Инсталляция программных пакетов в АРМ-системах 364
    - Удаление программных пакетов из RPM-систем 366
    - Инсталляция зависимых программных пакетов в RPM-системах 366
    - Удаление зависимых программных пакетов из RPM-систем 370
    - Обновление программных пакетов в RPM-системах 371
    - Поиск пакетов, готовых к копированию на RPM-системы 373
    - Инсталляция программных пакетов в системе Debian 374
    - Удаление программных пакетов из системы Debian 376
    - Инсталляция зависимых пакетов в системе Debian 377
    - Удаление зависимых пакетов из системы Debian 381
    - Обновление зависимых пакетов в системе Debian 383
    - Поиск пакетов, доступных для копирования в систему Debian 385
    - Удаление ненужных инсталляционных пакетов из системы Debian 388
    - Устранение проблем с помощью системы АРТ 389
    - Выводы 391
1. Сетевое взаимодействие 393
    - Определение состояния сетевых интерфейсов 394
    - Проверка способности компьютера принимать запросы 397
    - Контроль прохождения пакета между двумя узлами 399
    - Выполнение DNS-преобразования 401
    - Настройка сетевого интерфейса 405
    - Получение информации о состоянии сетевого интерфейса беспроводнойсвязи 408
    - Настройка сетевого интерфейса беспроводнойсвязи 411
    - Получение адресов средствами ОНСР 412
    - Активизация сетевого соединения 414
    - Перевод сетевого интерфейса в неактивизированноесостояние 416
    - Отображение таблицы маршрутизации 417
    - Внесение изменений в таблицу маршрутизации 420
    - Устранение проблем, связанных с сетевым взаимодействием 424
    - Выводы 428
1. Работав сети 431
    - Организация защищенного взаимодействия с другим компьютером 431
    - Защищенная регистрация на другой машине без использования пароля 435
    - Защищенная система РТР 439
    - Защищенное копирование файлов между узлами сети 441
    - Защищенная передача файлов и создание резервных копий 443
    - Копирование файлов из веб 451
    - Копирование веб-сайтов 457
    - Указание последовательностей имен копируемых файлов 459
    - Выводы 461
1. Предметный указатель


[Дальше](.md)

[README.md](../../README.md)