
# Шарим


1. Установите пакет samba

sudo apt-get install samba

2. ЧТо такое побщая папка, зачем оно может быть нужно?

Это директория, доступная для нескольких пользователей или устройств в сети. Она позволяет обмениваться файлами, работать с документами совместно или предоставлять общий доступ к данным.

3. Создайте общую папку без пароля с правами только на чтение файлов
```sh
sudo mkdir /media/samba/public
sudo chmod -R 0755 /media/samba/public
sudo chown -R nobody:nogroup /media/samba/public
sudo nano /etc/samba/smb.conf
```
```sh
[public]
  path = /media/samba/public
  browseable = yes
  writable = no
  guest ok = yes
  read only = yes
```
4. Создайте общую папку с паролем с правами на чтение и запись
```sh
sudo mkdir /media/samba/private
sudo chmod -R 0770 /media/samba/private
sudo chown -R username:groupname /media/samba/private
sudo smbpasswd -a username
sudo nano /etc/samba/smb.conf
```
```sh
[private]
  path = /media/samba/private
  browseable = yes
  writable = yes
  guest ok = no
  valid users = username
```
5. Создайте общую папку с доступом для какой-то группы с полными правами
```sh
sudo mkdir /media/samba/group_share
sudo chmod -R 0770 /media/samba/group_share
sudo chown -R groupname:groupname /media/samba/group_share
sudo nano /etc/samba/smb.conf
```
```sh
[group_share]
  path = /media/samba/group_share
  browseable = yes
  writable = yes
  guest ok = no
  valid users = @groupname
```
6. Создайте общую папку в которой у одной группы будет полный доступ, а у другой только доступ на чтение.
Третья группа не должна иметь к ней доступа
```sh
sudo mkdir /media/samba/multi_group_share
sudo chmod -R 0770 /media/samba/multi_group_share
sudo chown -R full_access_group:full_access_group /media/samba/multi_group_share
sudo nano /etc/samba/smb.conf
```
```sh
[multi_group_share]
  path = /media/samba/multi_group_share
  browseable = yes
  writable = yes
  guest ok = no
  valid users = @full_access_group @read_only_group
  read list = @read_only_group
  write list = @full_access_group
```
