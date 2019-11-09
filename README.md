# Контейнеры Docker для разворачивания окружения под сайт на 1С Битрикс 

Контейнеры Docker для разворачивания окружения под сайт на 1С Битрикс ( Nginx + PHP-FPM 7.1 + Mysql 5.7 )

## Требования

Сервер с ОС CentOS 7 X64 и установленным на него docker

## Установка  и запуск Docker

yum install epel-release

### Обновляем систему и ПО

yum update -y

yum upgrade -y

### Перезапускаем сервер

reboot

### Устанавливаем Docker и запускаем его

yum install -y mc nano wget git docker docker-compose && chkconfig docker on && service docker restart

## Скачивание , сборка и запуск контейнеров

cd /ваша папка

git clone https://github.com/krutikov-vadim2016/bitrix-php-fpm7.1-mysql5.7.git

cd bitrix-php-fpm7.2-mysql5.7

chown -R 33:33 www tmp

### Запускаем контейнеры

docker-compose up -d
или
docker-compose up --build



###  Проверяем работоспособность и настраиваем сайт на битриксе

Сайт доступен по ссылке http://IP_SERVER

Установка битрикса http://IP_SERVER/bitrixsetup.php

Перенос готового сайта из бэкапа http://IP_SERVER/restore.php
### !!!После установки битрикса удалите скрипты restore.php и bitrixsetup.php если не удалил установщик

Данные к MySQL:
root / secret ( пароль прописывается в файле docker-compose.yml )

в качестве сервера подключения к БД указать mysql вместо localhost
