# Лабораторная работа № 6 Интеграция рекламных сервисов в интерактивное приложение.
Отчет по лабораторной работе #6 выполнила:
- Додонова Елена Игоревна
- РИ-300002
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

## Цель работы
создание интерактивного приложения с рейтинговой системой пользователя и интеграция игровых сервисов в готовое приложение.

## Задание 1
### Используя видео-материалы практических работ 1-5 повторить реализацию приведенного ниже функционала:

– 1 Практическая работа «Интеграция баннерной рекламы»

– 2 Практическая работа «Интеграция видеорекламы»

– 3 Практическая работа «Показ видеорекламы пользователю за вознаграждение»

– 4 Практическая работа «Создание внутриигрового магазина»

– 5 Практическая работа «Система антиблокировки рекламы»

### – 1 Практическая работа «Интеграция баннерной рекламы»
Ход работы:
1) На платформе Yandex Game подключим возможность монетизации.

![image (15)](https://user-images.githubusercontent.com/90499063/208471304-4b1d11b1-eb6f-4627-9086-902835dc4eef.png)

2) Создадим RTB-блок.

![image (16)](https://user-images.githubusercontent.com/90499063/208471829-729d0612-3b79-4705-8174-783d193e5b86.png)

![image (17)](https://user-images.githubusercontent.com/90499063/208472116-3468bbb5-c998-46d1-bb68-ecfaa9264f4b.png)

![image (18)](https://user-images.githubusercontent.com/90499063/208472466-48b0b2f1-5ebd-4b4c-8efa-9c32741ccbd6.png)

3) Настроим проект для интеграции с рекламой. Для этого полученный номер RTB-блока добавим в ячейку баннерной статистической рекламы. Поставим галочку для отображения рекламы внутри игры.

![image (19)](https://user-images.githubusercontent.com/90499063/208472514-f6ec37bd-ee6b-48b2-9493-68cad76ff3b0.png)

![image (20)](https://user-images.githubusercontent.com/90499063/208472576-14fbf9f6-011d-4d3f-b920-37d8b90e2d30.png)

4) Сделаем билд проекта и загрузим на Yandex Game. При запуске и между сессиями можно наблюдать рекламу.

![image (21)](https://user-images.githubusercontent.com/90499063/208472859-3c86348d-a939-4832-8de9-69f40f19ac26.png)

![image (22)](https://user-images.githubusercontent.com/90499063/208473355-9c78baa5-4d34-4758-bfd9-d8486c75ca48.png)


### – 2 Практическая работа «Интеграция видеорекламы»
Ход работы:
1) Добавим в скрипты CheckConnectYG и DragonPicker строчку кода, благодаря которой будет проигрываться реклама во время игры.

```
YandexGame.RewVideoShow(0);
```

2) Во всех объектах YandexGame на сценах отмечаем, что при просмотре рекламы пользователем, игра будет останавливаться на паузу.

![image (23)](https://user-images.githubusercontent.com/90499063/208473495-ec4280ce-e52e-4fee-9c9b-86d9a0a7d4a9.png)

3) Делаем билд, загружаем на платформу и видим наличие видеорекламы после проигрыша.

https://user-images.githubusercontent.com/90499063/208473755-ba1fa9ee-63b7-4ff8-af3d-1783278bc7cc.mp4


### – 3 Практическая работа «Показ видеорекламы пользователю за вознаграждение»
Ход работы:

1) Реализуем показ рекламы за вознаграждение. Создадим и напишем новый скрипт и подключим его к YandexManager, этот скрипт будет отвечать за показ рекламы за вознаграждение.

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using YG;

public class ADReward : MonoBehaviour
{
    private void OnEnable() => YandexGame.CloseVideoEvent += Rewarded;
    private void OnDisable() => YandexGame.CloseVideoEvent += Rewarded;

    void Rewarded(int id)
    {
        if(id == 1)
        {
            Debug.Log("Пользователь получил награду");
        }
        else
        {
            Debug.Log("Пользователь остался без награды");
        }
    }
    
    public void OpenAD()
    {
        YandexGame.RewVideoShow(Random.Range(0,2));
    }
}
```

2) Создадим и настроим кнопку, чтоб пользователь мог при нажатии на нее посмотреть рекламу за вознаграждение.

![image (24)](https://user-images.githubusercontent.com/90499063/208474207-8bd14012-9f72-4ecc-a16e-7de5d0c7d5b0.png)

3) Сделаем билд и загрузим на Yandex Игры. После просмотра рекламы пользователю дается вознаграждение.

![image (26)](https://user-images.githubusercontent.com/90499063/208474308-4561221a-640a-4f2a-a07f-480aba6a3e6c.png)

https://user-images.githubusercontent.com/90499063/208474903-92a0928c-687d-49f3-a73f-fc2bae61cf01.mp4


### – 4 Практическая работа «Создание внутриигрового магазина»
Ход работы:
1) Добавляем на сцену префаб OnePurchase из YandexGame, с помощью которого пользователь сможет делать внутриигровые покупки.

![image (27)](https://user-images.githubusercontent.com/90499063/208475187-62a9b129-b960-4d0a-9523-98868ef92743.png)

2) Настраиваем покупку алмазов на Yandex Игры и в юнити подключаем ID

![unnamed](https://user-images.githubusercontent.com/90499063/208475324-b3489de4-cc21-42ab-ac19-10c4f506f6f8.png)

![image (28)](https://user-images.githubusercontent.com/90499063/208475387-cc956ed0-aa45-484d-8b0b-e03c72c92d07.png)

3) Делаем билд, загружаем, и при нажатии на покупку алмазов у нас возникает ошибка, так как пока в черновике мы не можем совершить покупку.

![image (29)](https://user-images.githubusercontent.com/90499063/208475440-3bd03598-7e5a-4e31-af51-926503a54983.png)


### – 5 Практическая работа «Система антиблокировки рекламы»
Ход работы:
1) Ставим галочку на проверку адблока

![image (30)](https://user-images.githubusercontent.com/90499063/208475730-5ca17e30-1aa5-4f2b-b738-893ceae60561.png)

## Задание 2
### Добавить в приложение интерфейс для вывода статуса наличия игрока в сети (онлайн или офлайн).
Ход работы:
1) Напишем код в скрипт CheckConnectYG

```
[SerializeField] private TextMeshProUGUI userStatusOnOff;

public void CheckSDK()
{
    if (YandexGame.auth)
    {
        userStatusOnOff.text = "Online";
        Debug.Log("User authorization ok");
    }
    else
    {
        Debug.Log("User not authorization");
        YandexGame.AuthDialog();
    }
}
```

2) Создадим текст и подключим к нему код выше через Yandex Manager. В итоге у нас будет меняться текст при подключении с Offline на Online.

https://user-images.githubusercontent.com/90499063/208475815-82d7cbde-e34b-467e-9ea6-e23a38fa5446.mp4

## Задание 3
### Предложить наиболее подходящий на ваш взгляд способ монетизации игры D.Picker. Дать развернутый ответ с комментариями.
Ход работы:
Я считаю, что самые лучшие возможности монетизации игры такие:

- дополнительная жизнь / удвоение алмазов за просмотр рекламы после проигрыша;
 
- различные плюшки за просмотр видеорекламы (ограниченное количество просмотров в день);

- покупка скинов на персонажа и объекты в игре;

- возможность платной подписки для отключения рекламы;

- баннеры, но ими увлекаться не стоит, поскольку начинают быстро надоедать пользователю.

## Выводы
В ходе данной лабораторной работы мы создали систему покупок, работающую через валюту Яндекс Деньги.
Создали баннерную рекламу, отображающуюся внизу экрана.
Также создали систему вознаграждения за просмотр видеорекламы.
Добавили систему антиблокировки рекламы.

