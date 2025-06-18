
# Домашнее задание к занятию 1.  «Оркестрация группой Docker контейнеров на примере Docker Compose» - Морозов Александр

## Задача 1

Сценарий выполнения задачи:
- Установите docker и docker compose plugin на свою linux рабочую станцию или ВМ.
- Если dockerhub недоступен создайте файл /etc/docker/daemon.json с содержимым: ```{"registry-mirrors": ["https://mirror.gcr.io", "https://daocloud.io", "https://c.163.com/", "https://registry.docker-cn.com"]}```
- Зарегистрируйтесь и создайте публичный репозиторий  с именем "custom-nginx" на https://hub.docker.com (ТОЛЬКО ЕСЛИ У ВАС ЕСТЬ ДОСТУП);
- скачайте образ nginx:1.21.1;
- Создайте Dockerfile и реализуйте в нем замену дефолтной индекс-страницы(/usr/share/nginx/html/index.html), на файл index.html с содержимым:
```
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I will be DevOps Engineer!</h1>
</body>
</html>
```
- Соберите и отправьте созданный образ в свой dockerhub-репозитории c tag 1.0.0 (ТОЛЬКО ЕСЛИ ЕСТЬ ДОСТУП). 
- Предоставьте ответ в виде ссылки на https://hub.docker.com/<username_repo>/custom-nginx/general .

Ответ:

Устанавливаем Docker и Docker Compose
![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/1.png)

Загружаем образ nginx:1.21.1
![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/2.png)

Собираем новый докер образ Nginx с новой html страницей
![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/3.png)

Загружаем полученный образ в dockerhub-репозитории
![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/4.png)

Ссылка на dockerhub-репозитории:
https://hub.docker.com/repository/docker/mars1211/custom-nginx/general


## Задача 2
1. Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:
- имя контейнера "ФИО-custom-nginx-t2"
- контейнер работает в фоне
- контейнер опубликован на порту хост системы 127.0.0.1:8080
2. Не удаляя, переименуйте контейнер в "custom-nginx-t2"
3. Выполните команду ```date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080  ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html```
4. Убедитесь с помощью curl или веб браузера, что индекс-страница доступна.

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

Ответ:
![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/5.png)

