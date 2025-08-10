# TaskHub Frontend

React приложение для управления задачами с автоматической сборкой и развертыванием через GitHub CI/CD.

## 🚀 Быстрый старт

### Локальная разработка

```bash
# Установка зависимостей
npm install

# Запуск в режиме разработки
npm start

# Запуск тестов
npm test

# Сборка для продакшена
npm run build
```

### Docker (продакшен)

```bash
# Сборка и запуск продакшен образа
docker-compose up

# Только сборка
docker build -t taskhub-frontend .
```

### Docker (разработка)

```bash
# Запуск в режиме разработки с hot reload
docker-compose --profile dev up taskhub-frontend-dev
```

## 🔧 GitHub CI/CD

Проект настроен для автоматической сборки и развертывания через GitHub Actions:

### Workflows

1. **Test and Quality Check** - тестирование и проверка качества кода
2. **Build and Push Docker Image** - сборка и публикация Docker образа в GitHub Packages
3. **Deploy Application** - автоматическое развертывание (требует настройки)

### Автоматические триггеры

- **Push** в ветки `main` или `develop` - запуск тестов и сборка Docker образа
- **Pull Request** в ветки `main` или `develop` - запуск тестов
- **Теги** `v*` - релиз с публикацией Docker образа

### Docker образы

Docker образы автоматически публикуются в GitHub Container Registry:

- **Latest**: `ghcr.io/{username}/taskhub-frontend:latest`
- **По веткам**: `ghcr.io/{username}/taskhub-frontend:{branch-name}`
- **По тегам**: `ghcr.io/{username}/taskhub-frontend:{version}`

## 📦 Структура проекта

```
taskhub-frontend/
├── .github/workflows/     # GitHub Actions workflows
├── components/            # React компоненты
├── src/                  # Исходный код
├── public/               # Статические файлы
├── Dockerfile            # Docker для продакшена
├── Dockerfile.dev        # Docker для разработки
├── docker-compose.yml    # Docker Compose конфигурация
├── nginx.conf            # Nginx конфигурация
└── package.json          # Зависимости и скрипты
```

## 🌐 Nginx конфигурация

Включает:
- Gzip сжатие
- Кэширование статических файлов
- Поддержка React Router (SPA)
- Health check endpoint
- API проксирование (настраивается)

## 🔒 Безопасность

- Docker образы запускаются от непривилегированного пользователя
- Многоэтапная сборка для минимизации размера образа
- Исключение чувствительных файлов через `.dockerignore`

## 📋 Требования

- Node.js 18+
- Docker 20.10+
- Docker Compose 2.0+

## 🚀 Развертывание

### GitHub Packages

Docker образы автоматически публикуются в GitHub Container Registry при каждом push в main ветку.

### Ручное развертывание

```bash
# Скачать образ
docker pull ghcr.io/{username}/taskhub-frontend:latest

# Запустить контейнер
docker run -p 80:80 ghcr.io/{username}/taskhub-frontend:latest
```

### Kubernetes

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: taskhub-frontend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: taskhub-frontend
  template:
    metadata:
      labels:
        app: taskhub-frontend
    spec:
      containers:
      - name: taskhub-frontend
        image: ghcr.io/{username}/taskhub-frontend:latest
        ports:
        - containerPort: 80
        resources:
          requests:
            memory: "64Mi"
            cpu: "250m"
          limits:
            memory: "128Mi"
            cpu: "500m"
```

## 🤝 Вклад в проект

1. Fork репозитория
2. Создайте feature ветку (`git checkout -b feature/amazing-feature`)
3. Commit изменения (`git commit -m 'Add amazing feature'`)
4. Push в ветку (`git push origin feature/amazing-feature`)
5. Откройте Pull Request

## 📄 Лицензия

Этот проект лицензирован под MIT License.
