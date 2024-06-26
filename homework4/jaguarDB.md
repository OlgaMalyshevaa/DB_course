# JaguarDB

## а. История развития СУБД
DataJaguar — это стартап из Кремниевой долины, компания UStartX. Флагманский продукт DataJaguar — база данных JaguarDB. Дата создания: 2017 год.

## b. Инструменты для взаимодействия с СУБД
JaguarDB предлагает полный набор интерфейсов прикладного программирования (API). Эти API-интерфейсы могут быть легко использованы в клиентском терминале jql.bin или легко интегрируется с такими языками программирования как Java, Python, Go и Node.js. Такая гибкость позволяет разработчикам взаимодействовать с JaguarDB, используя предпочитаемую ими среду, обеспечивая бесперебойную и универсальную разработку.

## c.	Какой database engine используется в вашей СУБД?
JaguarDB использует собственный встроенный движок базы данных, разработанный специально для них.Он оптимизирован для работы с многомерными данными и обеспечивает высокую производительность при выполнении запросов и операций с данными.

## d.	Как устроен язык запросов в вашей СУБД? Разверните БД с данными и выполните ряд запросов. 
JaguarDB - это NoSQL, то есть масштабируемый с ограниченными возможностями SQL, ориентированный на
масштабируемость и производительность.
Стандартные SQL конструкции: JaguarDB поддерживает основные стандарты языка SQL, такие как SELECT, INSERT, UPDATE, DELETE, JOIN и другие.


**Insert command:**
```js
insert into user ( fname, lname, age, addr ) values ( 'Larry', 'Lee', 40,
'123 North Ave., CA' );
```
**Update command:**
```js
update user set fname='Tim', address='201 Main St., SR, CA 94506' where
fname='Sam' and lname='Walter';
```
**Delete command:**
```js
delete from user where fname='Sam' and lname='Walter';
```





## e. Распределение файлов БД по разным носителям?
Распределенная система баз данных Jaguar может похвастаться чрезвычайно масштабируемым дизайном
, основанным на кластерной архитектуре. Масштабирование JaguarDB основано на
кластерах, каждый из которых представляет собой согласованную группу узлов. Система позволяет легко
добавлять новые кластеры в любой момент, обеспечивая гибкость без
сбоев. Для повышения надежности данных доступны три реплики, обеспечивающие
избыточность. Для достижения оптимальной скорости записи и чтения распределение данных между серверными
узлами осуществляется посредством совместного использования. Примечательно, что любой клиент Jaguar может без особых усилий установить
подключение к любому серверу Jaguar.

## f.	На каком языке/ах программирования написана СУБД?
Сервер JaguarDB написан на C++. Клиентский API поддерживается Java, Scala, NodeJS, PHP, Python и т.д

## g.	Какие типы индексов поддерживаются в БД? Приведите пример создания индексов?
В JaguarDB реализованы как векторные, так и скалярные индексы. Скалярные индексы вместе с векторными индексами позволяют быстро находить записи данных, удовлетворяющие определенному условию, и получать к ним доступ.
JaguarDB поддерживает создание индекса BTree как для ключевых, так и для неключевых столбцов. Все ключевые столбцы автоматически сортируются в «Сортированном эластичном массиве», что позволяет легко запрашивать диапазон.

```js
create index addr_index on user( key: address, value: zipcode, city );
```

## h.	Как строится процесс выполнения запросов в вашей СУБД?

Процесс выполнения запроса в системе базы данных JaguarDB включает анализ SQL-запроса, оптимизацию плана запроса и выполнение запроса для извлечения и обработки данных. Этот многоэтапный процесс обеспечивает эффективное выполнение запросов и извлечение данных в архитектуре JaguarDB.

## i.	Есть ли для вашей СУБД понятие «план запросов»? Если да, объясните, как работает данный этап.
Да, в СУБД JaguarDB также существует понятие "план запроса" (query plan), которое играет важную роль в оптимизации выполнения запросов и обеспечении эффективности работы системы. План запроса представляет собой стратегию выполнения запроса, которая определяется оптимизатором запросов и определяет, каким образом данные будут извлечены и обработаны для удовлетворения запроса.

