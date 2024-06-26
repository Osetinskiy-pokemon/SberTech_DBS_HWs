# Знакомство с KeyDB
## История развития СУБД:
KeyDB – это высокопроизводительная, многопоточная база данных типа "ключ-значение". Она является форком известной СУБД Redis, который был создан для улучшения производительности за счет многопоточности, не изменяя при этом основной модели взаимодействия Redis. 

**История развития KeyDB:**
* **2019 год:** KeyDB начала свое существование как форк Redis, целью которого было внедрение многопоточной обработки запросов для улучшения производительности. Создатели KeyDB заметили, что Redis, хотя и крайне производителен в своем однопоточном исполнении, имеет ограничения по производительности на многоядерных процессорах.

    Основные особенности при запуске:
    * Многопоточность: в отличие от Redis, который использует однопоточную модель, KeyDB работает с несколькими потоками для выполнения команд, что позволяет эффективнее использовать ресурсы многоядерных процессоров.
    * Совместимость с Redis: KeyDB поддерживает большинство команд и функций Redis, что позволяет пользователям Redis легко мигрировать на KeyDB без изменения большей части кода.
* **2020-2021 годы:** Разработка KeyDB продолжилась с внедрением дополнительных функций и улучшений производительности. Были добавлены такие функции, как репликация потоков, что позволяет реплицировать данные между экземплярами KeyDB более эффективно.
* **2022 год и далее:** KeyDB продолжает развиваться с добавлением новых возможностей, таких как улучшенное управление памятью и более гибкие настройки конфигурации. Комьюнити вокруг KeyDB растет, предоставляя обратную связь и поддержку для дальнейшего улучшения продукта.
* **На сегодняшний день** доступна версия 6.3.2, в которую включены поддержка бета-уровня KeyDB FLASH, новые команды ASYNC, улучшение задержки и ряд исправлений ошибок.
* Также сообщается, что **вскоре** будут доступны поддержка мультитенантности через выделенные пространства имен, появится встроенная поддержка вложенных хешей, что означает поддержку вложенных структур данных, такие как хэши, значения и списки внутри хэшей, а также поддержку большинства объектов JSON.

## Инструменты для взаимодействия с СУБД:
Для взаимодействия с базой данных KeyDB можно использовать различные инструменты и библиотеки, большинство из которых также совместимы с Redis благодаря их общей совместимости на уровне команд. Несколько популярных инструментов и библиотек для работы с KeyDB представлены ниже.

1. Клиентские библиотеки
KeyDB поддерживает широкий спектр клиентских библиотек, доступных для различных языков программирования:
    * redis-py (Python): Python клиент для работы с Redis и KeyDB. Он предоставляет простой интерфейс для выполнения команд KeyDB.
    * Jedis (Java): популярная клиентская библиотека для Java, которая также может использоваться для взаимодействия с KeyDB благодаря совместимости с Redis.
    * node_redis (Node.js): библиотека предоставляет API для Node.js для взаимодействия с Redis и KeyDB.

2. Интерфейсы командной строки (CLI)
    * KeyDB CLI: KeyDB поддерживает стандартный интерфейс командной строки Redis, который позволяет взаимодействовать с базой данных через терминал, что является мощным инструментом для управления базой данных, выполнения запросов и отладки.

3. Инструменты мониторинга и управления
    * RedisInsight by Redis Labs: GUI инструмент, который можно использовать для визуализации и управления базами данных Redis и KeyDB. Он предоставляет удобные инструменты для мониторинга производительности, анализа данных и управления ключами.
    * Redmon: веб-интерфейс для мониторинга Redis/KeyDB, который позволяет наблюдать за состоянием сервера в реальном времени.

4. Библиотеки для интеграции
    * Spring Data Redis (Java): Spring Data Redis предоставляет легко интегрируемые конфигурации для подключения к Redis и KeyDB в Java приложениях, используя Spring Framework.
    * Lettuce (Java): высокопроизводительная, асинхронная, реактивная библиотека для работы с Redis и KeyDB в Java.

