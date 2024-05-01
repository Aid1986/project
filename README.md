# Задание 1
![1](https://github.com/Aid1986/project/blob/main/Снимок%20экрана%202024-05-01%20000845.png)

# Задание 2

#!/bin/bash

# Проверка доступности порта веб-сервера
if nc -z -v -w5 127.0.0.1 80; then
    echo "Порт веб-сервера доступен"
else
    echo "Порт веб-сервера недоступен"
    exit 1
fi

# Проверка существования файла index.html
if [ -f /www/html/index.html ]; then
    echo "Файл index.html существует"
else
    echo "Файл index.html отсутствует"
    exit 1
fi



vrrp_instance VI_1 {
        state MASTER
        interface ens33
        virtual_router_id 15
        priority 255
        advert_int 1

        virtual_ipaddress {
              192.168.111.15/24
        }

        track_script {
            check_webserver
        }
}

vrrp_script check_webserver {
    script "/path/to/check_webserver.sh"
    interval 3
    fall 2
    rise 1
}



vrrp_instance VI_1 {
        state BUCKAP
        interface ens33
        virtual_router_id 15
        priority 100
        advert_int 1

        virtual_ipaddress {
              192.168.111.15/24
        }

        track_script {
            check_webserver
        }
}

vrrp_script check_webserver {
    script "/path/to/check_webserver.sh"
    interval 3
    fall 2
    rise 1
}


![2-2](https://github.com/Aid1986/project/blob/main/2-2.png)

![2-3](https://github.com/Aid1986/project/blob/main/2-3.png)

![2](https://github.com/Aid1986/project/blob/main/2.png)

![2-1](https://github.com/Aid1986/project/blob/main/2-1.png)
