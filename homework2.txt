Задание 1.
Вероятность того, что стрелок попадет в мишень, выстрелив один раз, равна 0.8. Стрелок выстрелил 100 раз. Найдите вероятность того, что стрелок попадет в цель ровно 85 раз.

p=0.8
n=100
q=1-p
k=85
P=combinations(n,k)*(p**k)*(q**(n-k)) = 0.04806 = 4.806%

Задание 2.
Вероятность того, что лампочка перегорит в течение первого дня эксплуатации, равна 0.0004. В жилом комплексе после ремонта в один день включили 5000 новых лампочек. Какова вероятность, что ни одна из них не перегорит в первый день? Какова вероятность, что перегорят ровно две?

n=5000
p=0.0004
l=n*p

Какова вероятность, что ни одна из них не перегорит в первый день? 
m=0
P_0=(l**m)/factorial(m)*(2.72**(-l)) = 0.13516 = 13.52%

Какова вероятность, что перегорят ровно две?
m=2
P_2=(l**m)/factorial(m)*(2.72**(-l)) = 0.2703 = 27.03%

Задание 3.
Монету подбросили 144 раза. Какова вероятность, что орел выпадет ровно 70 раз?

n=144
k=70
p=0.5
q=1-p
P=combinations(n,k)*(p**k)*(q**(n-k)) = 0.0628 = 6.28%

Задание 4.
В первом ящике находится 10 мячей, из которых 7 - белые. Во втором ящике - 11 мячей, из которых 9 белых. Из каждого ящика вытаскивают случайным образом по два мяча. Какова вероятность того, что все мячи белые? Какова вероятность того, что ровно два мяча белые? Какова вероятность того, что хотя бы один мяч белый?


Какова вероятность того, что все мячи белые?
P=combinations(7,2)*combinations(9,2)/(combinations(10,2)*combinations(11,2))
= 0.30545 = 30.54%

Какова вероятность того, что ровно два мяча белые?
n1 = combinations(3,2)*combinations(9,2)
n2 = combinations(7,1)*combinations(3,1)*combinations(9,1)*combinations(2,1)
n3 = combinations(7,2)*combinations(2,2)

P=(n1+n2+n3)/(combinations(10,2)*combinations(11,2))=0.2048=20.48%

Какова вероятность того, что хотя бы один мяч белый?

P=1 - combinations(3,2)*combinations(2,2)/(combinations(10,2)*combinations(11,2))
=0.9987 = 99.87%

n_0_0=combinations(7,0)*combinations(3,2)*combinations(9,0)*combinations(2,2)
n_0_1=combinations(7,0)*combinations(3,2)*combinations(9,1)*combinations(2,1)
n_0_2=combinations(7,0)*combinations(3,2)*combinations(9,2)*combinations(2,0)

n_1_0=combinations(7,1)*combinations(3,1)*combinations(9,0)*combinations(2,2)
n_1_1=combinations(7,1)*combinations(3,1)*combinations(9,1)*combinations(2,1)
n_1_2=combinations(7,1)*combinations(3,1)*combinations(9,2)*combinations(2,0)

n_2_0=combinations(7,2)*combinations(3,0)*combinations(9,0)*combinations(2,2)
n_2_1=combinations(7,2)*combinations(3,0)*combinations(9,1)*combinations(2,1)
n_2_2=combinations(7,2)*combinations(3,0)*combinations(9,2)*combinations(2,0)


P=(n_0_1+n_0_2+n_1_0+n_1_1+n_1_2+n_2_0+n_2_1+n_2_2)/(combinations(10,2)*combinations(11,2))
=0.9987=99.87%

