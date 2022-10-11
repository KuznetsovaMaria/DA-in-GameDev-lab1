# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнила:
- Кузнецова Мария Сергеевна
- РИ210932
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | # | 20 |
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

Создала проект в Unity, подгрузила предоставленные файлы, создала C# скрипт. В скрипте реализовала программу

```c#

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

```

Настроила объект и дополнительные параметры в проекте Unity
При запуске программы на консоль выводятся числа из таблицы, проигрывается нужное аудиосопровождение для каждой строки

![2022-10-11 (5)](https://user-images.githubusercontent.com/113997426/195041103-b9a09189-85f8-4547-832c-5baada3fddd0.png)

При повторном запуске программы в PyCharm числа меняются, проект в Unity срабатывает корректно

![2022-10-11 (7)](https://user-images.githubusercontent.com/113997426/195041458-457fff7b-24c3-4419-8c96-77f3cdb70d17.png)

![2022-10-11 (9)](https://user-images.githubusercontent.com/113997426/195041864-27b9ed51-677d-40d7-88a4-ed8751b28fda.png)



## Задание 2

Ход работы:


## Задание 3


## Выводы
В ходе лабораторной работы #2, следуя инструкциям и методическим указаниям, ознакомилась с программными средствами для организации передачи данных между инструментами google, python & unity

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
