## Урок 8. Корреляционный анализ
### Задание 1
Даны значения величины заработной платы заемщиков банка (zp) и значения их поведенческого кредитного скоринга (ks): zp = [35, 45, 190, 200, 40, 70, 54, 150, 120, 110], ks = [401, 574, 874, 919, 459, 739, 653, 902, 746, 832]. Найдите ковариацию этих двух величин с помощью элементарных действий, а затем с помощью функции cov из numpy Полученные значения должны быть равны. Найдите коэффициент корреляции Пирсона с помощью ковариации и среднеквадратичных отклонений двух признаков, а затем с использованием функций из библиотек numpy и pandas.

import numpy as np
import matplotlib.pyplot as plt

zp = np.array([35, 45, 190, 200, 40, 70, 54, 150, 120, 110])
ks = np.array([401, 574, 874, 919, 459, 739, 653, 902, 746, 832])


cov = np.mean(zp*ks) - np.mean(zp)*np.mean(ks)
print(cov,np.cov(zp, ks, ddof=0)[0, 1])

cov_p = cov/(np.std(zp)*np.std(ks))
print(cov_p, np.cov(zp,ks,ddof=0)[0][1]/(np.std(zp,ddof=0)*np.std(ks,ddof=0)))

print(np.corrcoef(zp, ks)[0][1])

plt.scatter(zp, ks)
plt.title(f'r = {round(np.corrcoef(zp, ks)[0][1], 4)}')
plt.xlabel('zp')
plt.ylabel('ks')
plt.show()

9157.839999999997 9157.840000000002
0.8874900920739158 0.8874900920739163
0.8874900920739163

### Задание 2
Измерены значения IQ выборки студентов, обучающихся в местных технических вузах: 131, 125, 115, 122, 131, 115, 107, 99, 125, 111. Известно, что в генеральной совокупности IQ распределен нормально. Найдите доверительный интервал для математического ожидания с надежностью 0.95.

from scipy import stats

x = np.array([131, 125, 115, 122, 131, 115, 107, 99, 125, 111])

n=len(x)
m = np.mean(x)
s = np.std(x,ddof=1)
a = 0.05

z = abs(stats.t.ppf(a/2,n-1))

print(f'[{round(m-z*s/n**0.5,2)};{round(m+z*s/n**0.5,2)}]')

[110.56;125.64]

### Задание 3
Известно, что рост футболистов в сборной распределен нормально с дисперсией генеральной совокупности, равной 25 кв.см. Объем выборки равен 27, среднее выборочное составляет 174.2. Найдите доверительный интервал для математического ожидания с надежностью 0.95.

D=25
s=D**0.5
n=27
m=174.2
a=1-0.95

z = abs(stats.norm.ppf(1-a/2))

print(f'[{round(m-z*s/n**0.5,2)};{round(m+z*s/n**0.5,2)}]')

[172.31;176.09]