## Урок 9. Линейная регрессия Логистическая регрессия

### Задание 1
Даны значения величины заработной платы заемщиков банка (zp) и значения их поведенческого кредитного скоринга (ks): zp = [35, 45, 190, 200, 40, 70, 54, 150, 120, 110], ks = [401, 574, 874, 919, 459, 739, 653, 902, 746, 832]. Используя математические операции, посчитать коэффициенты линейной регрессии, приняв за X заработную плату (то есть, zp - признак), а за y - значения скорингового балла (то есть, ks - целевая переменная). Произвести расчет как с использованием intercept, так и без.

import numpy as np
from scipy import stats
from matplotlib import pyplot as plt

zp = np.array([35, 45, 190, 200, 40, 70, 54, 150, 120, 110])
ks = np.array([401, 574, 874, 919, 459, 739, 653, 902, 746, 832])

print(f'Шапиро-Уилка zp {stats.shapiro(zp)[1]>0.05}')
print(f'Шапиро-Уилка ks {stats.shapiro(ks)[1]>0.05}')

plt.scatter(zp, ks)
R = np.corrcoef(zp, ks)[0, 1] ** 2 
print(f'Корреляция {R}')

b1 = (np.mean(zp * ks) - np.mean(zp) * np.mean(ks)) / (np.mean(zp ** 2) - np.mean(zp) ** 2)
b0 = np.mean(ks) - b1 * np.mean(zp)
print(f'ks = {round(b0,4)}+{round(b1,4)}*zp') 
ks1 = b0 + b1 * zp 
plt.scatter(zp, ks1)
plt.plot(zp, ks1)


Шапиро-Уилка zp True
Шапиро-Уилка ks True
Корреляция 0.7876386635293684
ks = 444.1774+2.6205*zp


#Интерсепт
from sklearn.linear_model import LinearRegression

model = LinearRegression()
zp1 = zp.reshape((-1,1))

regres = model.fit(zp1,ks)

print(f'ks = {round(regres.intercept_,4)}+{round(regres.coef_[0],4)}*zp')

### Задание 2
Посчитать коэффициент линейной регрессии при заработной плате (zp), используя градиентный спуск (без intercept).

B0 = 1
B1 = 1
n = len(zp)
alpha = 5e-5
for i in range(10 ** 6 * 2):
    B1 -= alpha * (2 / n) * np.sum((B0 + B1 * zp - ks) * zp)
    B0 -= alpha * (2 / n) * np.sum((B0 + B1 * zp - ks))
    if i % 50000 == 0:
        print(B0, B1)
print(f'ks = {round(B0,4)}+{round(B1,4)}*zp') 
ks = 444.1774+2.6205*zp



### Задание 3
Произвести вычисления как в пункте 2, но с вычислением intercept. Учесть, что изменение коэффициентов должно производиться на каждом шаге одновременно (то есть изменение одного коэффициента не должно влиять на изменение другого во время одной итерации).

def mse_ab(a, b, x, y):
    return np.sum(((a + b * x)-y) ** 2) / len(x)

def mse_pa(a, b, x, y): 
    return 2 * np.sum((a + b * x) - y) / len(x)

def mse_pb(a, b, x, y):
    return 2 * np.sum(((a + b * x) - y) * x) / len(x)


alpha = 3e-5
b = 1
a = 1
mseab_min = mse_ab(a, b, zp, ks)
i_min = 1
b_min = b
a_min = a 
for i in range(10**6*2):
    a -= alpha * mse_pa(a, b, zp, ks)
    b -= alpha * mse_pb(a, b, zp, ks)
    if i % 10000 == 0:
        print(f'Итерация = {i}, a = {a}, b = {b}, mse = {mse_ab(a, b, zp, ks)}'.format(i = i, a = a, b = b))

print(f'ks = {round(a,4)}+{round(b,4)}*zp') 

ks = 444.1774+2.6205*zp