     PZ6 Технологии индустриального программирования.  
     Студент: Выборнов О.А.  
     Группа: ЭФМО-02-25  
    
Цели работы: 
        
        -Понять, что такое ORM и чем удобен GORM.
        -Научиться описывать модели Go-структурами и автоматически создавать таблицы (миграции через AutoMigrate).
        -Освоить базовые связи: 1:N и M:N + выборки с Preload.
        -Написать короткий REST (2-3 ручки) для проверки результата.

Как запустить:

1)cклонировать репозиторий:

    git clone -b main --single-branch https://github.com/omnikk/PZ6.git

2)Через cmd командой "go run ."

Проверка здоровья  
    
    curl http://localhost:8081/health
<img width="665" height="439" alt="image" src="https://github.com/user-attachments/assets/515c3154-e941-4ace-9621-ad02e345538a" />

Создание пользователя
    
    curl -X POST http://localhost:8081/users \
      -H "Content-Type: application/json" \
      -d '{"name":"Alice","email":"alice@example.com"}'
<img width="1084" height="477" alt="image" src="https://github.com/user-attachments/assets/f5a4bd17-7fe4-48bc-9169-d37225d6a8cc" />


Создание заметки с тегами

    Invoke-WebRequest -Uri "http://localhost:8080/notes" `
      -Method POST `
      -ContentType "application/json" `
      -Body '{"title":"Первая заметка","content":"Текст...","userId":1,"tags":["go","gorm"]}'
<img width="1094" height="520" alt="image" src="https://github.com/user-attachments/assets/7f44b204-23d7-4d8a-b5fc-376c84c18222" />


Cтруктура проекта:

    ├pz6
    │   go.mod
    │   go.sum
    │
    ├───cmd
    │   └───server
    │           main.go
    │
    └───internal
        ├───db
        │       postgres.go
        │
        ├───httpapi
        │       handlers.go
        │       router.go
        │
        └───models
                models.go

Описание структуры:


    go.mod — файл модуля Go с зависимостями
    go.sum — контрольные суммы зависимостей проекта
    main.go — главная точка входа в приложение
    postgres.go — подключение к PostgreSQL через GORM, настройка пула соединений (SetMaxOpenConns, SetMaxIdleConns, SetConnMaxLifetime)
    router.go — настраивает маршруты (роуты) REST API с помощью chi
    handlers.go — обработчики HTTP-запросов (/health, /users, /notes, /notes/{id}); создание и получение данных, JSON-ответы и обработка ошибок
    models.go — структуры моделей (User, Note, Tag) с GORM-тегами; описывает связи 1:N и M:N
   

