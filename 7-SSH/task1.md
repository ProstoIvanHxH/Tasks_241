# Настриваем

1. Какой по умолчанию используется порт для поключения?

22

2. Можно ли его изменить? если да то как?

nano /etc/openssh/sshd_config

В файле изменить Port 22 на необходимый

4. Какая служба отвечает за обработку запросов на подключения по ssh?

sshd

5. Какой файл конфигурации отвечает за его настройку?

/etc/openssh/sshd_config

6. Попробуйте подключиться по ssh к предоставленному вам серверу

ssh -p 233 student@arzdez.ru

7. Отредактируйте файл настроек на сервере так, чтобы была возможность подключиться к серверу используя пользователя root

control sshd-permit-root-login enabled

8. Измените колличество ошибок ввода пароля перед сборосом соединения, покажите эти измененения

В sshd_config

MaxAuthTries= 2

10. Создайте пользователя ssh-user и попробуйте им подключиться к серверу

sudo adduser ssh-user

sudo passwd ssh-user

ssh -p 224 ssh-user@95.31.204.147

12. Ограничте ему возможность подключения к серверу

DenyUsers ssh-user

13. Как вы это сделали?

в sshd_config

DenyUsers ssh-user

15. Что хранится в файле known_hosts?

отпечатки всех серверов, которые вы посещаете что не позволяет сливать пароли и секретные ключи, если отпечаток не совпал.