## Задача 3
1. Воспользуйтесь docker help или google, чтобы узнать как подключиться к стандартному потоку ввода/вывода/ошибок контейнера "custom-nginx-t2".
2. Подключитесь к контейнеру и нажмите комбинацию Ctrl-C.
3. Выполните ```docker ps -a``` и объясните своими словами почему контейнер остановился.
4. Перезапустите контейнер
5. Зайдите в интерактивный терминал контейнера "custom-nginx-t2" с оболочкой bash.
6. Установите любимый текстовый редактор(vim, nano итд) с помощью apt-get.
7. Отредактируйте файл "/etc/nginx/conf.d/default.conf", заменив порт "listen 80" на "listen 81".
8. Запомните(!) и выполните команду ```nginx -s reload```, а затем внутри контейнера ```curl http://127.0.0.1:80 ; curl http://127.0.0.1:81```.
9. Выйдите из контейнера, набрав в консоли  ```exit``` или Ctrl-D.
10. Проверьте вывод команд: ```ss -tlpn | grep 127.0.0.1:8080``` , ```docker port custom-nginx-t2```, ```curl http://127.0.0.1:8080```. Кратко объясните суть возникшей проблемы.
11. * Это дополнительное, необязательное задание. Попробуйте самостоятельно исправить конфигурацию контейнера, используя доступные источники в интернете. Не изменяйте конфигурацию nginx и не удаляйте контейнер. Останавливать контейнер можно. [пример источника](https://www.baeldung.com/linux/assign-port-docker-container)
12. Удалите запущенный контейнер "custom-nginx-t2", не останавливая его.(воспользуйтесь --help или google)

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

Ответ:

В режиме ввода/вывода/ошибок контейнера при нажатии Ctrl-C происходит завершение процесса запуска контейнера. Что и привело к остановке контейнера.
![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/6.png)

![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/7.png)

Мы изменили конфигурацию Nginx. В новой конфигурации Nginx слушает порт 81, вместо 80 ранее, и перенаправляет запрос на HTML страницу. Соответственно после перезапуска Nginx, внутри контейнера при обращении на порт 80 мы получаем ошибку, а при обращении на порт 81 видим HTML. 
![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/8.png)

При обращении на хост по порту 8080 который перенаправлял на порт 80 контейнера. Мы получаем ошибку. Так как Nginx контейнера больше не слушает порт 80.
![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/9.png)

Меняем конфиг контейнера, что бы восстановить работоспособность сайта
![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/10.png)

![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/11.png)

![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/12.png)

Удаляем контейнер
![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/13.png)


## Задача 4


- Запустите первый контейнер из образа ***centos*** c любым тегом в фоновом режиме, подключив папку  текущий рабочий каталог ```$(pwd)``` на хостовой машине в ```/data``` контейнера, используя ключ -v.
- Запустите второй контейнер из образа ***debian*** в фоновом режиме, подключив текущий рабочий каталог ```$(pwd)``` в ```/data``` контейнера. 
- Подключитесь к первому контейнеру с помощью ```docker exec``` и создайте текстовый файл любого содержания в ```/data```.
- Добавьте ещё один файл в текущий каталог ```$(pwd)``` на хостовой машине.
- Подключитесь во второй контейнер и отобразите листинг и содержание файлов в ```/data``` контейнера.

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

Ответ:

![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/14.png)

![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/15.png)


## Задача 5

1. Создайте отдельную директорию(например /tmp/netology/docker/task5) и 2 файла внутри него.
"compose.yaml" с содержимым:
```
version: "3"
services:
  portainer:
    network_mode: host
    image: portainer/portainer-ce:latest
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```
"docker-compose.yaml" с содержимым:
```
version: "3"
services:
  registry:
    image: registry:2

    ports:
    - "5000:5000"
```

И выполните команду "docker compose up -d". Какой из файлов был запущен и почему? (подсказка: https://docs.docker.com/compose/compose-application-model/#the-compose-file )

2. Отредактируйте файл compose.yaml так, чтобы были запущенны оба файла. (подсказка: https://docs.docker.com/compose/compose-file/14-include/)

3. Выполните в консоли вашей хостовой ОС необходимые команды чтобы залить образ custom-nginx как custom-nginx:latest в запущенное вами, локальное registry. Дополнительная документация: https://distribution.github.io/distribution/about/deploying/
4. Откройте страницу "https://127.0.0.1:9000" и произведите начальную настройку portainer.(логин и пароль адмнистратора)
5. Откройте страницу "http://127.0.0.1:9000/#!/home", выберите ваше local  окружение. Перейдите на вкладку "stacks" и в "web editor" задеплойте следующий компоуз:

```
version: '3'

services:
  nginx:
    image: 127.0.0.1:5000/custom-nginx
    ports:
      - "9090:80"
```
6. Перейдите на страницу "http://127.0.0.1:9000/#!/2/docker/containers", выберите контейнер с nginx и нажмите на кнопку "inspect". В представлении <> Tree разверните поле "Config" и сделайте скриншот от поля "AppArmorProfile" до "Driver".

7. Удалите любой из манифестов компоуза(например compose.yaml).  Выполните команду "docker compose up -d". Прочитайте warning, объясните суть предупреждения и выполните предложенное действие. Погасите compose-проект ОДНОЙ(обязательно!!) командой.

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод, файл compose.yaml , скриншот portainer c задеплоенным компоузом.


Ответ:

При наличие разных файлов docker compose, первым по умолчанию запускается файл compose.yaml
![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/16.png)

Редактируем файл compose.yaml, что бы при запуске docker compose запуск происходил из всех файлов
![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/17.png)

![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/18.png)

Производим первоначальную настройку portainer
![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/21.png)

Деплоим новый компоуд для образа custom-nginx
![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/22.png)

![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/23.png)

inspect контейнера nginx
![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/24.png)

Выполнение команды "docker compose up -d" с отсутствующим файлом compose.yaml. Вывел предупреждение то что запущенный контейнер portainer отсутствует в манифесте docker-compose.yaml. 
Используя атрибут --remove-orphans к команде "docker compose up -d". Удаляет несоответсвующие контейнеры манифесту.
![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/25.png)

При удалении проекта docker compose у нас продолжает работать контейнер nginx, т.к. этот контейнер не относится к проету
![alt text](https://github.com/Mars12121/devops-netology/blob/main/05-virt-03-docker-intro/img/26.png)



---

### Правила приема

Домашнее задание выполните в файле readme.md в GitHub-репозитории. В личном кабинете отправьте на проверку ссылку на .md-файл в вашем репозитории.