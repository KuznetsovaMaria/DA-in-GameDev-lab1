# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #5 выполнила:
- Кузнецова Мария Сергеевна
- РИ210932
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | # | 20 |

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

Применить ml агент для моделирования экономической системы игры в Unity и ознакомиться с графиками работы ml агента

## Задание 1
### Пошагово выполнить каждый пункт раздела "ход работы" с описанием и примерами реализации задач
# Ход работы:

1) Скачала необходимые для выполнения лабораторной работы файлы; создала новый проект в unity, подключила нужные packages

![2022-12-02 (13)](https://user-images.githubusercontent.com/113997426/205327725-3bc4e14c-2695-4a5d-b209-c7b2207a3996.png)

2) В anaconda prompt создала и запустила виртуальное пространство

```
conda create -n MLAgent python=3.6.13
conda activate MLAgent
```

3) Установила необходимые библиотеки

```
pip install mlagents==0.28.0
pip install torch~=1.7.1 -f https://download.pytorch.org/whl/torch_stable.html
```

4) Начала обучение ml агента

![2022-12-02 (5)](https://user-images.githubusercontent.com/113997426/205328787-98e1e80c-e6d2-45aa-889f-91acb17581d6.png)

5) Проверила сохранение результатов в папку

![2022-12-02 (14)](https://user-images.githubusercontent.com/113997426/205328897-c99ed900-aeb5-4445-bd48-ab0988a99b35.png)

6) Установила и запустила TensorBoard

![2022-12-02 (15)](https://user-images.githubusercontent.com/113997426/205329095-27152e8b-f150-42b1-9a58-57912b6f348e.png)

7) Получила следующие графики

![2022-12-02 (16)](https://user-images.githubusercontent.com/113997426/205329163-de28ff3e-bac1-4e43-8f4c-4bab33a90809.png)

![2022-12-02 (17)](https://user-images.githubusercontent.com/113997426/205329339-1a88b6e4-44e2-4396-9a90-1dfd42df6e80.png)

![2022-12-02 (18)](https://user-images.githubusercontent.com/113997426/205329355-887a33f6-dfba-4257-9af5-15484d4a66d9.png)


## Задание 2 Измените параметры файла. yaml-агента и определить какие параметры и как влияют на обучение модели.

Буду изменять параметры yaml-файла и отслеживать графики, уделяя особое вгимание cumulative reward

1) Изменила batch_size: 1024 на 2000, график следующий

![2022-12-02 (20)](https://user-images.githubusercontent.com/113997426/205330348-a455ee3d-281e-4340-b20e-65a82d147cf8.png)

Кривая Economic в конце стала стремиться вниз

2) Изменила lambd: 0.95 на 0.9

![2022-12-02 (22)](https://user-images.githubusercontent.com/113997426/205334728-34a8394e-8d26-4a2f-b8e0-9b108f333271.png)
В этот раз график reard вышел на плато 

3) Изменила epsilon: 0.2 на 0.1 

![2022-12-02 (28)](https://user-images.githubusercontent.com/113997426/205340481-858ec470-9a5b-4735-a5c2-879cabe58425.png)
График показал резкий и значительный рост параметра

4) А если в обратную сторону? epsilon: 0.3

![2022-12-02 (26)](https://user-images.githubusercontent.com/113997426/205339010-bda58d1d-51ac-4281-93e2-332d816ca5e9.png)
График практически не изменил форму, только значения

5) Изменила num_epoch: 3 на 10

![2022-12-02 (30)](https://user-images.githubusercontent.com/113997426/205342209-c9421e4e-d10f-419d-8158-26fa243063bd.png)
График на каждой итерации стабильно равен 1

6) Изменила buffer_size: 10240 на 50240

![2022-12-02 (34)](https://user-images.githubusercontent.com/113997426/205344174-5b549204-c9a2-4519-a72b-2216798609fe.png)
График в начале резко пошел вниз, но затем начал, хоть и медленнее, но расти



## Задание 3


## Выводы




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
