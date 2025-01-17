# Журнальчики

1. Посмотретите журналы ssh

journalctl -u ssh

2. Выведите журналы в реальном времени

journalctl -fu ssh

3. Выведите лог в реальном времени для службы sshd

sudo journalctl -fu sshd

4. Можно ли без комады journalctl прочитать логи systemd?

да в директории /var/log

strings /var/log/journal/af4967d77fba44c6b093d0e9862f6ddd/system.journal | grep -i message


5. Сколько будет 2-2?

42
