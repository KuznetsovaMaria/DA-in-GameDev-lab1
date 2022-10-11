# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнила:
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
Создала и настроила новый проект в google console

![2022-10-10 (2)](https://user-images.githubusercontent.com/113997426/195037462-124d406b-b698-457c-bf23-1333fcc8fec9.png)

![2022-10-10 (3)](https://user-images.githubusercontent.com/113997426/195037532-8f04b564-0741-4e28-8477-efa93a585929.png)

Создала новую таблицу в google sheets и настроила доступ

![2022-10-10 (6)](https://user-images.githubusercontent.com/113997426/195037725-63d2e7c1-2cfc-45ba-8376-384ccb76e489.png)

В pycharm написала программу, связала с таблицей. В результате запуска программы полученные значения переносятся в таблицу

![2022-10-10 (9)](https://user-images.githubusercontent.com/113997426/195038041-f006339c-ccdf-4aa0-9dd8-56284ccacfeb.png)

![2022-10-10 (11)](https://user-images.githubusercontent.com/113997426/195038067-322e5abc-6d8e-4c75-a7be-c53e588875db.png)

Создала проект в Unity, подгрузила предоставленные файлы, создала C# скрипт. В скрипет реализовала программу


using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Networking;
using SimpleJSON;


public class NewBehaviourScript : MonoBehaviour
{
    public AudioClip GoodSpeak;

    public AudioClip NormalSpeak;

    public AudioClip BadSpeak;

    private AudioSource SelectAudio;

    private Dictionary<string, float> dataSet = new Dictionary<string, float>();

    private bool statusStart = false;

    private int i = 1;


    // Start is called before the first frame update
    void Start()
    {
        StartCoroutine(GoogleSheets());
    }

    // Update is called once per frame
    void Update()
    {
        if (dataSet["Mon_" + i.ToString()] <= 10 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioGood());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] > 10 & dataSet["Mon_" + i.ToString()] < 100 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioNormal());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] >= 100 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioBad());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }
    }

    IEnumerator GoogleSheets()
    {
        UnityWebRequest currentResp = UnityWebRequest.Get("https://sheets.googleapis.com/v4/spreadsheets/1b-WZ4ZITn-KI7LYBrqpWbNIMmcfSebJlSIr2Nl1JeYA/values/Лист1?key=AIzaSyBZnRELGhNuTzdA7vZUyrebhqM_htng3wk");
        yield return currentResp.SendWebRequest();
        string rawResp = currentResp.downloadHandler.text;
        var rawJSON = JSON.Parse(rawResp);
        foreach (var itemRawJSON in rawJSON["values"])
        {
            var parseJSON = JSON.Parse(itemRawJSON.ToString());
            var selectRow = parseJSON[0].AsStringList;
            dataSet.Add("Mon_" + selectRow[0], float.Parse(selectRow[2]));
        }
        //Debug.Log(dataSet["Mon_1"]);


    }

    IEnumerator PlaySelectAudioGood()
    {
        statusStart = true;
        SelectAudio = GetComponent<AudioSource>();
        SelectAudio.clip = GoodSpeak;
        SelectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioNormal()
    {
        statusStart = true;
        SelectAudio = GetComponent<AudioSource>();
        SelectAudio.clip = NormalSpeak;
        SelectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioBad()
    {
        statusStart = true;
        SelectAudio = GetComponent<AudioSource>();
        SelectAudio.clip = BadSpeak;
        SelectAudio.Play();
        yield return new WaitForSeconds(4);
        statusStart = false;
        i++;
    }

}


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



## Задание 3
Какова роль параметра Lr?

Параметр Lr влияет на наклон прямой графика, на a, b
![2022-09-27 (14)](https://user-images.githubusercontent.com/113997426/192572233-89d0f263-c866-4e2d-b54f-9218a368dd80.png)


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
