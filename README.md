# HighLoad-YouTube
Технопарк Mail.ru 3 семестр.

## Содержание

* ### [Тема и целевая аудитория](#1)
* ### [Расчет нагрузки](#2)
* ### [Логическая схема](#3)
* ### [Физическая схема](#4)
* ### [Технологии](#5)
* ### [Схема проекта](#6)
* ### [Список серверов](#7)
* ### [Источники](#8)

## 1. <a name="1">Тема и целевая аудитория</a>
**YouTube**  — видеохостинг, предоставляющий пользователям услуги хранения, доставки и показа видео.

### MVP
- Регистрация 
- Загрузка видео
- Просмотр видео
- Комментирование видео

### Целевая аудитория
У [**YouTube**](https://www.globalmediainsight.com/blog/youtube-users-statistics/) более 2,6 миллиардов активных пользователей в месяц.

| **Страна**              | **Количество пользователей в месяц, млн** |
| ----------------------- | ----------------------------------------- |
| India                   | 467                                       |
| USA                     | 240                                       |
| Indonesia               | 127                                       |
| Brazil                  | 107                                       |
| Russia                  | 99                                        |
| Japan                   | 93.8                                      |
| Mexico                  | 74.1                                      |
| Germany                 | 66                                        |
| Pakistan                | 55.7                                      |
| Vietnam                 | 54.2                                      |

## 2. <a name="2">Расчет нагрузки</a>
### Продуктовые метрики
* Месячная аудитория - 2.6 млрд
* Дневная аудитория - 122 млн
* Средний размер хранилища пользователя - 2 Мб (аватарка и данные о пользователе)
* Среднее количество действий пользователя по типам в день
  > [средняя длительность видео на YouTube](https://exlibris.ru/news/statistika-youtube-2019-infografika/#:~:text=%D0%9F%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D0%B8%20%D1%81%D0%BC%D0%BE%D1%82%D1%80%D1%8F%D1%82%20%D0%B2%D0%B8%D0%B4%D0%B5%D0%BE%20%D0%BA%D0%B0%D0%B6%D0%B4%D1%8B%D0%B9%20%D0%B4%D0%B5%D0%BD%D1%8C&text=%D0%92%20%D1%81%D1%80%D0%B5%D0%B4%D0%BD%D0%B5%D0%BC%20%D0%BD%D0%B0%20%D0%BA%D0%B0%D0%B6%D0%B4%D0%BE%D0%B3%D0%BE%20%D1%87%D0%B5%D0%BB%D0%BE%D0%B2%D0%B5%D0%BA%D0%B0,%D0%BF%D0%BE%D1%8D%D1%82%D0%BE%D0%BC%D1%83%20%D1%81%D1%80%D0%B5%D0%B4%D0%BD%D0%B8%D0%B5%20%D0%BF%D0%BE%D0%BA%D0%B0%D0%B7%D0%B0%D1%82%D0%B5%D0%BB%D0%B8%20%D1%82%D0%B0%D0%BA%D0%B8%D0%B5%20%D0%B2%D0%BF%D0%B5%D1%87%D0%B0%D1%82%D0%BB%D1%8F%D1%8E%D1%89%D0%B8%D0%B5.) 8,4 минуты
  
  >[пользователи в стреднем ставят](https://tubularlabs.com/blog/3-metrics-youtube-success/) 4 лайка на 100 видео
  
  получаем что в среднем пользователь смотрит 2 видео в день и около 60 в месяц, отсюда делаем вывод что пользователь ставит в месяц 2 лайка

  > [пользователи в среднем оставляю](https://tubularlabs.com/blog/3-metrics-youtube-success/) 5 комментариев на 1000 видео
  
  получвем что в среднем пользователь оставляет один комментарий в 3 месяца, округлим до 1 комментария в месяц

  | **Действие**           | **Среднее количество в месяц** |
  | -----------------------| -------------------------------|
  | Лайк                   | 2                              |
  | Комментарий            | 1                              |

### Технические метрики
#### Размер хранения
* #### Видео
> Каждую минуту на YouTube загружается более  500 часов нового контента.\
> [1 час видео весит 8 Гб.](http://7youtube.ru/news/skolko-vesit-video.html)

За сутки получаем 
> 24 * 500 * 8 = 96 000Гб

За год
> 96 000 * 365 = 34 218 Пб

За пять лет
> 34 218 * 5 = 171 093 Пб

Так как все видео надо хранить минимум в двух экземплярах

> 342 186 Пб


#### Сетевой трафик
> В среднем посетитель проводит  на YouTube 14 минут и 21 секунду  каждый день.
* #### Просмотр ежедневно
> 14 минут и 21 секунду = 861 секунда.

> 122 млн * 861 = 105 042 млн секунд = 4 377 млн часов просматривается в течении суток.

[1 час видео весит 8 Гб](http://7youtube.ru/news/skolko-vesit-video.html)

> 4 377 млн часов * 8 Гб = 35 016 млн Гб за сутки

> 35 016 /  (24 * 60 * 60) = 35 016 / 86 400 = 405.2 млн Гб в секунду

* #### Загрузка видео

> 24 * 60 * 500 = 720 000 часов видео загружается ежедневно

> 720 000 * 8 = 5.76 млн Гб видео загружается ежедненво

> 5.76 / 86 400 = 66.6 тыс Гб в секуну 

#### RPS в разбивке по типам запросов
Пользователи выбирают видео для просмотра тремя способами
1. С главной страницы: home page -> video
2. Через рекомендации: home page -> recommendation -> video
3. Через поиск:        home page -> search -> video

Мы получаем что в среднем это три запроса на поиск видео

> 2 видео просмотренных пользователем * 3 запроса * 122 млн DAU = 732 млн запросов в сутки\
> 732 млн / (24 * 60 * 60) = 8472 rps

[пользователи в стреднем ставят](https://tubularlabs.com/blog/3-metrics-youtube-success/) 4 лайка на 100 видео
>  122 млн * 4% = 4.88 млн лайков в день\
>  4.88 млн / (24 * 60 * 60) = 56 rps

[пользователи в среднем оставляю](https://tubularlabs.com/blog/3-metrics-youtube-success/) 5 комментариев на 1000 видео
> 122 млн * 0.5% = 0.61 млн коментариев в день\
> 0.61 млн / (24 * 60 * 60) = 7 rps

Чтобы загрузить видео необходимо сделать 4 запроса.\
Каждую минуту на YouTube загружается более  500 часов нового контента.\
Средняя длительность видео 8.4 минуты.

> 500 * 60 / 8.4 = 3571 видео в минуту ставится на загрузку\
> 3571 * 60 * 24 = 5142240 видео pf сутки ставится на загрузку\
> 5.14 млн * 4 запроса = 20.56 млн запрос в сутки\
> 20.56 млн / (24 * 60 * 60) = 237 rps

4 377 млн часов просматривается в течении суток.
> 4 377 млн / (24 * 60 * 60) = 50 659 часов видео в секнду

| **Действие**           | **RPS** |
| -----------------------| --------|
| Поиск видео            | 8472    |
| Лайки                  | 56      |
| Комментарии            | 7       |
|Загрузка видео          | 237     |
|Просмотр                |50 659 часов в секнду|

## 3. <a name="3">Логическая схема</a>
![](https://github.com/yutfut/HighLoad-YouTube/blob/master/image/db.jpg)

## 4. <a name="4">Физическая схема</a>
* ### Хранение сессий пользователей
Для хранения сессий будем использовать in-memory Redis. Благодаря тому, что Redis является in-memory базой данных, то доступ к определенной записи будет практически равен доступу к оперативной памяти. Помимо свой быстроты Redis поддерживает неблокирующую master-slave репликацию из коробки.
* ### Хранение видео
По типу хранения видео можно разделить на категории:
1. HDD
2. SSD

Изначально все видео будут загружаться на HDD, но те видео которые будут иметь популярность, будем копировать на SSD, чтобы отдавать быстрее, когда популярность будет проходить они будут удаляться с SSD.
* ### Профили, лайки, комментарии
Данные, для которых необходима надежность и не нужен столь быстрый доступ(профили, комментарии, лайки) будем хранить в Postgresql. Для повышения доступности и надеждности сервиса будем использовать технологию шардирования и в разных шардах будем хранить информацию о разных сущностях проекта.

## 5. <a name="5">Технологии</a>
|технология    |область примерения|мотивационная часть|
|--------------|------------------|-------------------|
|js, html, css|Frontend|набор технологий наиболее популярный на рынке, поэтому для него всегда можно найти разработчиков.                   |
|React|Библиотека Frontend|Ускорит процесс разработки.|
|Go|Backend|Быстрый, компилируемый, обладает удобный параллелизм, а также он прост в освоении командой разработки.|
|GRPC|Backend||
|C/C++|Backend|Обеспечить максимальную скорость в самых нагруженных частях проекта.|
|Redis|Хранение сессий|In-memory БД позволяет обеспечить высокую скорость на чтение и запись.|
|Postgresql|Хранение пользователей, комментариев, лайков|Обладает хорошей функциональностью и поддержкой.|
|Nginx|Web-server Reverse proxy|Быстрый, прост в найстройке и использовании.|
|GitLab CI|Система контроля версий.|Линтеры, юнит-тесты, end to end тесты, selenium|
|Kubernetes|Deploy||
## 6. <a name="6">Схема проекта</a>

![](https://github.com/yutfut/HighLoad-YouTube/blob/master/image/HL_1.jpg)