## j.	Поддерживаются ли транзакции в вашей СУБД? Если да, то расскажите о нем. Если нет, то существует ли альтернатива?
СУБД JaguarDB поддерживает транзакции.
В JaguarDB транзакции реализованы с помощью механизма журнализации (logging). При выполнении операций в рамках транзакции все изменения данных записываются в журнал транзакций (transaction log) до их фактической фиксации (commit). Этот журнал позволяет восстановить состояние данных в случае сбоя системы или отката транзакции.

## k. Какие методы восстановления поддерживаются в вашей СУБД. Расскажите о них?
В СУБД JaguarDB поддерживаются следующие методы восстановления данных:
1. Восстановление с использованием журнала транзакций (Transaction Log Recovery): JaguarDB использует журнал транзакций для восстановления данных до последней зафиксированной транзакции. Этот метод позволяет восстановить целостность данных после сбоев системы.

2. Восстановление с использованием резервных копий (Backup and Restore): JaguarDB поддерживает создание и восстановление резервных копий базы данных. При необходимости можно восстановить данные из предварительно созданных резервных копий.

## l.	Расскажите про шардинг в вашей конкретной СУБД. Какие типы используются? Принцип работы.
JaguarDB поддерживает следующие типы шардинга:

1. Шардинг по ключу (Key-Based Sharding): Данные разделяются на шарды на основе значения определенного ключа. Каждый шард ответственен за определенный диапазон значений ключа, что позволяет равномерно распределять нагрузку на узлы и улучшать параллелизм обработки запросов.

2. Шардинг по диапазону (Range-Based Sharding): Данные разбиваются на шарды на основе определенного диапазона значений ключей. Этот тип шардинга позволяет эффективно работать с упорядоченными данными и уменьшить количество операций перемещения данных между шардами.

Принцип работы шардинга в JaguarDB заключается в том, что каждый шард содержит только часть данных, что позволяет распределить нагрузку на несколько узлов и повысить производительность системы. При выполнении запросов данные могут быть распределены между шардами в зависимости от ключа или диапазона значений, что обеспечивает балансировку нагрузки и оптимизацию доступа к данным.

## m.	Возможно ли применить термины Data Mining, Data Warehousing и OLAP в вашей СУБД?
JaguarDB поддерживает хранилища данных (Data Warehouses)\
JaguarDB позволяет проводить анализ данных (Data Mining)\
СУБД JaguarDB поддерживает OLAP


## n.	Какие методы защиты поддерживаются вашей СУБД? Шифрование трафика, модели авторизации и т.п.
В JaguarDB реализовано несколько методов защиты, сюда входят: шифрование трафика, аудит доступа, модели авторизации.


## o.	Какие сообщества развивают данную СУБД? Кто в проекте имеет права на коммит и создание дистрибутива версий? Расскажите об этих людей и/или компаниях?
Как упоминалось ранее, DataJaguar — это стартап из Кремниевой долины, компания UStartX.


## p.	Создайте свои собственные данные для демонстрации работы СУБД. 
```js
create store products ( key: 
    product_id int, value: name char(32),
    price DECIMAL(10, 2),
    quantity INT
);
```

```js
create store user ( key: name char(32),
 value: age int, address char(128), rdate date );
```
```js
 insert into user ( fname, lname, age ) values ( 'David', 'Doe', 30 );
 insert into user ( fname, lname, age, addr ) values ( 'Larry', 'Lee', 40,
'123 North Ave., CA' );
```


## r.	Где найти документацию и пройти обучение?
Документацию по JaguarDB можно найти на [сайте](http://www.jaguardb.com/windex.html). \
Так же на сайте есть подробное [руководство](http://www.jaguardb.com/doc/JaguarUserManual.pdf) на 232 страницы. \
К сожалению, не удалось найти ни одного курса по изучению JaguarDB.

## s.	Как быть в курсе происходящего
У JaguarDB есть официальный [YouTube-канал](https://www.youtube.com/@jaguardb), который содержит десять видео продолжительностью от одной до трёх минут. Первое видео было загружено девять месяцев назад, однако самое популярное из них собрало всего 59 просмотров.
