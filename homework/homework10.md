## Урок 10. Дисперсионный анализ

Провести дисперсионный анализ для определения того, есть ли различия среднего роста среди взрослых футболистов, хоккеистов и штангистов. 

Даны значения роста в трех группах случайно выбранных спортсменов: 

Футболисты: 173, 175, 180, 178, 177, 185, 183, 182. 

Хоккеисты: 177, 179, 180, 188, 177, 172, 171, 184, 180. 

Штангисты: 172, 173, 169, 177, 166, 180, 178, 177, 172, 166, 170. 

Данная промежуточная аттестация оценивается по системе "зачет" / "не зачет". 

"Зачет" ставится, если Слушатель успешно выполнил задание. "Незачет" ставится, если Слушатель не выполнил задание. 

Критерии оценивания: 1 - Слушатель провел дисперсионный анализ для определения того, есть ли различия среднего роста среди взрослых футболистов, хоккеистов и штангистов.

import numpy as np
import pandas as pd
from scipy import stats
from statsmodels.stats.multicomp import pairwise_tukeyhsd
import pandas as pd

f = np.array([173, 175, 180, 178, 177, 185, 183, 182])
h = np.array([177, 179, 180, 188, 177, 172, 171, 184, 180])
w = np.array([172, 173, 169, 177, 166, 180, 178, 177, 172, 166, 170])


print(f'Нормальность тест Шапиро-Уилка f {stats.shapiro(f)[1]>0.05}')
print(f'Нормальность тест Шапиро-Уилка h {stats.shapiro(h)[1]>0.05}')
print(f'Нормальность тест Шапиро-Уилка w {stats.shapiro(w)[1]>0.05}')

print(f'Однородность дисперсий Бартлетт f-h-w {stats.bartlett(f,h,w)[1]>0.05}')

print(f'Гипотеза 0 (m1=m2=m3) Крускал-Уоллес {stats.kruskal(f, h, w)[1]>0.05}') 

df = pd.DataFrame({"score": [173, 175, 180, 178, 177, 185, 183, 182, 
                             177, 179, 180, 188, 177, 172, 171, 184, 180,
                             172, 173, 169, 177, 166, 180, 178, 177, 172, 166, 170],
                   "group": np.repeat(["football", "hockey", "weightlifters"], repeats = [8, 9, 11])})
df


tukey = pairwise_tukeyhsd(df["score"], df["group"], alpha = 0.05)
print(tukey)

print(stats.tukey_hsd(f,h,w))

Нормальность тест Шапиро-Уилка f True
Нормальность тест Шапиро-Уилка h True
Нормальность тест Шапиро-Уилка w True
Однородность дисперсий Бартлетт f-h-w True

Гипотеза 0 (m1=m2=m3) False
     Multiple Comparison of Means - Tukey HSD, FWER=0.05      
==============================================================
 group1      group2    meandiff p-adj   lower    upper  reject
--------------------------------------------------------------
football        hockey  -0.4583  0.979  -6.2732  5.3566  False
football weightlifters  -6.3977 0.0219 -11.9583 -0.8372   True
  hockey weightlifters  -5.9394 0.0284 -11.3181 -0.5607   True
--------------------------------------------------------------
Tukey's HSD Pairwise Group Comparisons (95.0% Confidence Interval)
Comparison  Statistic  p-value  Lower CI  Upper CI
 (0 - 1)      0.458     0.979    -5.357     6.273
 (0 - 2)      6.398     0.022     0.837    11.958
 (1 - 0)     -0.458     0.979    -6.273     5.357
 (1 - 2)      5.939     0.028     0.561    11.318
 (2 - 0)     -6.398     0.022   -11.958    -0.837
 (2 - 1)     -5.939     0.028   -11.318    -0.561

Между группой football и hockey нет различий в среднем росте, тогда как между группами football и weightlifters, а так же между группами hockey и weightlifters есть различия в среднем росте.