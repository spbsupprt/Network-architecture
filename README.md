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


![image](https://github.com/user-attachments/assets/fab951de-b778-4f82-be36-4cdff7cfd6ac)


Проверка пинга между хостами и разынми подсетями:

(192.168.2.130) - (192.168.1.2)
(192.168.0.2) - (192.168.2.130)
(192.168.0.2) - (192.168.1.2)

```
root@centralServer:~# ping -c2 192.168.2.130
PING 192.168.2.130 (192.168.2.130) 56(84) bytes of data.
64 bytes from 192.168.2.130: icmp_seq=1 ttl=62 time=3.80 ms
64 bytes from 192.168.2.130: icmp_seq=2 ttl=62 time=3.83 ms

--- 192.168.2.130 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 3.802/3.817/3.832/0.015 ms

root@centralServer:~# ping -c2 192.168.1.2
PING 192.168.1.2 (192.168.1.2) 56(84) bytes of data.
64 bytes from 192.168.1.2: icmp_seq=1 ttl=62 time=1.54 ms
64 bytes from 192.168.1.2: icmp_seq=2 ttl=62 time=4.13 ms

--- 192.168.1.2 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1003ms
rtt min/avg/max/mdev = 1.538/2.835/4.133/1.297 ms

root@office1Server:~# ping -c2 192.168.0.2
PING 192.168.0.2 (192.168.0.2) 56(84) bytes of data.
64 bytes from 192.168.0.2: icmp_seq=1 ttl=62 time=3.71 ms
64 bytes from 192.168.0.2: icmp_seq=2 ttl=62 time=4.12 ms

--- 192.168.0.2 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 3.706/3.910/4.115/0.204 ms

root@office1Server:~# ping -c2 192.168.1.2
PING 192.168.1.2 (192.168.1.2) 56(84) bytes of data.
64 bytes from 192.168.1.2: icmp_seq=1 ttl=61 time=2.16 ms
64 bytes from 192.168.1.2: icmp_seq=2 ttl=61 time=2.76 ms

--- 192.168.1.2 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 2.159/2.457/2.756/0.298 ms

root@office2Server:~# ping -c2 192.168.0.2
PING 192.168.0.2 (192.168.0.2) 56(84) bytes of data.
64 bytes from 192.168.0.2: icmp_seq=1 ttl=62 time=3.69 ms
64 bytes from 192.168.0.2: icmp_seq=2 ttl=62 time=3.91 ms

--- 192.168.0.2 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 3.685/3.796/3.908/0.111 ms

root@office2Server:~# ping -c2 192.168.2.130
PING 192.168.2.130 (192.168.2.130) 56(84) bytes of data.
64 bytes from 192.168.2.130: icmp_seq=1 ttl=61 time=1.87 ms
64 bytes from 192.168.2.130: icmp_seq=2 ttl=61 time=5.71 ms

--- 192.168.2.130 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 1.867/3.787/5.708/1.920 ms

```






