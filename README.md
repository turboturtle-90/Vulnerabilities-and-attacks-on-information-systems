# Домашнее задание к занятию «Уязвимости и атаки на информационные системы» - `Смирнов Максим`

### Задание 1

-Какие сетевые службы разрешены?
-Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)

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

### Задание 2

`Ссылка на .cfg`

https://github.com/turboturtle-90/Homework_clustering_and_load_balancing/blob/593b469a59cef8dcb0deedeb24426b0453281f6e/haproxy.cfg-assignment2 

`Балансировка на 7 уровне по roubdrobin с весовыми множителями и обработкой только при адресации к домену example.com`
![2-weighted-level7.jpg](https://github.com/turboturtle-90/Homework_clustering_and_load_balancing/blob/593b469a59cef8dcb0deedeb24426b0453281f6e/2-weighted-level7.jpg)


`Текст конфига /etc/haproxy/haproxy.cfg в части балансировки roundronib на 7 уровне приведен ниже :`

```                                                         
frontend example  # секция фронтенд
        mode http
        bind :8088
        #default_backend web_servers
        acl ACL_example.com hdr(host) -i example.com
        use_backend web_servers if ACL_example.com

backend web_servers    # секция бэкенд
        mode http
        balance roundrobin
        option httpchk
        http-check send meth GET uri /index.html
        server s1 127.0.0.1:8888 check weight 2
        server s2 127.0.0.1:9999 check weight 3
        server s3 127.0.0.1:9999 check weight 4
```
---
