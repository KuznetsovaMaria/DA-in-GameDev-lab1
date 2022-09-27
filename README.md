# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнила:
- Кузнецова Мария Сергеевна
- РИ210932
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
Ознакомиться с основными операторами зыка Python на примере реализации линейной регрессии.


## Задание 1
### Пошагово выполнить каждый пункт раздела "ход работы" с описанием и примерами реализации задач
# Ход работы:
В google colab написать код, сохранить на диске, запустить

![2022-09-27](https://user-images.githubusercontent.com/113997426/192476720-bdab6f9e-f230-4b15-bf48-d06bc91c0627.png)
![2022-09-27 (1)](https://user-images.githubusercontent.com/113997426/192476784-992599a8-ffd9-450c-8759-f09ddd46bf7a.png)

В unity создать скрипт на c#, в нем написать код, прикрепить скрипт к объекту, запустить
![2022-09-27 (5)](https://user-images.githubusercontent.com/113997426/192563101-dc4bea6e-4dd3-4f85-8e84-3d580b4669c7.png)
![2022-09-27 (2)](https://user-images.githubusercontent.com/113997426/192485162-ff2a1642-3249-4aad-8267-86a9c77352b4.png)

## Задание 2

Ход работы:
- Произвести подготовку данных для работы с алгоритмом линейной регрессии. 10 видов данных были установлены случайным образом, и данные находились в линейной зависимости. Данные преобразуются в формат массива, чтобы их можно было вычислить напрямую при использовании умножения и сложения.

```py

In [ ]:
#Import the required modules, numpy for calculation, and Matplotlib for drawing
import numpy as np
import matplotlib.pyplot as plt
#This code is for jupyter Notebook only
%matplotlib inline

# define data, and change list to array
x = [3,21,22,34,54,34,55,67,89,99]
x = np.array(x)
y = [2,22,24,65,79,82,55,130,150,199]
y = np.array(y)

#Show the effect of a scatter plot
plt.scatter(x,y)

```

Выполнение:
Подготовка данных
![2022-09-27 (6)](https://user-images.githubusercontent.com/113997426/192563858-c4e07e58-4a18-4b20-aa1d-decdff66a332.png)

- Определите связанные функции. Функция модели: определяет модель линейной регрессии wx+b. Функция потерь: функция потерь среднеквадратичной ошибки. Функция оптимизации: метод градиентного спуска для нахождения частных производных w и b.
![2022-09-27 (7)](https://user-images.githubusercontent.com/113997426/192565762-fc23d18f-8b9b-41f2-a02a-be031c58abcb.png)

Начало итерации
Шаг 1. Инициализация и модель итеративной оптимизации
![2022-09-27 (8)](https://user-images.githubusercontent.com/113997426/192567675-10904894-4b2e-4049-88a7-8381ce78b79d.png)

Шаг 2. На второй итерации отображаются значения параметров, значения потерь и эффекты визуализации после итерации
![2022-09-27 (9)](https://user-images.githubusercontent.com/113997426/192568113-1ca8f9bd-03ee-4047-a1c7-c5ae78493453.png)

Шаг 3. Третья итерация показывает значения параметров, значения потерь и визуализацию после итерации
![2022-09-27 (10)](https://user-images.githubusercontent.com/113997426/192568574-71c572d3-ed95-497e-ba34-dcd0fd6a8371.png)

Шаг 4. На четвертой итерации отображаются значения параметров, значения потерь и эффекты визуализации
![2022-09-27 (11)](https://user-images.githubusercontent.com/113997426/192568919-5d20c9ff-3e18-4eb7-8787-d829dbf238af.png)

Шаг 5. Пятая итерация показывает значение параметра, значение потерь и эффект визуализации после итерации
![2022-09-27 (12)](https://user-images.githubusercontent.com/113997426/192569345-b93e553c-ce05-4cea-be69-84cb0372e0ed.png)

Шаг 6. 10000-я итерация, показывающая значения параметров, потери и визуализацию после итерации
![2022-09-27 (13)](https://user-images.githubusercontent.com/113997426/192570086-79ed7297-81f9-4dc5-9ce4-c7f11c42f11b.png)


Ходу работы следовали:
Код написали, данные подготовили, график построили



Задание 3
Какова роль параметра Lr?

Параметр Lr влияет на наклон прямой графика, на a, b
![2022-09-27 (14)](https://user-images.githubusercontent.com/113997426/192572233-89d0f263-c866-4e2d-b54f-9218a368dd80.png)

```

## Выводы
В ходе лабораторной работы #1 выполнили инструкции по установке и настройке всех необходимых программ. Внимательно ознакомились с задачами и предложенным кодом. Достигли поставленной цели, познакомились с основными операторами зыка Python на примере реализации линейной регрессии. К отчету приложили результаты выполненной работы.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
