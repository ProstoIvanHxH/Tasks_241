# Открываем firewald

1. Удалите iptables и установите firewalld

sudo apt-get remove iptables 
sudo apt-get install firewalld -y

2. Попробуйте так-же проверить возможность подключения по ssh

ssh username@server_ip

3. Если её нет то откройте порт

firewall-cmd --add-port=22/tcp --permanent

4. Выведите список открытых портов с помощью firewall-cmd

firewall-cmd --list-all

5. Можно ли там добавить порты по названию сервиса?

firewall-cmd --add-service=ssh --permanent

firewall-cmd --reload

6. На вашей Локальной виртуальной машине попробуйте подключиться к серверу samba из предыдущих заданий
7. Если не получилось то откройте нужные порты

firewall-cmd --add-port=123/tcp --permanent

9. Сделайте так чтобы изменения были постоянными

systemctl restart firewalld
