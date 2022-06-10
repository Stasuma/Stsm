# Stsm
Производственная


import scipy
from scipy.optimize import linprog
import numpy as np

#ввод размерности матрицы
a=int(input('Видов товаров:'))
b=int(input('Видов материалов:'))

data=[]#ввод значений матрицы
for i in range(b): 
    data.append([])
    for j in range(a):
        data[i].append(float(input('Расход материала на товар: ')))
data1=np.array(data)#делаем матрицу удобнее для восприятия пользователем
data2=data1.transpose()
print('Матрица значений:')
print(data2)

price=[]#ввод цены товаров
for i in range(a):
    price.append(float(input('Цена товара (с минусом):')))
print('Цены товаров')
print(price)

quantity=[]#ввод количества материалов на склад
for i in range(b):
    quantity.append(float(input('Кол-во материала на складе:')))
print('Кол-во материалов на складе')
print(quantity)

def function(f):#формируем функцию
    print('Целевая функция в формульном виде')
    func = []
    x = 1
    for i in range(a):
        func1 = [abs(f[i]), '*x', x]
        #к каждому значению строки цены применяем модуль так как они с -
        #и добавляем к нему значение x
        x=x+1
        func.append("".join(map(str,func1)))#убираем кавычки у значений
    print("+".join(map(str,func)))#ставим между значения знак +
function(price)

def optimal_value(p, d, q):#находим оптимальное значение лин прог
    ov=linprog(p, d, q, method = 'interior-point')
    print('Оптимальное значение целевой функции:', abs(ov.fun))
    print('При x:',ov.x)
optimal_value(price, data, quantity)


def simplex_method(p, d, q):#находим оптимальное значение симплекс методом
    sm=linprog(p, d, q, method = 'simplex')
    print('Оптимальное значение целевой функции(симплекс):', abs(sm.fun))
    print('При x:',sm.x)

xy=int(input('Решить симплекс-методом?(введите 1-если да, введите 2 - если нет)'))#опциональный симплекс-метод
if xy==1:
    simplex_method(price, data, quantity)
elif xy==2:
    print('Конец')