5. Поддержка в облачных платформах
    * AWS ElastiCache: поскольку KeyDB совместим с Redis, его также можно развернуть и управлять через облачные сервисы, поддерживающие Redis, такие как AWS ElastiCache.

Для того чтобы взаимодействовать с KeyDB через CLI, можно использовать следующие команды (bash):
```
# Подключение к серверу KeyDB
keydb-cli -h <hostname> -p <port>

# Установка ключа
SET mykey "Hello, KeyDB"

#Получение значения ключа
GET mykey
```

## Какой database engine используется в KeyDB:
KeyDB, как и его предшественник Redis, использует в качестве основы для хранения данных in-memory database engine. Это означает, что все данные хранятся в оперативной памяти, что обеспечивает очень высокую скорость чтения и записи данных. Такая архитектура идеально подходит для задач, требующих максимально быстрого доступа к данным, например, для кэширования, сессий в веб-приложениях и других операций, требующих высокой производительности.

Особенности in-memory хранения в KeyDB:
* Высокая производительность: доступ к данным осуществляется очень быстро, так как они находятся непосредственно в оперативной памяти.
* Персистентность: несмотря на то что основное хранение происходит в памяти, KeyDB предлагает различные механизмы для сохранения данных на диск, что позволяет восстановить состояние базы данных после перезагрузки системы. KeyDB поддерживает два основных способа персистентности:
    * RDB (Redis Database File): снимки состояния базы данных сохраняются в определённые моменты времени в виде одного файла.
    * AOF (Append Only File): все операции, изменяющие данные, записываются в файл в виде команд, что позволяет восстановить последовательное состояние изменений.
* Многопоточность: в отличие от Redis, KeyDB реализует многопоточную обработку запросов, что значительно улучшает производительность на многоядерных системах. Это достигается за счёт использования нескольких потоков для обработки команд, позволяя более эффективно использовать аппаратные ресурсы сервера.

Для настройки персистентности в KeyDB можно использовать конфигурационные параметры в файле настройки или через команды CLI. Пример включения AOF для непрерывной записи изменений:
```
# Включение AOF
CONFIG SET appendonly yes

# Указание пути к AOF файлу
CONFIG SET appendfilename "appendonly.aof"
```
Этот механизм обеспечивает надёжность и гарантирует, что данные не потеряются в случае сбоя системы, обеспечивая при этом высокую производительность работы базы данных.

## Как устроен язык запросов KeyDB:
KeyDB использует тот же язык запросов, что и Redis, который является простым и основан на текстовых командах. Этот язык не является SQL-подобным, вместо этого он использует набор простых команд для выполнения операций над данными, которые включают создание, чтение, обновление и удаление значений ключей. Каждая команда определяет операцию над определённым типом данных, такими как строки, списки, словари (хэши), множества и отсортированные множества.

**Примеры команд KeyDB:**
* SET key value – установка значения ключа.
* GET key – получение значения ключа.
* HSET key field value – установка значения в хэш.
* HGET key field – получение значения из хэша.
* LPUSH key value – добавление значения в начало списка.
* LPOP key – извлечение первого значения из списка.
* SADD key value – добавление элемента в множество.
* SMEMBERS key – получение всех элементов множества.

**Разворачивание и выполнение нескольких запросов:**

