# Пишем юниты

1. Создайте скрипт который создаёт папку заполняет её файлами ( имена 1-4 ) и записывает в них информацию
о текущей дате, версии ядра, имени компьютера и списе всех файлов в домашнем каталоге пользователя от которого выполняется скрипт( не забудьте сдлеать проверку на существование файлов и папок)
```sh
#!/bin/bash
set -euo pipefail
DIR_NAME="$HOME/folder"

if [ ! -d "$DIR_NAME" ]; then
    mkdir "$DIR_NAME"
    echo "Папка создана"
else
    echo "Папка уже создана"
fi

for i in {1..4}; do
    if [ ! -f "$DIR_NAME/$i" ]; then
        touch $DIR_NAME/$i
        echo "Файл $i создан"
        if [ "$i" == 1 ]; then
             date > $DIR_NAME/1
        elif [ "$i" == 2 ]; then
             cat /proc/version > $DIR_NAME/2
        elif [ "$i" == 3 ]; then
             hostname > $DIR_NAME/3
        else
             ls -la > $DIR_NAME/4
    fi
    else
        echo "Файл $i уже существует"
fi
done 
```
2. Создайте юнит который будет вызывать этот скрипт при запуске. Проверьте
```sh
[Unit]
Description = unit

[Service]
ExecStart=/home/systemd-script
User=test
Type=oneshot
WorkingDirectory=/home/test

[Install]
WantedBy=multi-user.target
```
3. Создайте таймер который будет вызывать выполнение одноимённого systemd юнита каждые 5 минут.
```sh
[Unit]
Description=timer

[Timer]
OnBootSec=0
OnUnitActiveSec=5m

[Install]
WantedBy=timers.target
```
4. От какого пользователя вызыаются юниты поумолчанию?

root

5. Создайте пользователя от имени которого будет выполняться ваш скрипт.

sudo useradd tester

6. Дополните юнит информацией о пользователе от которого должен выплняться скрипт.
```sh
[Unit]
Description=unit
[Service]
User=tester
ExecStart=/path/to/your/script.sh
[Install]
WantedBy=multi-user.target
```
7. Дополните ваш скрипт так, что бы он независимо от местоположения всега выполнялся в домашней папке того кто его вызывает.
```sh
#!/bin/bash
cd $HOME
```
