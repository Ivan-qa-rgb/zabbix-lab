[![Zabbix](https://img.shields.io/badge/Zabbix-Download-DC2D27?style=for-the-badge&logo=zabbix&logoColor=white)](https://www.zabbix.com/download)
# Zabbix Lab

Проект по мониторингу на базе Zabbix, развернутый через Docker Compose на Ubuntu.  
Показывает полный цикл: сбор метрик, настройку триггеров и проверку алертинга в локальной воспроизводимой среде.

---

## Основные моменты

- Развертывание через Docker Compose с изолированными сервисами.
- Мониторинг Ubuntu-хоста через Zabbix agent.
- Кастомный триггер по порогу загрузки CPU для проверки алертинга.
- Постоянное хранение данных и конфигурации в MySQL.
- Наглядные артефакты мониторинга в интерфейсе Zabbix.

---

## Архитектура

| Компонент | Роль | Порт |
|-----------|------|------|
| Zabbix Server | Собирает метрики с агентов | 10051 |
| Zabbix Web | Nginx frontend и дашборды | 8080 |
| MySQL 8.0 | Хранит метрики и конфигурацию | — |
| Zabbix Agent | Мониторимый Ubuntu-хост | 10050 |

---

## Быстрый старт

```bash
git clone https://github.com/Ivan-qa-rgb/zabbix-lab.git
cd zabbix-lab
docker-compose up -d
```

Откройте [http://localhost:8080](http://localhost:8080).  
Логин: `Admin`  
Пароль: `zabbix`

---

## Что настроено

| Параметр | Значение |
|---------|-------|
| Хост | Ubuntu |
| Шаблон | Linux by Zabbix agent |
| Элементы данных | 73 (CPU, Memory, Disk, Network, Processes) |
| Триггеры | 35 всего, 1 кастомный |
| Кастомный триггер | Загрузка CPU выше 75% → Warning |

---

## Скриншоты

| Метрика | Просмотр | Примечание |
|--------|---------|-------|
| Доступность хоста | [View](https://github.com/Ivan-qa-rgb/zabbix-lab/blob/main/screenshots/hosts.png) | Агент ZBX зеленый, хост онлайн |
| Использование CPU | [View](https://github.com/Ivan-qa-rgb/zabbix-lab/blob/main/screenshots/cpu.png) | ~100% загрузка, виден кастомный триггер |
| Использование памяти | [View](https://github.com/Ivan-qa-rgb/zabbix-lab/blob/main/screenshots/memory.png) | ~23% использования, базовый триггер |

---

## Акцент проекта

- Оркестрация через Docker Compose с постоянным хранилищем.
- Автоподключение Zabbix agent и active checks.
- Проектирование выражения триггера и настройка severity.
- Практическая схема мониторинга для небольшой инфраструктуры.

---

## Технологии

- Zabbix 7.0 LTS
- Docker и Docker Compose
- MySQL 8.0
- Ubuntu 22.04

---
