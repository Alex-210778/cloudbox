# ☁️ CloudBox

CloudBox — это учебный проект облачного хранилища с микросервисной архитектурой, в котором реализованы:

- Загрузка, скачивание и удаление файлов
- Авторизация и управление ролями через Keycloak
- Kafka для событий (загрузка, экспорт, уведомления)
- Redis для кэширования
- MinIO для хранения файлов
- Telegram-бот для уведомлений
- REST API (Swagger/OpenAPI)
- Возможность расширения с помощью AI (анализ и генерация на основе файлов)

---

## 📦 Структура репозитория

```
cloudbox/
├── docker/                  # Docker Compose инфраструктура
├── gateway-service/         # Spring Cloud Gateway
├── auth-service/            # Keycloak (внешний)
├── user-service/            # Управление пользователями
├── file-service/            # Загрузка/скачивание файлов, MinIO
├── export-service/          # Экспорт файлов/отчётов
├── ai-service/              # Интеграция с AI (в будущем)
├── notification-service/    # Telegram бот и email
├── audit-service/           # Логирование действий
├── frontend/                # React + Tailwind
└── README.md
```

---

## 🚀 Быстрый старт

### Требования:
- Docker + Docker Compose
- JDK 21
- Maven или Gradle

### 1. Клонируй репозиторий

```bash
git clone https://github.com/Alex-210778/cloudbox.git
cd cloudbox
```

### 2. Запусти инфраструктуру

```bash
cd docker
docker compose up -d
```

🔹 Чтобы проверить, всё ли работает:

```bash
docker ps                     # Проверка, что контейнеры запущены
docker compose logs -f        # Просмотр логов всех сервисов
docker compose down           # Остановить контейнеры
```

⏱ Первый запуск может занять несколько минут.

---

### 3. Проверь доступность сервисов

| Сервис      | URL                          | Доступ                          |
|-------------|------------------------------|---------------------------------|
| Keycloak    | http://localhost:8080        | `admin` / `admin`               |
| MinIO       | http://localhost:9001        | `minio` / `minio123`           |
| PostgreSQL  | `localhost:5432`             | `cloudbox` / `cloudbox`        |
| Kafka       | `kafka:9092`                 | (используется внутри сервисов) |
| Redis       | `localhost:6379`             | —                               |

---

## 🔐 Авторизация и роли

Настраивается через Keycloak:

- Realm: `cloudbox`
- Роли: `admin`, `user`, `readonly`
- Клиенты:
    - `cloudbox-frontend` (PKCE)
    - `cloudbox-backend` (client credentials)

⚠️ Файл импорта realm будет добавлен позже.

---

## 🧩 MVP микросервисы

| Сервис         | Назначение                        |
|----------------|-----------------------------------|
| Gateway        | Точка входа, маршрутизация        |
| User Service   | CRUD пользователей, роли          |
| File Service   | Работа с файлами, MinIO           |
| Export Service | Экспорт файлов и метаданных       |
| Notification   | Уведомления: Telegram/email       |
| Audit Service  | Логирование действий              |

---

## 📌 Планы на будущее

- Интеграция с AI (рефераты, поиск по содержимому)
- Распознавание текста (OCR)
- Генерация описаний файлов
- Поддержка WebSockets
- Мониторинг через Prometheus + Grafana

---

## 🛠️ Разработка и вклад

Проект создаётся с целью прокачки Java-скиллов.  
Frontend часть разрабатывается на React, backend — Java 21 + Spring Boot.
