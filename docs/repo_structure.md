# Структура репозитория

```
task1-infrastructure/
├── docs/                   # Документация проекта
│   ├── architecture.md     # Архитектурная схема и описание
│   ├── images/             # Изображения для документации
│   │   └── architecture_diagram.png  # Диаграмма архитектуры
│   ├── repo_structure.md   # Структура репозитория
│   └── testing.md          # Инструкция по тестированию
├── group_vars/             # Групповые переменные для Ansible
├── README.md               # Основная документация
├── Vagrantfile             # Конфигурация вирьуальной машины
├── inventory.ini           # Инвентарь Ansible
├── playbook.yml            # Основной плейбук Ansible
└── roles/                  # Роли Ansible
    └── infrastructure/     # Основная роль для настройки инфраструктуры
        ├── defaults/       # Переменные по умолчанию
        │   └── main.yml    # Определение переменных
        ├── files/          # Статчиеские файлы
        ├── handlers/       # Обработчики событий
        │   └── main.yaml   # Определение обработчиков (restart services)
        ├── tasks/          # Задачи роли
        │   └── main.yml    # Основные задачи по настройке
        ├── templates/      # Шаблоны Jinja2
        │   ├── app_logs.j2             # Конфигурация logrotate
        │   ├── docker-compose.yml.j2   # Конфиг для Docker Compose
        │   ├── Dockerfile.j2           # Шаблон Dockerfile
        │   ├── flask-app.service.j2    # Systemd сервис
        │   ├── nginx.conf.j2           # Конфигурация Nginx
        │   ├── setup_and_monitor.sh.j2 # Скрипт мониторинга и бэкапа
        │   └── system_metrics.sh.j2    # Скрипт сбора метрик
        └── vars/           # Переменные роли
            └── main.yml    # Опредлеление переменных
```

## Назначение файлов

### Основные файлы

- **README.md**: Основная документация проекта
- **inventory.ini**: Список серверов для Ansible
- **playbook.yml**: Основной Ansible-плейбук
- **Vagrantfile**: Конфигурация тестовой виртуальной машины

### Роль infrastructure

- **defaults/main.yml**: Переменные по умолчанию (пути, настройки)
- **handlers/main.yaml**: Обработчики для перезапуска сервисов
- **tasks/main.yml**: Задачи по настройке инфраструктуры
- **templates/**: Шаблоны конфигурационных файлов и скриптов
- **vars/main.yml**: Переменные с более высоким приоритетом

### Документация

- **docs/architecture.md**: Описание архитектуры системы
- **docs/testing.md**: Инструкции по тестированию
- **docs/repo_structure.md**: Описание структуры репозитория
- **docs/images/**: Каталог для хранения изображений

---
