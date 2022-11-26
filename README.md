# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #4 выполнила:
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
Познакомиться с программными средствами для создания системы машинного обучения и ее интеграции в Unity.


## Задание 1
### Пошагово выполнить каждый пункт раздела "ход работы" с описанием и примерами реализации задач
# Ход работы:
1) Создала новый проект в Unity, скачала необходимые для выполнения лабораторной работы материалы, добавила ML agent

![2022-11-26 (19)](https://user-images.githubusercontent.com/113997426/204080705-be147cc7-cc84-4a2a-a6d4-2021207a8bbf.png)

2) Активировала новый mlagent 

![2022-11-26 (21)](https://user-images.githubusercontent.com/113997426/204080783-e57f2532-a2bd-4ee5-aec8-0261a86c7cfc.png)

3) Установила torch

![2022-11-26 (23)](https://user-images.githubusercontent.com/113997426/204080854-c3b2502d-7814-4e48-a602-fca5cbef885e.png)

4) Создала сцену с шаром (RollerAgent) и кубом (Target) на плоскости, добавила материалы

![2022-11-26 (25)](https://user-images.githubusercontent.com/113997426/204080945-1391ffb4-ca91-4255-8b0f-18eb8cbb7627.png)

5) Создала и привязала к RollerAgent новый скрипт С#, добавила в него код

```c#

using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Unity.MLAgents;
using Unity.MLAgents.Sensors;
using Unity.MLAgents.Actuators;

public class RollerAgent : Agent
{
    Rigidbody rBody;

    void Start()
    {
        rBody = GetComponent<Rigidbody>();
    }

    public Transform Target;
    public override void OnEpisodeBegin()
    {
        if (this.transform.localPosition.y < 0)
        {
            this.rBody.angularVelocity = Vector3.zero;
            this.rBody.velocity = Vector3.zero;
            this.transform.localPosition = new Vector3(0, 0.5f, 0);
        }

        Target.localPosition = new Vector3(Random.value * 8-4, 0.5f, Random.value * 8-4);
    }
    public override void CollectObservations(VectorSensor sensor)
    {
        sensor.AddObservation(Target.localPosition);
        sensor.AddObservation(this.transform.localPosition);
        sensor.AddObservation(rBody.velocity.x);
        sensor.AddObservation(rBody.velocity.z);
    }
    public float forceMultiplier = 10;

    public override void OnActionReceived(ActionBuffers actionBuffers)
    {
        Vector3 controlSignal = Vector3.zero;
        controlSignal.x = actionBuffers.ContinuousActions[0];
        controlSignal.z = actionBuffers.ContinuousActions[1];
        rBody.AddForce(controlSignal * forceMultiplier);

        float distanceToTarget = Vector3.Distance(this.transform.localPosition, Target.localPosition);

        if(distanceToTarget < 1.42f)
        {
            SetReward(1.0f);
            EndEpisode();
        }
        else if (this.transform.localPosition.y < 0)
        {
            EndEpisode();
        }
    }
}

```

6) Объекту RollerAgent добавила и настроила необходимые компоненты: Rigidbody, Decision Requester, Behavior Parameters

![2022-11-26 (27)](https://user-images.githubusercontent.com/113997426/204082339-fa598236-4990-4879-9aa8-d98803f586db.png)

7) Добавила yaml файл, внесла код

```
behaviors:
  RollerBall:
    trainer_type: ppo
    hyperparameters:
      batch_size: 10
      buffer_size: 100
      learning_rate: 3.0e-4
      beta: 5.0e-4
      epsilon: 0.2
      lambd: 0.99
      num_epoch: 3
      learning_rate_schedule: linear
    network_settings:
      normalize: false
      hidden_units: 128
      num_layers: 2
    reward_signals:
      extrinsic:
        gamma: 0.99
        strength: 1.0
    max_steps: 500000
    time_horizon: 64
    summary_freq: 10000
    
```

8) Запустила работу mlagent 

![2022-11-26 (31)](https://user-images.githubusercontent.com/113997426/204082556-40a8189a-2487-41fa-949b-d250a8da4a23.png)

9) Запустила сцену с 1, 9 и 36 копиями модели

![2022-11-26 (32)](https://user-images.githubusercontent.com/113997426/204082667-cbf3faf1-adf1-4521-a376-6762808ccf54.png)

![2022-11-26 (33)](https://user-images.githubusercontent.com/113997426/204082684-9fed8789-cd35-4e45-acf8-8637e9a9c2d6.png)

![2022-11-26 (34)](https://user-images.githubusercontent.com/113997426/204082691-39990813-694b-4796-b8f7-54fdb89145aa.png)

![2022-11-26 (35)](https://user-images.githubusercontent.com/113997426/204082730-0a65bd55-db55-46f6-b721-698f5908cb4c.png)

10) Настроила модель в behaviour parameters, проверила ее работу

![2022-11-26 (36)](https://user-images.githubusercontent.com/113997426/204082795-0be4c1c8-4fc6-43ee-982c-e68f85361617.png)

![2022-11-26 (37)](https://user-images.githubusercontent.com/113997426/204082820-12ea9474-f6c1-4676-82ee-65efbdca6640.png)

![2022-11-26 (38)](https://user-images.githubusercontent.com/113997426/204082870-61b0c6f7-e875-407b-9372-7edb7d775cbb.png)


## Задание 2


## Задание 3


## Выводы

В ходе лабораторной работы 3 я познакомилась с программными средствами для создания системы машинного обучения и ее интеграции в Unity. Научилась создавать и настраивать mlagent, тренировать нейросеть для реализации программы "охоты" сферы на куб, двигающийся в заданном диапазоне.
Игровой баланс - это уравновешивание игры между восприятием ее как скучной и сложной за счет балансировки всех показателей в игре: силы, времени, пространства и т.д. Системы машинного обучения могут быть использованы для имитации использования игры реальными пользователями и выявления возможных стратегий и, следовательно, существующих недочетов в балансе игры.


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
