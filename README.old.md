# TaskHub Frontend

Минималистичный веб-интерфейс для TaskHub backend сервиса.

## Быстрый старт

1. **Убедитесь, что backend запущен:**
   ```bash
   # В корне проекта
   ./mvnw spring-boot:run
   ```
   Backend должен быть доступен по адресу: `http://localhost:8080`

2. **Запустите frontend:**
   ```bash
   # Перейдите в папку frontend
   cd frontend
   
   # Запустите простой HTTP сервер (любой из вариантов):
   
   # Python 3
   python -m http.server 3000
   
   # Python 2
   python -m SimpleHTTPServer 3000
   
   # Node.js (если установлен)
   npx serve -p 3000
   
   # PHP (если установлен)
   php -S localhost:3000
   ```

3. **Откройте в браузере:**
   ```
   http://localhost:3000
   ```

## Функциональность

### ✅ Реализовано:
- 📋 **Просмотр задач** - отображение всех задач с backend
- ➕ **Создание задач** - форма для ручного создания задачи
- 🗑️ **Удаление задач** - кнопка удаления для каждой задачи
- 🤖 **AI Генерация** - создание задач через OpenRouter AI
- 🎨 **Responsive UI** - адаптивный интерфейс с Tailwind CSS
- 📱 **SPA Navigation** - переключение между разделами без перезагрузки

### 🔧 API Endpoints:
- `GET /api/v1/tasks` - получение всех задач
- `POST /api/v1/tasks` - создание новой задачи
- `DELETE /api/v1/tasks/{id}` - удаление задачи
- `POST /api/v1/tasks/generate` - генерация задачи через AI

## Структура файлов

```
frontend/
├── index.html              # Основная HTML страница
├── main.js                 # Главный JavaScript файл
├── components/
│   ├── TaskList.js         # Компонент списка задач
│   ├── TaskForm.js         # Компонент формы создания
│   └── TaskGenerator.js    # Компонент AI генерации
└── README.md              # Этот файл
```

## Технические детали

- **Стек:** Vanilla JavaScript + HTML + Tailwind CSS (CDN)
- **Модули:** ES6 modules
- **HTTP клиент:** Fetch API
- **Стили:** Tailwind CSS через CDN
- **Сборка:** Не требуется (работает напрямую в браузере)

## Возможные проблемы

### CORS ошибки
Если возникают CORS ошибки, убедитесь что в backend настроен правильный CORS для `http://localhost:3000`.

### Backend недоступен
Проверьте что backend запущен и отвечает:
```bash
curl http://localhost:8080/api/v1/tasks/ping
# Должен вернуть: pong
```

### Порт уже используется
Если порт 3000 занят, используйте другой:
```bash
python -m http.server 3001
# Затем откройте http://localhost:3001
```