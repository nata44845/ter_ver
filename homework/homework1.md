## Урок 1. Расчет вероятности случайных событий

### Задание 1.

Из колоды в 52 карты извлекаются случайным образом 4 карты. a) Найти вероятность того, что все карты – крести. б) Найти вероятность, что среди 4-х карт окажется хотя бы один туз.

a)Найти вероятность того, что все карты – крести.
В колоде 52/4=13 карт одной масти.

P=13/52*12/51*11/50*10/49=0.002641=2.64%
P=combinations(13,4)/combinations(52,4)=0.002641=2.64%

б) б) Найти вероятность, что среди 4-х карт окажется хотя бы один туз.
В колоде 4 туза. Выбираем комбинации для 1,2,3,4 тузов

n1=combinations(4,1)*combinations(48,3)
n2=combinations(4,2)*combinations(48,2)
n3=combinations(4,1)*combinations(48,1)
n4=combinations(4,4)
P=(n1+n2+n3+n4)/combinations(52,4)=0.28126=28.13%

Вариант вытянуть 0 тузов, отнимаем от 1 комбинации без тузов

P=1-combinations(48,4)/combinations(52,4)=0.28126=28.13%

### Задание 2.

На входной двери подъезда установлен кодовый замок, содержащий десять кнопок с цифрами от 0 до 9. Код содержит три цифры, которые нужно нажать одновременно. Какова вероятность того, что человек, не знающий код, откроет дверь с первой попытки?

P=1/combinations(10,3)=0.0083333=0.833%

### Задание 3.

В ящике имеется 15 деталей, из которых 9 окрашены. Рабочий случайным образом извлекает 3 детали. Какова вероятность того, что все извлеченные детали окрашены?

P=9/15*8/14*7/13=0.1846153=18.46%
P=combinations(9,3)/combinations(15,3)=0.1846153=18.46%


### Задание 4.

В лотерее 100 билетов. Из них 2 выигрышных. Какова вероятность того, что 2 приобретенных билета окажутся выигрышными?

P=2/100*1/99=0.000202=0.0202%
P=combinations(2,2)*combinations(98,0)/combinations(100,2)=0.0202%