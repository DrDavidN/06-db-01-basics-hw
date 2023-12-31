# 06-db-01-basics-hw - «Типы и структура СУБД» - Дрибноход Давид

## Задача 1

Архитектор ПО решил проконсультироваться у вас, какой тип БД 
лучше выбрать для хранения определённых данных.

Он вам предоставил следующие типы сущностей, которые нужно будет хранить в БД:

- электронные чеки в json-виде,

  Ответ: В этом случае подойдет документо-ориентированная СУБД, например, MongoDB, потому, что в качестве объекта хранения выступает документ формата json.
  
- склады и автомобильные дороги для логистической компании,

  Ответ: Подойдет графовая БД так как адреса и названия складов представляют из себя узлы, а дороги, по которым происходит перемещение между этими складами, представляют ребра графовой структуры.
  
- генеалогические деревья,

  Ответ: Сетевая БД потому, что у потомка может быть несколько связей с родителями.
  
- кэш идентификаторов клиентов с ограниченным временем жизни для движка аутенфикации,

  Ответ: В данном случае подойдет БД формата ключ-значение так как можно задать время жизни для каждой записи, т.е. ключ - это идентификатор, а значение - имя клиента
  
- отношения клиент-покупка для интернет-магазина.

  Ответ: Реляционная БД так как множество записей о клиентах имеют множество связей с товарами и их свойствами.


## Задача 2

Вы создали распределённое высоконагруженное приложение и хотите классифицировать его согласно 
CAP-теореме. Какой классификации по CAP-теореме соответствует ваша система, если 
(каждый пункт — это отдельная реализация вашей системы и для каждого пункта нужно привести классификацию):

- данные записываются на все узлы с задержкой до часа (асинхронная запись);

  Ответ: Это A или AP - система, так как данные на всех узлах совпадают только через 1 час, т.е. нет согласованности данных.
  
- при сетевых сбоях система может разделиться на 2 раздельных кластера;

  Ответ: Это P или AP система. Система может разделяться на несколько изолированных частей причем система доступна в этот момент.
  
- система может не прислать корректный ответ или сбросить соединение.

  Ответ: Это СP или С или Р система, так как она не обеспечивает доступность ответа.

Согласно PACELC-теореме как бы вы классифицировали эти реализации?

- данные записываются на все узлы с задержкой до часа (асинхронная запись);

  Ответ: Система PA/EL, так как не обеспечивается согласованность данных или PA/EC, если работает один узел.
  
- при сетевых сбоях система может разделиться на 2 раздельных кластера;

  Ответ: PA или PC
  
- система может не прислать корректный ответ или сбросить соединение.

  Ответ: PC/EC

## Задача 3

Могут ли в одной системе сочетаться принципы BASE и ACID? Почему?

Ответ: Два этих принципа не могут сочетаться потому, что они противоречат друг другу. BASE ориентирован на производительность системы (доступность), ACID на сохранность данных (стойкость к разделению и сохранность данных).

## Задача 4

Вам дали задачу написать системное решение, основой которого бы послужили:

- фиксация некоторых значений с временем жизни,
- реакция на истечение таймаута.

Вы слышали о key-value-хранилище, которое имеет механизм Pub/Sub. 
Что это за система? Какие минусы выбора этой системы?

Ответ: Вероятно речь идет о системе Redis, которая может выступать как key-value хранилище, так и брокером сообщений.

Минусы системы Redis:
- Нет гарантий устойчивости системы, особенно учитывая то, что операции по сохранению данных на диск (об этом — ниже) выполняются асинхронно.
- Высокие требования к оперативной памяти сервера, так как данные хранятся в ней
- Работает только на одном ядре процессора в однопоточном режиме
- Отсутствует разграничение прав по пользователям и доступ предоставляется только  по общему логину  и паролю
- Отсутствие синтаксиса языка SQL
- Экземпляр БД не масштабируется
