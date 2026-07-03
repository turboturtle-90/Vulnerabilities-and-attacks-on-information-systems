# Домашнее задание к занятию «Уязвимости и атаки на информационные системы» - `Смирнов Максим`

### Задание 1

-Какие сетевые службы разрешены?
-Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)

***

`При сканировании были выявлены следующие разрешенные службы:`
![allowed-serv.jpg](https://github.com/turboturtle-90/Vulnerabilities-and-attacks-on-information-systems/blob/a43be2f79d9376a56812219636aac2d967966578/allowed-serv.jpg)

Возможные уязвисимости:

1. vsftpd 2.3.4 - Backdoor Command Execution
   
``` 
https://www.exploit-db.com/exploits/49757
```


2. MySQL 5.0.x - Single Row SubSelect Remote Denial of Service
   
``` 
https://www.exploit-db.com/exploits/29724
```

3. Samba 3.5.11/3.6.3 - Remote Code Execution
   
``` 
https://www.exploit-db.com/exploits/37834
```
***
***

### Задание 2

Проведите сканирование Metasploitable в режимах SYN, FIN, Xmas, UDP.
Запишите сеансы сканирования в Wireshark.
Ответьте на следующие вопросы:

-Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?
-Как отвечает сервер?

***



С точки зрения сетевого трафика, разные режимы используют разные протоколы и разные пакеты.

SYN - работает по TCP и отправляет запрос на установку соединения. Сервер ответит в соотвествии с протоколом:
- если открыт придет ответ ACK
- если закрыт придет ответ RST, SYN

FIN - работает по TCP и отправляет запрос на закрытие соединения. Сервер ответит в соотвествии с протоколом:
- если открыт, ответа не будет. Запрос на закрытие соединения без собственно его открытия будет посчитан ошибочным и не вызовет никакого ответа
- если закрыт придет ответ RST

XMas - работает по TCP и отправляет запрос с несколькими флагами сразу. Сервер ответит в соотвествии с протоколом:
- если открыт, ответа не будет. Запрос с противоречивыми флагами будет посчитан ошибочным и не вызовет никакого ответа
- если закрыт придет ответ RST

UPD - работает по UPD и отправляет пакет данных. Сервер ответит в соотвествии с протоколом:
- порты TCP просто проигнорируют запрос
- если UDP открыт, служба сидящая на порту что-то ответит
- если закрыт придет ответ "destination unreachable"

Примеры логов Wireshark из тестового сканирования приведены ниже



`SYN ответ на открытый порт `

![SYN-OPEN.jpg](https://github.com/turboturtle-90/Vulnerabilities-and-attacks-on-information-systems/blob/ea06cc1c034bd8e18e07268c1b3b22500f843c55/SYN-OPEN.jpg)

`SYN ответ на закрытый порт `

![SYN-CLOSED.jpg](https://github.com/turboturtle-90/Vulnerabilities-and-attacks-on-information-systems/blob/ea06cc1c034bd8e18e07268c1b3b22500f843c55/SYN-CLOSED.jpg)

`FIN запрос на открытый порт - а ответа от него нет`

![FIN-OPEN-example.jpg](https://github.com/turboturtle-90/Vulnerabilities-and-attacks-on-information-systems/blob/ea06cc1c034bd8e18e07268c1b3b22500f843c55/FIN-OPEN-example.jpg)

`FIN ответ на закрытый порт `

![FIN-CLOSED-example.jpg](https://github.com/turboturtle-90/Vulnerabilities-and-attacks-on-information-systems/blob/ea06cc1c034bd8e18e07268c1b3b22500f843c55/FIN-CLOSED-example.jpg)

`XMas запрос на открытый порт - а ответа от него нет`

![XMS-OPEN.jpg](https://github.com/turboturtle-90/Vulnerabilities-and-attacks-on-information-systems/blob/ea06cc1c034bd8e18e07268c1b3b22500f843c55/XMS-OPEN.jpg)

`XMas ответ на закрытый порт `

![XMS-CLOSED.jpg](https://github.com/turboturtle-90/Vulnerabilities-and-attacks-on-information-systems/blob/ea06cc1c034bd8e18e07268c1b3b22500f843c55/XMS-CLOSED.jpg)

`UDP сканирование - ответы служб с портов 53 и 137, "destination unreachable" c остальных`

![UDP.jpg](https://github.com/turboturtle-90/Vulnerabilities-and-attacks-on-information-systems/blob/ea06cc1c034bd8e18e07268c1b3b22500f843c55/UDP.jpg)


---
