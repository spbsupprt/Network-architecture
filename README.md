# Network-architecture


Планируемая архитектура

построить следующую архитектуру

- Сеть office1

192.168.2.0/26 - dev
192.168.2.64/26 - test servers
192.168.2.128/26 - managers
192.168.2.192/26 - office hardware

- Сеть office2

192.168.1.0/25 - dev
192.168.1.128/26 - test servers
192.168.1.192/26 - office hardware

- Сеть central

192.168.0.0/28 - directors
192.168.0.32/28 - office hardware
192.168.0.64/26 - wifi



![image](https://github.com/user-attachments/assets/1edcb472-d9bf-4eab-bfbd-4d19ae52f005)


Итого должны получится следующие сервера

- inetRouter
- centralRouter
- office1Router
- office2Router
- centralServer
- office1Server
- office2Server

### Теоретическая часть:

- Найти свободные подсети

- Посчитать сколько узлов в каждой подсети, включая свободные

- Указать broadcast адрес для каждой подсети

- проверить нет ли ошибок при разбиении

### Практическая часть:

- Соединить офисы в сеть согласно схеме и настроить роутинг

- Все сервера и роутеры должны ходить в инет черз inetRouter

- Все сервера должны видеть друг друга

- у всех новых серверов отключить дефолт на нат (eth0), который вагрант поднимает для связи

- при нехватке сетевых интервейсов добавить по несколько адресов на интерфейс


---


### 1.Теоретическая часть:

Воспользуемся https://ip-calculator.ru/

И составим таблицу:

![image](https://github.com/user-attachments/assets/6bedabfb-04c1-43ce-87b8-54ea64cbc574)


Свободные сети:

192.168.0.16/28
192.168.0.48/28
192.168.0.128/25
192.168.255.64/26
192.168.255.32/27
192.168.255.16/28
192.168.255.8/29
192.168.255.4/30

---

### 2.Практическая часть:

Дано :

7 ненастроенных серверов.

![image](https://github.com/user-attachments/assets/97f219a3-f44c-4f21-bbde-97babc38b587)


Хотим привести к виду:

![image](https://github.com/user-attachments/assets/496d10a8-673a-4a4d-9a15-ea971548ab42)




Применяем плейбук 

https://github.com/spbsupprt/Network-architecture/blob/main/network.yml

















