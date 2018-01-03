# Ansible-djangobb

Настройка стека:
djangobb(virtualenv)+mysql+uwsgi+nginx+supervisor+tor


### Первоначальная настройка:

Генерация ключа, добавление публичного ключа на удаленный хост
```bash
$ ssh-keygen
$ ssh-copy-id root@REMOTE_HOST_IP
```
Где REMOTE_HOST_IP - адрес удаленного хоста


### Запуск установки djangobb

`ansible-playbook web.yml`

После установки создается отчет. Файл `report.txt`

Пароль пользователя генерируется случайно при первом вызове и сохраняется в 

`credentials/{{ inventory_hostname }}/userpass`

## Отчет об установке

Сгенерировать `report.txt` без вызова "лишних" тасков можно следующей командой:


`ansible-playbook web.yml --tags report`

В отчет попадают следующие данные:
1. Логин\пароль пользователя
2. Логин\пароль админа djangobb
3. Логин\пароль базы mysql
4. Имя onion домена
5. Приватный ключ домена
6. Внешний ipv4 адрес сервера
7. Список портов которые слушаются на внешнем интерфейсе(0.0.0.0)

## Теги

`nginx` - обновление настроек nginx. 

`uwsgi` - обновление настроек uwsgi

`supervisor` - обновление настроек supervisor

`tor` - обновление настроек tor

`mysql` - создание пользователя и базы

`django_admin` - создание суперюзера djangobb 
