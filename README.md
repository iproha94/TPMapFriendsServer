# Сервер для Android приложения [ссылка](https://github.com/Evgeny-Ivanov/MapFriends)

**Язык:** Java  
**База данных:** MySQL  

**Используемые технологии:**  
1. JDBC  
2. Jetty servlets  
3. Log4j  
4. Gson

**Описание для Android-разработчика:**  
*package com.wordpress.ilyaps.model; class Coor*  
он абстрактный, все поля есть *(id, longitude, latitude, date)* (*date* - родная для Java). Переопределить нужно два метода: *set* этой даты из типа полученной от базы данных , и *get* Даты в стиле базы данных для вставки в базу данных. 
Эти заморочки нужны, потому что мы используем разные базы данных, и формат даты для них специфический может быть.

При этом мы сериализуем и десериализуем объекты из Java, поэтому основной тип объекта должен быть типа родной Java (*java.util.Date*).   
Я создал класс *CoorMysql*. Тебе нужно будет создать класс *CoorLitesql* и работать и десериализовать/сериализовать его.  
В Mysql я использую тип *DataTime*. Если в твоей БД такой же тип, то можешь брать мой готовый *CoorMysql*.  

*package com.wordpress.ilyaps.message*
Для отправки данных из андроида в сервер, создаешь объект класса *DataMsg*, т.е. создал, сериализовал, отправил POST параметром */data-to-server*. Ответ придет также json, т.е. тебе нужно десериализовать объект класса *StatusMsg*.  
В нем есть поле - кол-во добавленных записей, мало ли нужно будет.  
Для получения данных от сервера в андроид тебе нужно создать объект класса *RequestDataMsg* и сериализованный отправляешь POST запосом на */data-from-server*, получаешь ответ json, который десериализуется в объект *DataAndStatusMsg*  

Для удобства реализованы *get* запросы указанных урлов.  
Пример:  
*http://localhost:8081/data-to-server?id=77&longitude=12&latitude=13*  
Особенность - дата выставится текущая и можно только одну запись за один запрос.  
*http://localhost:8081/data-from-server?id=77*