![img1](https://github.com/Osetinskiy-pokemon/SberTech_DBS_HWs/assets/71440118/8d77f901-47bb-4b93-a426-c46af8ddb1aa)

![img2](https://github.com/Osetinskiy-pokemon/SberTech_DBS_HWs/assets/71440118/a58c4fe3-cbbd-4bab-b155-617a1bc7090a)

![img3](https://github.com/Osetinskiy-pokemon/SberTech_DBS_HWs/assets/71440118/3483d7bf-f8c8-46d3-9e7d-cbd96413b451)

![img4](https://github.com/Osetinskiy-pokemon/SberTech_DBS_HWs/assets/71440118/e6c80deb-dc81-4ce8-89ce-38a93a6da160)

## Распределение файлов БД по разным носителям:
Распределение файлов базы данных KeyDB по разным носителям имеет особенности, связанные с её архитектурой in-memory и механизмами персистентности данных. Поскольку KeyDB является базой данных типа "ключ-значение", которая первоначально хранит все данные в оперативной памяти (RAM), механизмы распределения данных по физическим носителям зависят от выбранного метода сохранения данных на диск.

Основные способы хранения данных в KeyDB:
* Оперативная память (RAM):
    * Основное хранение данных: все данные хранятся в оперативной памяти для обеспечения максимальной скорости доступа, что делает KeyDB идеальным решением для задач, требующих высокой производительности, таких как кэширование, сессии веб-приложений и очереди сообщений.
* Дисковые накопители (HDD или SSD):
    * RDB (Snapshotting): при использовании механизма RDB состояние базы данных в определённые моменты времени полностью снимается и сохраняется на диск в виде одного файла, что может быть полезно для реализации резервного копирования и восстановления после сбоя.
    * AOF (Append Only File): при использовании AOF все операции, изменяющие данные, записываются в журнал команд. Этот файл может храниться на более быстрых SSD для ускорения процесса восстановления и уменьшения времени отклика при перезагрузке.
* Облачное хранение:
    * Для улучшения надежности и масштабируемости, файлы базы данных могут быть также сохранены в облачное хранилище. Это может быть полезно для геораспределённого резервного копирования и катастрофоустойчивости.

**Примеры настройки:**

* Конфигурация для RDB может включать автоматическое создание снимков через определенные интервалы времени, которые затем можно сохранять на разные типы накопителей в зависимости от требований к производительности и стоимости.
* Конфигурация AOF может быть настроена таким образом, чтобы файлы журнала были распределены по SSD для увеличения скорости записи и уменьшения задержек при восстановлении.

## На каком языке/ах программирования написана СУБД:
KeyDB, так же как и Redis, из которого она была производной, написана в основном на языке программирования C. Выбор обусловлен необходимостью обеспечения высокой производительности и эффективности управления памятью, что критично для баз данных, работающих с данными в реальном времени и хранящих большие объемы информации в оперативной памяти.

Язык C позволяет разработчикам тонко настраивать управление памятью и процессами, что идеально подходит для создания высокопроизводительных систем, таких как KeyDB. Это также способствует легкой интеграции с различными системными уровнями и операционными системами.

## Какие типы индексов поддерживаются в БД:
KeyDB, как и Redis, по умолчанию не предоставляет традиционные механизмы индексации, как в реляционных базах данных. Основная работа с данными происходит через прямой доступ к ключам. Однако, можно организовать индексацию данных с помощью структур данных и дополнительных библиотек, включая внешние решения, такие как RediSearch.

Использование структур данных KeyDB, таких как списки, множества, отсортированные множества и хэши, может служить своего рода индексацией:
* Списки: могут использоваться для создания очередей или стеков, где порядок элементов имеет значение.
* Множества: идеальны для хранения уникальных элементов, которые можно быстро проверять на наличие.
* Отсортированные множества (sorted sets): позволяют хранить элементы с заданным весом (score), что полезно для ранжирования или приоритетных очередей.
* Хэши: подходят для хранения объектов с множеством полей, например, информации о пользователе.

Например, есть база данных пользователей, есть желание индексировать их по количеству очков. Можно использовать отсортированное множество, где ключ — это идентификатор пользователя, а score — количество очков.
```
# Добавление пользователей с их очками
ZADD scores 10 user_1 13 user_2 11 user_3
# Получение списка пользователей, отсортированных по очкам
ZRANGE scores 0 -1 WITHSCORES
```

**Внешние индексационные решения:**

RediSearch — это модуль для Redis и KeyDB, который предоставляет полноценные функции поиска и вторичной индексации. С его помощью можно создавать индексы по различным полям, проводить сложные поисковые запросы с различными условиями и фильтрами.

## Процесс выполнения запросов в KeyDB:
Процесс выполнения запросов в KeyDB, как и в его предшественнике Redis, основывается на эффективной обработке команд в оперативной памяти. Отличительной особенностью KeyDB является его многопоточная архитектура, которая позволяет параллельно обрабатывать множество запросов, что значительно повышает производительность по сравнению с однопоточной моделью Redis. Ниже описаны этапы выполнения запросов в KeyDB.

1. Приём запросов
    * Сетевое подключение: клиенты подключаются к серверу KeyDB через TCP/IP. KeyDB слушает входящие подключения на заданном порте (по умолчанию 6379).
    * Обработка входящих данных: когда запрос поступает от клиента, сервер KeyDB принимает и обрабатывает входящий поток данных. Запросы представлены в виде последовательности байтов.

2. Обработка запросов
    * Анализ запроса (Parsing): KeyDB анализирует текст запроса, разделяя его на команду и аргументы.
    * Выполнение команды: определив команду и её аргументы, сервер выполняет соответствующую операцию, используя данные, хранящиеся в оперативной памяти. Запросы могут касаться различных типов данных, таких как строки, списки, множества, хеши, отсортированные множества.

3. Многопоточная обработка
    * Многопоточность: в KeyDB многие операции, включая сетевую обработку и выполнение команд, распараллеливаются между несколькими потоками, что позволяет более эффективно использовать многоядерные процессоры.

4. Отправка ответа
    * Формирование ответа: после обработки запроса KeyDB формирует ответ.
    * Отправка ответа клиенту: ответ отправляется обратно клиенту через тот же сетевой сокет, который был использован для приёма запроса.

5. Логирование и персистентность
    * Журналирование (AOF): если включена персистентность с помощью AOF, все изменяющие данные команды записываются в файл журнала, что позволяет восстановить состояние базы данных после перезапуска.
    * Снимки состояния (RDB): в определённые моменты времени KeyDB может создавать снимки текущего состояния данных, сохраняя их в файл.

Выполнение команды SET key value:
1. Команда SET key value поступает от клиента.
2. KeyDB анализирует команду и определяет, что это команда установки значения.
3. Значение value ассоциируется с ключом key в памяти.
4. Если включен AOF, команда записывается в файл AOF.
5. KeyDB формирует ответ OK, который отправляется обратно клиенту.

Многопоточная модель позволяет KeyDB обрабатывать большое количество запросов одновременно, что делает её идеальной для высоконагруженных приложений, требующих быстрого доступа к данным.

## Понятие «план запросов» в KeyDB:
KeyDB, подобно Redis, не использует понятие «план запросов» в том смысле, как это принято в традиционных реляционных системах управления базами данных (СУБД). В реляционных СУБД план запроса — это детализированное описание того, как база данных выполнит запрос, включая использование индексов, соединения таблиц и другие операции оптимизации.

**Особенности выполнения запросов в KeyDB:**
1. Прямая обработка команд: KeyDB работает как сервер команд, где каждая команда имеет определённые функции и выполняется непосредственно без предварительного составления планов выполнения. Команды применяются напрямую к данным в памяти.
2. Отсутствие оптимизации запросов: поскольку KeyDB использует структуры данных, оптимизированные для конкретных типов операций (например, быстрый доступ к ключам, спискам, словарям, множествам и т.д.), не требуется дополнительной оптимизации выполнения запросов в виде плана запроса. Каждая команда оптимизирована для максимальной производительности с учётом своей структуры данных.
3. Мгновенное выполнение: KeyDB разрабатывался для обеспечения высокой производительности при работе с запросами в реальном времени. Все операции, включая чтение и запись, обрабатываются очень быстро благодаря прямому доступу к данным в памяти.

**Примеры запросов без плана:**

Когда происходит выполнение запроса в KeyDB, например, GET key для получения значения по ключу или HGETALL myhash для получения всех пар ключ-значение из хеша, сервер немедленно обращается к соответствующей структуре данных и выполняет запрос без предварительного анализа или планирования.

## Поддержка транзакций KeyDB:
KeyDB, как и Redis, поддерживает транзакции, хотя они и отличаются от традиционных реляционных транзакций. В KeyDB транзакции обеспечивают выполнение группы команд в виде атомарной операции, но без некоторых возможностей, таких как проверки целостности данных на уровне транзакции или сложное управление конфликтами.

**Особенности транзакций в KeyDB:**
* Атомарность: группа команд в транзакции KeyDB выполняется атомарно, что означает, что либо все команды выполняются, либо ни одна, если произойдет ошибка в процессе выполнения.
* Изоляция: команды в транзакции исполняются последовательно, как один неделимый блок. Однако KeyDB не обеспечивает полной изоляции на уровне транзакций в многопользовательском окружении, как в реляционных СУБД.
* Отсутствие защиты от взаимоблокировок: в KeyDB не реализована детекция взаимоблокировок, и пользователь должен самостоятельно управлять возможными блокировками.

**Как работают транзакции в KeyDB:**
1. MULTI: начинает транзакцию.
2. Команды: серия команд, которые нужно выполнить.
3. EXEC: запускает выполнение всех команд, добавленных после MULTI.

**Альтернативы для управления состоянием в KeyDB:**
* Lua-скрипты обеспечивают возможность выполнения сложных операций как единой атомарной задачи на сервере.
* WATCH: команда для оптимистичного блокирования. WATCH следит за изменениями ключей, и если ключ изменяется другим клиентом во время транзакции, EXEC не выполнит транзакцию.

Транзакции в KeyDB идеально подходят для сценариев, где требуется гарантировать атомарность выполнения нескольких операций. Они особенно полезны в сценариях, связанных с модификацией нескольких ключей, где необходимо обеспечить, что изменения применяются полностью или не применяются вовсе.

## Методы восстановления в KeyDB:
KeyDB, как и его основа Redis, поддерживает несколько методов восстановления данных для обеспечения надежности и устойчивости системы к сбоям. Методы включают использование снимков состояния базы данных (RDB) и журналов всех операций (AOF). Рассмотрим каждый из этих методов подробнее.

1. RDB (Redis Database File) — это метод снимков, который сохраняет полное состояние базы данных в определенные моменты времени. Снимки создаются периодически на основе настроек, которые определяют, как часто и при каких условиях создавать новый снимок.

    Преимущества:
        * Быстрое восстановление: RDB позволяет быстро восстановить всю базу данных, поскольку для восстановления используется один файл.
        * Эффективное использование дискового пространства — сжатие данных при сохранении.

В конфигурационном файле keydb.conf можно настроить интервалы создания снимков, например:
```
save 900 1   # сохранять каждые 15 минут, если было хотя бы 1 изменение
save 300 5  # сохранять каждые 5 минут, если было хотя бы 5 изменений
```

2. AOF (Append Only File) записывает каждую операцию, изменяющую данные, в журнал команд. Этот метод обеспечивает высокую устойчивость данных, так как в случае сбоя можно восстановить базу данных, выполнив все операции из AOF.

    Преимущества:
    * Устойчивость к сбоям: AOF минимизирует риск потери данных, так как каждая операция записывается по мере её выполнения.
    * Точность восстановления: восстановление данных до последней успешной команды.

В keydb.conf можно настроить поведение AOF:
```
appendonly yes
appendfsync everysec  # синхронизация с диском каждую секунду
```

При перезапуске KeyDB автоматически проверяет наличие и читает последний доступный AOF или RDB файл для **восстановления данных**.

Процесс восстановления:
* Использование AOF: если AOF включен, KeyDB восстанавливает данные, последовательно выполняя команды из файла.
* Использование RDB: если AOF отключен, но доступен RDB файл, KeyDB восстанавливает состояние базы данных из этого файла.

Часто рекомендуется использовать одновременно и RDB, и AOF для максимальной надежности. RDB обеспечивает быстрое восстановление при старте и минимизацию потерь данных, а AOF гарантирует, что операции не будут потеряны между интервалами сохранения RDB.
Эти методы восстановления данных позволяют гарантировать, что система KeyDB может быстро восстановиться после сбоев, обеспечивая надежность и доступность критически важных данных.

## Шардинг в KeyDB:
Шардинг в KeyDB, как и в Redis, позволяет распределить нагрузку данных по разным узлам, что увеличивает производительность и масштабируемость системы. Шардинг в KeyDB осуществляется путём разделения данных на фрагменты, каждый из которых хранится на отдельном узле. Ниже описано несколько подходов к шардингу.

1. Шардинг на уровне приложения
    Самый базовый и распространенный метод шардинга, при котором логика распределения данных по узлам встроена непосредственно в приложение. Приложение знает, какой шард содержит нужные данные, и направляет запросы соответственно.

    Принцип работы:
    * Приложение использует хэш-функцию или другой механизм для определения, на каком сервере должен храниться каждый ключ.
    * Каждый экземпляр KeyDB управляет своим набором данных независимо от других.

2. Шардинг с использованием прокси
    Прокси-серверы, такие как Twemproxy или KeyDB Proxy, могут автоматически распределять запросы между различными узлами KeyDB. Прокси принимает запросы от клиентов и перенаправляет их на соответствующий узел, основываясь на ключе запроса.

    Принцип работы:
    * Прокси-сервер выступает в качестве посредника между клиентами и серверами KeyDB.
    * Клиенты подключаются к прокси, а прокси перенаправляет запросы на нужные узлы на основе алгоритма шардинга.

3. Кластеризация KeyDB
    KeyDB поддерживает кластерный режим, который автоматически управляет шардингом данных по узлам. В этом режиме узлы KeyDB обмениваются информацией о состоянии кластера, автоматически перераспределяя данные при необходимости.

    Принцип работы:
    * Кластер KeyDB состоит из множества узлов, каждый из которых хранит часть данных.
    * Клиенты подключаются к любому узлу кластера, который может перенаправлять запросы на узел, владеющий данными.
    * Кластер поддерживает автоматическое перебалансирование данных при добавлении или удалении узлов.

Преимущества шардинга в KeyDB:
* Масштабируемость: шардинг позволяет обрабатывать больший объем данных и увеличивать пропускную способность системы.
* Высокая доступность: распределение данных по нескольким узлам может улучшить доступность и устойчивость системы к отказам.
* Гибкость: есть мозможность выбора метода шардинга, который лучше всего подходит для конкретного приложения и инфраструктуры.

## Применение терминов Data Mining, Data Warehousing и OLAP в KeyDB:
KeyDB, как и его основа Redis, первоначально разработан как база данных типа "ключ-значение" для операций с высокой производительностью и низкой задержкой. Хотя основное назначение KeyDB — это обеспечение быстрого доступа к данным в оперативной памяти, ниже рассмотрим, как термины Data Mining, Data Warehousing и OLAP могут быть связаны или применены к этой системе.

1. Data Mining (извлечение данных) — это процесс анализа больших наборов данных для выявления закономерностей и тенденций. KeyDB сама по себе не предоставляет инструментов для Data Mining, но её можно использовать в качестве одного из компонентов в более широкой архитектуре для сбора и временного хранения данных, которые могут быть использованы другими системами для анализа.

2. Data Warehousing (хранилище данных) включает сбор данных из разных источников для дальнейшего анализа и отчетности. Хранилища данных обычно оптимизированы для операций чтения, агрегирования и управления большими объемами данных. KeyDB, будучи системой управления базами данных в памяти, не предназначена для использования в качестве традиционного хранилища данных из-за ограниченности по объему хранимой информации и отсутствия поддержки сложных запросов анализа данных. Однако она может использоваться для реализации кэширования или временного хранения в сценариях, где требуется быстрый доступ к данным.

3. OLAP (On-Line Analytical Processing) — это подход к быстрому анализу информации из многомерных баз данных. OLAP часто связан с комплексными запросами, агрегацией данных и способностью выполнять сложные аналитические расчеты. KeyDB не поддерживает многомерные запросы или сложные аналитические операции, которые являются характерными для OLAP-систем. Тем не менее, KeyDB может быть использована для поддержки онлайн-обработки транзакций (OLTP), обеспечивая быструю запись и извлечение данных, которые впоследствии могут быть обработаны OLAP-системами.

Хотя KeyDB сама по себе не предназначена для выполнения задач Data Mining, Data Warehousing и OLAP, она может играть важную роль в архитектуре данных, где эти процессы требуют поддержки быстрого доступа к данным или временного хранения информации в процессе их обработки. Для комплексного анализа данных обычно используются специализированные инструменты и платформы, которые могут взаимодействовать с KeyDB для получения или временного хранения необходимых данных.

## Методы защиты, поддерживаемые KeyDB (шифрование трафика, модели авторизации и т.п.):
KeyDB, как и Redis, предоставляет различные методы защиты, которые обеспечивают безопасность данных и трафика между клиентами и сервером, которые включают шифрование трафика, модели аутентификации и конфигурационные настройки для управления доступом. Ниже перечислены основные методы защиты, поддерживаемые KeyDB:

1. Шифрование трафика (TLS/SSL)

    KeyDB поддерживает шифрование трафика через TLS/SSL, что позволяет защитить данные, передаваемые между клиентами и серверами, от перехвата и прослушивания. Шифрование может быть включено для всех клиентских соединений, а также для внутренних соединений в рамках кластера KeyDB.

    Для включения TLS необходимо настроить соответствующие параметры в конфигурационном файле keydb.conf. Например:
```
tls-port 6379
tls-cert-file /path/to/cert.pem
tls-key-file /path/to/key.pem
tls-ca-cert-file /path/to/ca.pem
tls-auth-clients no
```

Эти настройки определяют порт для TLS-соединений и пути к сертификатам для шифрования.

2. Аутентификация

   KeyDB поддерживает базовую аутентификацию с помощью пароля, которая конфигурируется через директиву requirepass в конфигурационном файле. Когда эта опция включена, клиенты должны аутентифицироваться, отправляя пароль при установлении соединения.
    Пример настройки аутентификации (После этого клиенты должны будут отправить команду AUTH с правильным паролем для доступа к серверу):
```
requirepass yourpassword
```

3. Расширенные настройки безопасности
    * Protected mode: режим предотвращает доступ к базе данных с любых IP-адресов, кроме localhost, если не задан пароль. Это стандартная мера безопасности для предотвращения несанкционированного доступа.
    * Access Control Lists (ACLs): ACL позволяют более тонко настраивать права доступа для различных пользователей, определяя, какие команды и на каких ключах разрешено выполнять.

    Пример настройки ACL:
```
# В этом примере пользователю don разрешено выполнять команды get, set и select, но запрещено удалять ключи
ACL SETUSER don on >alicepassword +get +set +select -del ~keys:*
```

4. Журналирование

   Настройка журналирования помогает отслеживать все операции, выполняемые в базе данных, что является важным аспектом обеспечения безопасности. Журналы можно анализировать на предмет подозрительной активности или аудита.

## Cообщества, развивающие KeyDB, кто в проекте имеет права на коммит и создание дистрибутива версий:
KeyDB развивается как проект с открытым исходным кодом, и его разработка ведётся командой, а также сообществом энтузиастов и разработчиков. Ранее была инсформация, что основное управление проектом осуществляется компанией EQ Alpha Technology Inc., которая стоит за большинством разработок и обновлений KeyDB.

EQ Alpha Technology Inc. — это компания, которая активно разрабатывает и поддерживает KeyDB. Она вносит значительный вклад в развитие базы данных, включая релизы новых версий, исправление ошибок, добавление новых функций и улучшение производительности. Компания также обеспечивает поддержку для коммерческих клиентов, предлагая усиленные версии KeyDB с дополнительными возможностями и улучшенной поддержкой.

Помимо основной команды разработчиков из EQ Alpha Technology, к развитию KeyDB также присоединяются **независимые разработчики и компании**, которые используют эту СУБД в своих проектах. Они вносят свой вклад, отправляя пулл-реквесты через GitHub, где размещён исходный код проекта.

* Независимые разработчики могут отправлять пулл-реквесты через GitHub. Эти изменения рассматриваются командой EQ Alpha и другими членами сообщества.
* Право на коммит имеют ключевые разработчики из EQ Alpha Technology, а также некоторые активные участники сообщества, которые заработали доверие своими вкладами в проект.
* Создание официальных дистрибутивов и версий обычно контролируется основной командой разработчиков. Они управляют версиями, исправлениями ошибок и распространением обновлений.

KeyDB поддерживает активное взаимодействие с сообществом через **различные платформы**:
* GitHub: основная платформа для взаимодействия, где пользователи могут сообщать о проблемах, обсуждать улучшения и отправлять пулл-реквесты.
* Форумы и Slack каналы: для более оперативного общения и поддержки используются различные форумы и каналы в Slack.

На данный момент KeyDB присоединилась к **Snap Inc.**

## Создание своих собственных данных для демонстрации работы СУБД: 
Собственные данные уже были созданы выше, как и демонстрация работы:

![img2](https://github.com/Osetinskiy-pokemon/SberTech_DBS_HWs/assets/71440118/a58c4fe3-cbbd-4bab-b155-617a1bc7090a)

## Как продолжить самостоятельное изучение языка запросов с помощью демобазы:
Для KeyDB, как и для многих других баз данных, не предоставляется официальная "демо-база данных" напрямую. Однако, учитывая что KeyDB совместима с Redis, легко создать демонстрационные данные для обучения или тестирования на основе общих примеров, используемых для Redis. Выше это уже было продемонстрировано.

## Где найти документацию и пройти обучение:
Для изучения и обучения использованию KeyDB можно воспользоваться следующими ресурсами:
* На официальном сайте KeyDB ([keydb.dev](https://docs.keydb.dev/)) доступна подробная документация, которая включает руководства пользователя, настройки конфигурации, информацию о командах и многопоточности. Здесь же можно найти разделы FAQ и блог, где обсуждаются различные аспекты использования и развития KeyDB.

* Исходный код KeyDB доступен на GitHub ([github.com/Snapchat/KeyDB](https://github.com/Snapchat/KeyDB)), где также можно найти дополнительную документацию и примеры использования. 

* Хотя специализированных курсов именно по KeyDB может быть не так много, есть возможность найти множество ресурсов по Redis, с которым KeyDB полностью совместима. Платформы, такие как Udemy, Coursera, и YouTube, предлагают курсы и видеоруководства, которые могут быть полезны для изучения концепций и операций, общих для Redis и KeyDB.

* Книги по Redis также могут быть полезны, так как основные принципы и команды применимы к KeyDB. Примеры таких книг: "Redis in Action" и "Redis Essentials".

* Блоги и статьи, написанные сообществом и экспертами, могут предложить практические советы, углублённые технические детали и реальные сценарии использования KeyDB. Часто эти ресурсы публикуются на технических блогах или платформах вроде Medium.
  
* Участие в сообществах и форумах, таких как Stack Overflow и Reddit, может помочь получить ответы на специфические вопросы, узнать о лучших практиках и поделиться опытом с другими пользователями KeyDB.
Эти ресурсы обеспечат хорошую стартовую базу для изучения KeyDB, а также помогут получить более глубокие знания и практические навыки работы с этой системой управления базами данных.

## Как быть в курсе происходящего
Чтобы быть в курсе последних новостей, обновлений и событий, связанных с KeyDB, можно использовать несколько подходов и ресурсов. Ниже представлены некоторые из наиболее эффективных по моему мнению способов оставаться информированным:

1. Официальный сайт KeyDB, где регулярно публикуются обновления, новости и блоги, связанные с развитием и использованием KeyDB. Это первичный источник официальной информации.
    ([keydb.dev](https://docs.keydb.dev/))

2. Социальные сети и блоги, такие как Twitter, LinkedIn, или Facebook. Компании часто используют эти платформы для быстрого распространения новостей о выпуске новых версий, организации мероприятий и публикации технических статей.
   ([twitter.com/realkeydb](https://twitter.com/realkeydb))

3. Проект KeyDB активно использует GitHub для управления исходным кодом. Можно следить за репозиторием, чтобы получать уведомления о новых коммитах, запросах на слияние, обсуждениях и других изменениях. Участие в обсуждениях и ознакомление с пулл-реквестами также может дать глубокое понимание направлений развития проекта.
    ([github.com/Snapchat/KeyDB](https://github.com/Snapchat/KeyDB))



