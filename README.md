# avitotech_ml_cup_2024

# Проект: Соревнование от AvitoTech по рекомендации наиболее релевантных рекламных объявлении для пользователей.

### Оглавление

[Описание проекта](#описание-проекта) 

[Этапы проекта](#этапы-проекта)  

[Структура проекта](#структура-проекта)  

[Используемые библиотеки](#используемые-библиотеки) 

[Выводы](#выводы) 

[Заключительные выводы](#заключительные-выводы) 

[Установка и использование](#установка-и-использование)  

### ***Описание проекта***
Разработать модель, которая сможет рекомендовать пользователю наиболее релевантную рекламу на основе реальных данных после анонимизации. 
Модель должна предсказывать вероятность того, что пользователь кликнет на рекламное объявление, исходя из его характеристик и предпочтений. 

Ссылка на соревнование на ods.ai [AvitoTech ML cup 2024](https://ods.ai/competitions/avitotechmlcup2024)

Признаки и доступные данные для проекта.

Данные о взаимодействии Пользователя и рекламной компании (train.parquet и test.parquet)
 |-- platform_id: id платформы (Android, Ios и т.п.)
 |-- user_id: id Пользователя 
 |-- adv_campaign_id: id рекламной компании 
 |-- target: клик / не клик
 |-- banner_code: код баннера
 |-- adv_creative_id: индификатор креатива
 |-- event_date: date Дата показа рекламной кампании пользователю
 |-- is_main: boolean True - показ рекламы был осуществлен с главной страницы

Данные о категориях (categories.parquet)
|-- microcat_id: id микрокатегории 
|-- level_id: id уровня в дереве микрокатегорий
|-- parent_microcat_id: id родительской микрокатегории
|-- logcat_id: id логической категории 
|-- vertical_id: id вертикали 
|-- category_id: id категории 
 

Данные о рекламной компании (campaigns_meta.parquet)
|-- adv_campaign_id: id рекламной компании 
|-- start_date: date дата начала рекламной компании 
|-- end_date: date дата завершения рекламной компании
|-- goal_cost: цена за клик на рекламу
|-- goal_budget: общий бюджет рекламной компании
|-- logcat_id: id логической категории товаров из рекламной кампании
|-- location_ids: id локации, на которую рекламная компания распространяется 

:arrow_up:[к оглавлению](#оглавление)

### Этапы проекта

Проект включает в себя несколько этапов, каждый из которых будет проанализирован и оформлен в Jupyter Notebook:

1. **Изучение и подготовка данных.**

   * Изучение структуры данных и признаков. Заполнение пропусков в данных, предподготовка признаков для последующего анализа.
     
2. **Работа с каждым признаком в данных:**
   
   * Знаковмство с признаком: изучение распределения значений, статистических показателей, выбросов, а также влияния каждого признака на целевой признак.
   * Выделение новых признаков: создание новых признаков на основе рассматриваемого на этом этапе и оценка их влияния на целевую переменную.
   * Принятие решения о включение признака для обучения модели: проведение корреляционнного и статистического анализа.
     
3. **Кодировка категориальных признаков.**
   
   * Для категориальных признаков будет проведена кодировка.
     
4. **Оценка влияния отобранных признаков на целевую переменную, а также изучение корреляции между признаками.**
   
   * Построение корреляционной матрицы для всех признаков.
   * Исключение признаков с высокой корреляцией между собой.
   * Оценка значимости влияния признаков на целевую переменную и отбор самых важных
  
5. **Обучение модели.**

   * Выбор подходящего алгоритма для машинного обучения.
     
6. **Оценка модели.**
   
    После обучения модели будут проведены тесты для оценки ее точности и качества предсказаний.
   
7. **Предсказание на тестовой выборке**
   
   В конце проекта выполним тестовое предсказание на тестовой выборке.

   
:arrow_up:[к оглавлению](#оглавление)

### ***Структура проекта***

- [avitotech-ml-cup-2024.ipynb](https://github.com/Twi1ightFox/avitotech_ml_cup_2024/blob/master/avitotech-ml-cup-2024.ipynb): Jupyter ноутбук.
- [README.md](https://github.com/Dashaklen/Project_2_HH/blob/master/README.md): Описание проекта.

:arrow_up:[к оглавлению](#оглавление)

### Используемые библиотеки

Для работы с проектом потребуется установить следующие библиотеки:

- numpy  Линейная алгебра
- polars  Обработка и чтение данных
- sklearn  Основные модули библиотеки scikit-learn
- scipy Статистический пакет SciPy
- category_encoders Кодировщики категорий
- lightgbm Для предсказания
:arrow_up:[к оглавлению](#оглавление)


### Выводы:

- В ходе работы были выделены следующие признаки, влияющие на оценку отеля и повышающие точность прогноза:
   *  'total_unique_banners_before_today' - количество увиденных уникальных баннеров пользователем к предыдущему дню
   *  'total_unique_campaigns_before_today' - количество увиденных уникальных рекламных кампаний пользователем к предыдущему дню
   *  'is_vertical_8_9' - является ли показанная реклама из 8 или 9 вертикали,
   *  'is_level_3_4' - является ли показанная реклама из 3 или 4 уровня,
   *  'shift_ctr_user_logcat_week' - ctr логической категории для каждого пользователя за прошедшую неделю,
   *  'budget_balances' - остатки баланса рекламной кампании к текущему дню,
   *  'is_click_banner_code' - был ли клик по баннеру у пользователя в прошлом
   *  'ctr_creative_banner' - был ли клик по данному креативу и конкретному баннеру в прошлом(предыдущий день),
   *  'ctr_creative_banner_w' - был ли клик по данному креативу и конкретному баннеру в прошлом(предыдущая неделя),
   *  'is_main' - был ли показ с главной страницы,
   *  'ctr_user_campaign' - ctr рекламной кампании для каждого пользователя за прошедший день,
   *  'cumsum_user_logcat_shows' - сколько показов каждой логической категории было каждому пользователю в прошлом,
   *  'ctr_user_logcat' - ctr логической категории для каждого пользователя за прошедший день,
   *  'is_first_show_adv_campaign_for_user' - был ли это первый показ рекламной кампании пользователю,
   *  'shift_ctr_user_adv_campaign_week' - ctr рекламной кампании для каждого пользователя за прошедшую неделю,
   *  'is_saturday' - был ли день показа субботой,
   *   'is_fri_or_sund' -был ли день показа пятницей или воскресеньем,
   *   'ctr_adv_campaign' - общая ctr рекламной кампании к предыдущему периоду,
   *   'ctr_banner' - общая ctr баннера к предыдущему периоду,
   *   'days_since_campaign_start' - количество дней, которое прошло с начала кампании до показа,
   *   'ctr_location' - общая ctr локации к предыдущему периоду,
   *   'ctr_user' - общий ctr юзера к предыдущему периоду,
   *   'is_click_category' - был ли в прошлом клик у конкретного юзера  конкретной категории,
   *   'categories_id1' - показана ли пользователю категория 1,
   *   'categories_id2' - показана ли пользователю категория 2,
   *   'categories_id3' - показана ли пользователю категория 3,
   *   'categories_id4' - показана ли пользователю категория 4,
   *   'categories_id5' - показана ли пользователю категория 5,
   *   'categories_id6' - показана ли пользователю категория 6,
   *   'categories_id7' - показана ли пользователю категория 7,
   *   'categories_id8' - показана ли пользователю категория 8,
   *   'categories_id9' - показана ли пользователю категория 9,
   *   'categories_id11' - показана ли пользователю категория 11,
   *   'platform_id_1' - просмотр с устройства 1,
   *   'platform_id_2' - просмотр с устройства 2,
   *   'platform_id_3' - просмотр с устройства 3,
   *   'platform_id_4' - просмотр с устройства 4,
   *   'week_1' - показ приходился на первую неделю месяца,
   *   'week_2' - показ приходился на вторую неделю месяца,
   *   'week_3' - показ приходился на третью неделю месяца,
   *   'week_4' - показ приходился на четвертую неделю месяца,
   *    'ctr_banner_us' - ctr баннера для каждого пользователя за прошедшие периоды(прошедший день),
   *    'ctr_user_week' - общий ctr юзера за прошедую неделю,
   *    'ctr_banner_us_week' - ctr баннера для каждого пользователя за прошедшие периоды(прошедшая неделя)

:arrow_up:[к оглавлению](#оглавление)

### Заключительные Выводы:
В ходе кросс валидации лучшими парметрами для модели LightGBM оказались:
   * 'learning_rate': 0.09. Меньшие и наоборт большие значения приводили к снижению качества предсказания модели
   * 'bagging_freq': 10. Увеличение до 10 значительно повысило качество предсказания
   * 'num_leaves': 31. Меньшие и наоборт большие значения приводили к снижению качества предсказания модели

Получение дополнительных данных могло бы улучшить модель:
   * Данные о времени показа рекламы. В разное время пользователи по разному реагируют на рекламные кампании. Например в будние дни можетт наблюдаться активность и в утренние часы, в то время как в выходные активность может сместиться на более поздние часы. Также это позволит выявить какие рекламные кампании в какое время и день недели более кликабельны.
   * Данные о поле пользователя. Мужчины и женщины интересуются разными товарами.
   * Данные о возрасте пользователей. В разном возрасте у пользователей разные интересы.

:arrow_up:[к оглавлению](#оглавление)

### Установка и использование

1. Клонируйте репозиторий:
   git clone [https://github.com/Twi1ightFox/avitotech_ml_cup_2024.git](https://github.com/Twi1ightFox/avitotech_ml_cup_2024)
   
2. Загрузите необходимые файлы:
   
   (Дополнительные таблицы для проекта)[https://ods.ai/competitions/avitotechmlcup2024/dataset]
   
3. Запустить Jupyter notebook для просмотра и запуска анализа.

:arrow_up:[к оглавлению](#оглавление)
