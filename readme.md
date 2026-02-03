Автоматизация подготовки Ubuntu сервера под продакшен развертывания микросервисов с помощью **ansible**, **docker**
В рамках выполненной части задания реализованы:

- Базовая подготовка VM (ubuntu server + ssh)
- Управление доступом: группы/пользователи/ssh-keys/sudo
- Установка Docker CE, Docker-compose plugin, автозапуск Docker, запуск Docker без sudo для разработчиков
- Развертывание Nexus repository manager в Docker и получение initial admin password для входа в UI

---

## Используемые технологии ##

- Ansible - декларативная автоматизация конфигураций сервера
- Docker CE + Docker-compose plugin - стандарт для запуска микросервисов и инфрастуктурных сервисов
- Nexus repository manager - популярное хранилище артефактов

## Архитектура ##

- Control machine: Git-репозиторий + python venv + ansible, выполняющие подключение по ssh
- Target VM: настраивается ansible ролями: 
    - users - группы/пользователи/ssh-keys/sudo
    - docker - Docker CE + compose plugin + автозапуск + группы
    - nexus mirror - запуск Nexus в Docker, ожидание готовности, сохранение initial admin password

## Требования ##
### Control Machine
- Ubuntu
- Python 3
- Git
- SSH client

### Virtual Machine (target)
- Ubuntu Server 24.04.3 LTS
- Включен OpenSSH server
- Доступ по сети (bridged/NAT+проброс портов)

## Скриншоты ##

В папке screenshots находятся скриншоты промежуточных результатов: 
- devops1.png: admin1 выполняет sudo без пароля, developer1 не может выполнить sudo
- devops2.png: Docker запущен, developer1 выполняет docker ps без sudo
- devops3.png: Успешный вход в NexusUI (страница после логина)

