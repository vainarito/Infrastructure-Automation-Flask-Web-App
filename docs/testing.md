# Инструкция для тестирования

## Предварительные условия

- Установлен Ansible 2.9+
- Установлен Vagrant и VirtualBox (для локального тестирования)
- Доступ к серверу с правами sudo

## Быстрое тестирование с Vagrant

1. Запустить виртуальную машину:
   ```bash
   vagrant up
   ```
2. Запустить Ansible playbook для развертывания инфраструктуры:
   ```bash
   ansible-playbook -i inventory.ini playbook.yml
   ```
3. Проверить доступность сервера:
   - Открыть в браузере: http://localhost:8080
   - Должна отобразиться страница авторизации Flask-приложения

## Проверка компонентов

### Тест 1: Веб-приложение

1. После развертывания инфраструктуры убедиться, что веб-приложение доступно по HTTP:
   - Открыть браузер и перейти по адресу http://localhost:8080 или http://test.local
   - Должна отобразиться страница авторизации
   - Попробовать создать пользователя и выполнить вход

### Тест 2: Логи и мониторинг

1. Проверить логи приложения:
   ```bash
   vagrant ssh
   sudo cat /var/log/flask.log
   ```
   - Убедиться, что в логах есть записи о запусках приложения и запросах

2. Проверить логи мониторинга:
   ```bash
   sudo cat /var/log/system_monitor.log
   sudo cat /var/log/system_metrics.log
   ```
   - Убедиться, что скрипты выполняются и записывают информацию

### Тест 3: Резервное копирование

1. Проверить каталог с резервными копиями базы данных:
   ```bash
   ls -la /home/devops/backups/
   ```
   - Убедиться, что файлы бэкапов создаются с указанием даты и времени

### Тест 4: Ротация логов

1. Проверить конфигурацию logrotate:
   ```bash
   sudo cat /etc/logrotate.d/app_logs
   sudo logrotate -d /etc/logrotate.d/app_logs
   ```
   - Убедиться , что конфигурация корректна и логи будут ротироваться

### Тест 5: Docker-режим

1. Изменить переменную `use_docker` в playbook.yml:
   ```yaml
   use_docker: true
   ```

2. Запустить playbook:
   ```bash
   ansible-playbook -i inventory.ini playbook.yml
   ```

3. Проверить, что контейнеры запущены:
   ```bash
   vagrant ssh
   docker ps
   ```
   - Должны быть запущены контейнеры для Flask-приложения и Nginx

4. Проверить  доступность веб-приложения через Docker:
   - Открыть в браузере: http://localhost:8080

## Устранение неполадок

1. Если веб-приложение недоступно:
   ```bash
   sudo systemctl status nginx
   sudo systemctl status flask-app
   ```

2. Для проверки портов:
   ```bash
   sudo netstat -tuln | grep -E '80|5000'
   ```

3. Проверка логов:
   ```bash
   sudo tail -f /var/log/flask.log
   sudo tail -f /var/log/nginx/error.log
   ```