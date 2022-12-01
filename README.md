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
Познакомиться с программными средствами для создания системы машинного обучения и ее интеграции в Unity.


## Задание 1
### Пошагово выполнить каждый пункт раздела "ход работы" с описанием и примерами реализации задач
# Ход работы:

Схема логичечких элементов

![image](https://user-images.githubusercontent.com/113997426/204098771-3307add2-be8b-4682-b8da-4081687329f1.png)

1) Создала новый проект в Unity, добавила пустой объект 'perceptron'

![2022-11-26 (40)](https://user-images.githubusercontent.com/113997426/204098615-610781fa-1fcc-45d4-8e51-02c175d7536f.png)

2) к объекту 'perceptron' прикрепила файл со скриптом, добавила код

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[System.Serializable]
public class TrainingSet
{
	public double[] input;
	public double output;
}

public class Perceptron : MonoBehaviour {

	public TrainingSet[] ts;
	double[] weights = {0,0};
	double bias = 0;
	double totalError = 0;

	double DotProductBias(double[] v1, double[] v2) 
	{
		if (v1 == null || v2 == null)
			return -1;
	 
		if (v1.Length != v2.Length)
			return -1;
	 
		double d = 0;
		for (int x = 0; x < v1.Length; x++)
		{
			d += v1[x] * v2[x];
		}

		d += bias;
	 
		return d;
	}

	double CalcOutput(int i)
	{
		double dp = DotProductBias(weights,ts[i].input);
		if(dp > 0) return(1);
		return (0);
	}

	void InitialiseWeights()
	{
		for(int i = 0; i < weights.Length; i++)
		{
			weights[i] = Random.Range(-1.0f,1.0f);
		}
		bias = Random.Range(-1.0f,1.0f);
	}

	void UpdateWeights(int j)
	{
		double error = ts[j].output - CalcOutput(j);
		totalError += Mathf.Abs((float)error);
		for(int i = 0; i < weights.Length; i++)
		{			
			weights[i] = weights[i] + error*ts[j].input[i]; 
		}
		bias += error;
	}

	double CalcOutput(double i1, double i2)
	{
		double[] inp = new double[] {i1, i2};
		double dp = DotProductBias(weights,inp);
		if(dp > 0) return(1);
		return (0);
	}

	void Train(int epochs)
	{
		InitialiseWeights();
		
		for(int e = 0; e < epochs; e++)
		{
			totalError = 0;
			for(int t = 0; t < ts.Length; t++)
			{
				UpdateWeights(t);
				Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
			}
			Debug.Log("TOTAL ERROR: " + totalError);
		}
	}

	void Start () {
		Train(8);
		Debug.Log("Test 0 0: " + CalcOutput(0,0));
		Debug.Log("Test 0 1: " + CalcOutput(0,1));
		Debug.Log("Test 1 0: " + CalcOutput(1,0));
		Debug.Log("Test 1 1: " + CalcOutput(1,1));		
	}
	
	void Update () {
		
	}
}
```

3) Настроила массив Ts, добавив в него логический элемент OR

![2022-11-26 (42)](https://user-images.githubusercontent.com/113997426/204099276-c74b3bc5-7e82-4555-ade4-9d7a023878e5.png)

4) Запустила работу программы и получила следующие результаты:

![2022-11-26 (43)](https://user-images.githubusercontent.com/113997426/204099521-5ee7036a-4c9f-479d-995b-592415d01145.png)
![2022-11-26 (44)](https://user-images.githubusercontent.com/113997426/204099526-c213bd67-1ede-4bb2-b89c-f8120471305e.png)
![2022-11-26 (45)](https://user-images.githubusercontent.com/113997426/204099530-e9e97293-cafa-4ee7-af42-4994114f7fca.png)
![2022-11-26 (46)](https://user-images.githubusercontent.com/113997426/204099535-ef0de24a-a1b8-461b-bb0b-e1a2ba3392af.png)

За 8 итераций метода Train перцептрон успевает обучиться и количество ошибок TotalError снижается до 0. Успех подтверждается с помощью результатов теста методом CalcOutput в последних четырех строчках

5) В массив Ts Добавила данные для логической функции AND, запустила работу программы

![2022-11-26 (53)](https://user-images.githubusercontent.com/113997426/204100963-22a98dcc-af58-427a-9522-b2a954f12f49.png)
![2022-11-26 (54)](https://user-images.githubusercontent.com/113997426/204100967-d0adaa87-bd0d-4025-b561-e142a083514f.png)
![2022-11-26 (55)](https://user-images.githubusercontent.com/113997426/204100971-cb4fecdf-c07b-48a4-9f7d-68f696bfd194.png)
![2022-11-26 (56)](https://user-images.githubusercontent.com/113997426/204100975-ac0ee24b-2204-44ad-938e-8ef768c9eae9.png)
 
 В данном примере перцептрон успевает обучиться за 8 итераций, однако делает это медленне, чем при OR логическом элементе.
 Однако, при повторных испытаниях оказывается, что 8-ми итераций иногда не хватает, поэтому с запасом делаю 16
 
 ![2022-11-26 (58)](https://user-images.githubusercontent.com/113997426/204101334-9cf6775b-03a5-4af7-aebb-3421ea96d76e.png)

```
Train(16);
```

6) Сменила данные в Ts на логику NAND, запустила программу

![2022-11-26 (59)](https://user-images.githubusercontent.com/113997426/204101489-b4411e41-5b41-49f8-b76b-6e19797e7449.png)

Перцептрон обучается и работает корректно

7) В массив Ts внесла логический элемент XOR

![2022-11-26 (60)](https://user-images.githubusercontent.com/113997426/204101675-b6f42cd3-2694-4773-817c-57c1265f8d01.png)
![2022-11-26 (61)](https://user-images.githubusercontent.com/113997426/204101680-60ba5c62-f11a-43b2-80e2-dde5cfa4cf1a.png)
 
 Видим, что количество ошибок в течение работы программы только возрастает, и повторные проверки с увеличением количества итераций эту тенденцию не меняют. 
 Перцептрон не обучается и работает некорректно

## Задание 2


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
