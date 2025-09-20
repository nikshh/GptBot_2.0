# Высокоуровневая схема архитектуры GptBot_v2

## Основная архитектура системы

```mermaid
graph TB
    %% Пользователи и внешние интерфейсы
    subgraph "Пользователи"
        U1[👤 Telegram Пользователи]
        U2[👨‍💼 Администраторы]
    end

    %% Входные точки
    subgraph "Входные точки"
        TG[📱 Telegram Bot API<br/>Основной чат с ИИ]
        MINIAPP[📲 Mini App<br/>Настройки и функции]
    end

    %% Основное приложение
    subgraph "Основное приложение"
        MAIN[🤖 bot main.py<br/>Главный обработчик]
        HANDLERS[📋 handlers<br/>Обработчики команд]
        RUN[▶️ run.py<br/>Точка входа]
    end

    %% Mini App функции
    subgraph "Mini App функции"
        MINIAPP_SETTINGS[⚙️ Настройки]
        MINIAPP_CONTEXT[🧹 Очистка контекста]
        MINIAPP_ROLES[🎭 Управление ролями]
        MINIAPP_SURF[🌐 Web-поиск Surf]
        MINIAPP_TTS[🔊 Text-to-Speech]
        MINIAPP_IMAGE[🎨 Генерация изображений]
        MINIAPP_SERVICES[🛠️ Доп. сервисы]
    end

    %% Дополнительные сервисы Mini App
    subgraph "Дополнительные сервисы"
        SHOPME[🛒 ShopMe]
        PRESENTATIONS[📊 Генерация презентаций]
        GHIBLI[🎌 Studio Ghibli стиль]
        ANTIPLAGIAT[📝 Антиплагиат]
    end

    %% Система обработки сообщений
    subgraph "Обработка сообщений"
        CONTENT[📝 Content Handlers<br/>text, photo, voice, etc.]
        COMMANDS[⚡ Command Handlers<br/>image, surf, talk, role]
        CALLBACKS[🔘 Callback Handlers<br/>Inline кнопки]
        ONBOARDING[🎯 Onboarding System<br/>GIF + Tutorial]
    end

    %% Детальная обработка контента
    subgraph "Обработка типов сообщений"
        TEXT_HANDLER[📝 Текстовые сообщения]
        VOICE_HANDLER[🎤 Голосовые сообщения<br/>Speech-to-Text]
        PHOTO_HANDLER[🖼️ Изображения<br/>GPT-4 Vision]
        DOC_HANDLER[📄 Документы<br/>PDF, DOCX парсинг]
        VIDEO_HANDLER[🎬 Видео<br/>Извлечение кадров]
        STICKER_HANDLER[😀 Стикеры]
    end

    %% Системы преобразования
    subgraph "Преобразование контента"
        STT_ENGINE[🗣️ Speech-to-Text<br/>Whisper API]
        TTS_ENGINE[🔊 Text-to-Speech<br/>Генерация голоса]
        VISION_ENGINE[👁️ Computer Vision<br/>Анализ изображений]
        DOC_PARSER_ENGINE[📋 Document Parser<br/>Извлечение текста]
    end

    %% ИИ и внешние сервисы
    subgraph "ИИ сервисы"
        OPENAI[🧠 OpenAI GPT-4]
        CLAUDE[🧠 Claude 3.5]
        DEEPSEEK[🧠 DeepSeek-R1]
        GROK[🧠 Grok-3]
        STABILITY[🎨 Stable Diffusion]
        DALLE[🎨 DALL-E]
    end

    %% Система управления контекстом
    subgraph "Управление контекстом"
        REDIS[📦 Redis<br/>Контекст диалогов]
        GLOBAL[🌐 Global.py<br/>Глобальное состояние]
        CONTEXT_MANAGER[🧠 Context Manager<br/>Управление историей ИИ]
        SYSTEM_PROMPTS[⚙️ System Prompts<br/>Командные промпты]
        MULTIMODAL_CONTEXT[🎭 Multimodal Context<br/>Мультимодальный контекст]
        CHAT_MODES[🔄 Chat Modes<br/>Режимы чата]
    end

    %% Режимы работы чата
    subgraph "Режимы чата"
        NORMAL_CHAT[💬 Обычный чат<br/>Стандартное общение]
        DOCUMENT_CHAT[📄 Чат с документом<br/>Работа с файлами]
        IMAGE_CHAT[🖼️ Чат с изображением<br/>Анализ картинок]
        VOICE_CHAT[🎤 Голосовой чат<br/>Речевое взаимодействие]
        MODE_SWITCHER[🔀 Переключатель режимов<br/>Автоматическое определение]
    end

    %% Система работы с документами
    subgraph "Работа с документами"
        DOC_SESSION[📋 Document Session<br/>Сессия работы с документом]
        DOC_EDITOR[✏️ Document Editor<br/>Редактирование документа]
        DOC_QA[❓ Document Q&A<br/>Вопросы по документу]
        DOC_ANALYZER[🔍 Document Analyzer<br/>Анализ содержимого]
        DOC_VERSIONING[📚 Document Versioning<br/>Версионирование изменений]
    end

    %% Векторные базы знаний
    subgraph "Векторные базы знаний"
        USER_KNOWLEDGE[👤 Персональная БЗ<br/>Данные пользователя]
        COMPANY_KNOWLEDGE[🏢 Корпоративная БЗ<br/>База знаний компании]
        VECTOR_SEARCH[🔍 Vector Search<br/>Семантический поиск]
        EMBEDDINGS[📊 Embeddings<br/>Векторизация текста]
    end

    %% Система извлечения знаний
    subgraph "Извлечение знаний"
        KNOWLEDGE_EXTRACTOR[🧩 Knowledge Extractor<br/>Автоизвлечение данных]
        USER_PROFILER[📋 User Profiler<br/>Профилирование пользователя]
        FALLBACK_SEARCH[🔄 Fallback Search<br/>Поиск при незнании]
        RAG_SYSTEM[🔗 RAG System<br/>Retrieval-Augmented Generation]
    end

    %% Система оплаты
    subgraph "Система оплаты"
        YOOKASSA[💳 YooKassa API]
        TGSTARS[⭐ Telegram Stars]
        AUTOPAY[🔄 Автоплатежи]
        WEBHOOKS[🔗 Webhooks]
    end

    %% Базы данных
    subgraph "Базы данных"
        USERS_DB[(👥 Users.db<br/>Пользователи)]
        DATA_DB[(📊 Data.db<br/>Аналитика)]
        KEYS_DB[(🔑 Keys.db<br/>Ключи и подарки)]
    end

    %% Система задач
    subgraph "Система задач"
        TASK_PROCESSOR[⚙️ Task Processor<br/>Обработчик задач]
        REDIS_QUEUE[📋 Redis Queue<br/>Очередь задач]
        FIFO[📄 FIFO Fallback<br/>Резервная очередь]
    end

    %% Аналитика и мониторинг
    subgraph "Аналитика"
        ANALYTICS[📈 Анализ данных<br/>analisys]
        LOGS[📝 Логирование<br/>security.log]
        MONITORING[👀 Мониторинг<br/>bureau]
    end

    %% Система генерации документов
    subgraph "Генерация документов"
        DOC_PROCESSOR[📄 Document Processor<br/>Умная генерация]
        EXCEL_GEN[📊 Excel Generator]
        PDF_GEN[📄 PDF Generator]
        DOCX_GEN[📝 DOCX Generator]
        TABLE_PARSER[📋 Table Parser<br/>Legacy pipe символы]
    end

    %% Система тарифов и онбординга
    subgraph "Тарифы и подписки"
        TRIAL[🎁 Trial 3 дня<br/>Бесплатный период]
        TARIFF_99[💰 Classic 99₽]
        TARIFF_199[⚡ Premium 199₽]
        TARIFF_399[👑 Ultima 399₽]
        TARIFF_1890[🏆 Ultima-12 1890₽]
    end

    %% Дополнительные сервисы
    subgraph "Внешние сервисы"
        INVOICE[🧾 Чеки ОФД<br/>invoice_mh]
        YOUTUBE[📺 YouTube QA]
    end

    %% Связи
    U1 --> TG
    U1 --> MINIAPP
    U2 --> TG

    TG --> MAIN
    MINIAPP --> MAIN

    MAIN --> RUN
    MAIN --> HANDLERS
    MAIN --> ONBOARDING
    HANDLERS --> CONTENT
    HANDLERS --> COMMANDS
    HANDLERS --> CALLBACKS

    %% Детальная обработка сообщений
    CONTENT --> TEXT_HANDLER
    CONTENT --> VOICE_HANDLER
    CONTENT --> PHOTO_HANDLER
    CONTENT --> DOC_HANDLER
    CONTENT --> VIDEO_HANDLER
    CONTENT --> STICKER_HANDLER

    %% Связи с системами преобразования
    VOICE_HANDLER --> STT_ENGINE
    PHOTO_HANDLER --> VISION_ENGINE
    DOC_HANDLER --> DOC_PARSER_ENGINE
    VIDEO_HANDLER --> VISION_ENGINE

    %% Связи с ИИ
    TEXT_HANDLER --> OPENAI
    TEXT_HANDLER --> CLAUDE
    STT_ENGINE --> OPENAI
    VISION_ENGINE --> OPENAI
    DOC_PARSER_ENGINE --> OPENAI

    %% TTS для ответов
    OPENAI --> TTS_ENGINE
    CLAUDE --> TTS_ENGINE

    %% Mini App связи
    MINIAPP --> MINIAPP_SETTINGS
    MINIAPP --> MINIAPP_CONTEXT
    MINIAPP --> MINIAPP_ROLES
    MINIAPP --> MINIAPP_SURF
    MINIAPP --> MINIAPP_TTS
    MINIAPP --> MINIAPP_IMAGE
    MINIAPP --> MINIAPP_SERVICES

    MINIAPP_SERVICES --> SHOPME
    MINIAPP_SERVICES --> PRESENTATIONS
    MINIAPP_SERVICES --> GHIBLI
    MINIAPP_SERVICES --> ANTIPLAGIAT

    CONTENT --> OPENAI
    CONTENT --> CLAUDE
    CONTENT --> DEEPSEEK
    CONTENT --> GROK
    COMMANDS --> STABILITY
    COMMANDS --> DALLE

    MAIN --> REDIS
    HANDLERS --> GLOBAL
    GLOBAL --> REDIS
    
    %% Связи с системой контекста
    HANDLERS --> CONTEXT_MANAGER
    CONTEXT_MANAGER --> REDIS
    CONTEXT_MANAGER --> SYSTEM_PROMPTS
    CONTEXT_MANAGER --> MULTIMODAL_CONTEXT
    CONTEXT_MANAGER --> CHAT_MODES
    SYSTEM_PROMPTS --> OPENAI
    SYSTEM_PROMPTS --> CLAUDE

    %% Мультимодальный контекст
    TEXT_HANDLER --> MULTIMODAL_CONTEXT
    VOICE_HANDLER --> MULTIMODAL_CONTEXT
    PHOTO_HANDLER --> MULTIMODAL_CONTEXT
    DOC_HANDLER --> MULTIMODAL_CONTEXT

    %% Режимы чата
    CHAT_MODES --> MODE_SWITCHER
    MODE_SWITCHER --> NORMAL_CHAT
    MODE_SWITCHER --> DOCUMENT_CHAT
    MODE_SWITCHER --> IMAGE_CHAT
    MODE_SWITCHER --> VOICE_CHAT

    %% Работа с документами
    DOC_HANDLER --> DOC_SESSION
    DOC_SESSION --> DOC_EDITOR
    DOC_SESSION --> DOC_QA
    DOC_SESSION --> DOC_ANALYZER
    DOC_SESSION --> DOC_VERSIONING
    
    %% Связи документного режима с ИИ
    DOC_QA --> OPENAI
    DOC_ANALYZER --> OPENAI
    DOC_EDITOR --> OPENAI

    %% Связи с системой оплаты
    CALLBACKS --> YOOKASSA
    CALLBACKS --> TGSTARS
    YOOKASSA --> WEBHOOKS
    AUTOPAY --> YOOKASSA
    
    %% Связи с тарифами
    ONBOARDING --> TRIAL
    CALLBACKS --> TARIFF_99
    CALLBACKS --> TARIFF_199
    CALLBACKS --> TARIFF_399
    CALLBACKS --> TARIFF_1890

    MAIN --> USERS_DB
    HANDLERS --> DATA_DB
    MAIN --> KEYS_DB

    TASK_PROCESSOR --> REDIS_QUEUE
    REDIS_QUEUE --> FIFO

    HANDLERS --> ANALYTICS
    MAIN --> LOGS
    MONITORING --> USERS_DB

    %% Связи с генерацией документов
    HANDLERS --> DOC_PROCESSOR
    DOC_PROCESSOR --> EXCEL_GEN
    DOC_PROCESSOR --> PDF_GEN
    DOC_PROCESSOR --> DOCX_GEN
    HANDLERS --> TABLE_PARSER

    HANDLERS --> INVOICE
    HANDLERS --> YOUTUBE

    %% Связи с векторными базами знаний
    HANDLERS --> KNOWLEDGE_EXTRACTOR
    KNOWLEDGE_EXTRACTOR --> USER_PROFILER
    USER_PROFILER --> USER_KNOWLEDGE
    
    %% Автонаполнение персональной БЗ
    TEXT_HANDLER --> KNOWLEDGE_EXTRACTOR
    VOICE_HANDLER --> KNOWLEDGE_EXTRACTOR
    
    %% Векторизация и поиск
    USER_KNOWLEDGE --> EMBEDDINGS
    COMPANY_KNOWLEDGE --> EMBEDDINGS
    EMBEDDINGS --> VECTOR_SEARCH
    
    %% RAG система
    OPENAI --> FALLBACK_SEARCH
    CLAUDE --> FALLBACK_SEARCH
    FALLBACK_SEARCH --> VECTOR_SEARCH
    VECTOR_SEARCH --> RAG_SYSTEM
    RAG_SYSTEM --> OPENAI
    RAG_SYSTEM --> CLAUDE
    
    %% Связи с базами данных
    USER_KNOWLEDGE --> USERS_DB
    COMPANY_KNOWLEDGE --> DATA_DB

    %% Стили
    classDef userClass fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    classDef botClass fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    classDef aiClass fill:#e8f5e8,stroke:#1b5e20,stroke-width:2px
    classDef dbClass fill:#fff3e0,stroke:#e65100,stroke-width:2px
    classDef payClass fill:#fce4ec,stroke:#880e4f,stroke-width:2px
    classDef miniappClass fill:#e3f2fd,stroke:#0d47a1,stroke-width:2px
    classDef serviceClass fill:#f1f8e9,stroke:#33691e,stroke-width:2px
    classDef tariffClass fill:#fff8e1,stroke:#ff8f00,stroke-width:2px
    classDef docClass fill:#fafafa,stroke:#424242,stroke-width:2px
    classDef handlerClass fill:#e8eaf6,stroke:#3f51b5,stroke-width:2px
    classDef engineClass fill:#f9fbe7,stroke:#689f38,stroke-width:2px
    classDef contextClass fill:#fce4ec,stroke:#ad1457,stroke-width:2px
    classDef knowledgeClass fill:#e0f2f1,stroke:#00695c,stroke-width:2px
    classDef ragClass fill:#fff3e0,stroke:#ef6c00,stroke-width:2px
    classDef modeClass fill:#e8eaf6,stroke:#5c6bc0,stroke-width:2px
    classDef docClass2 fill:#f3e5f5,stroke:#8e24aa,stroke-width:2px
    
    class U1,U2 userClass
    class MAIN,HANDLERS,RUN,ONBOARDING botClass
    class OPENAI,CLAUDE,DEEPSEEK,GROK,STABILITY,DALLE aiClass
    class USERS_DB,DATA_DB,KEYS_DB dbClass
    class YOOKASSA,TGSTARS,AUTOPAY,WEBHOOKS payClass
    class MINIAPP,MINIAPP_SETTINGS,MINIAPP_CONTEXT,MINIAPP_ROLES,MINIAPP_SURF,MINIAPP_TTS,MINIAPP_IMAGE,MINIAPP_SERVICES miniappClass
    class SHOPME,PRESENTATIONS,GHIBLI,ANTIPLAGIAT serviceClass
    class TRIAL,TARIFF_99,TARIFF_199,TARIFF_399,TARIFF_1890 tariffClass
    class DOC_PROCESSOR,EXCEL_GEN,PDF_GEN,DOCX_GEN,TABLE_PARSER docClass
    class TEXT_HANDLER,VOICE_HANDLER,PHOTO_HANDLER,DOC_HANDLER,VIDEO_HANDLER,STICKER_HANDLER handlerClass
    class STT_ENGINE,TTS_ENGINE,VISION_ENGINE,DOC_PARSER_ENGINE engineClass
    class CONTEXT_MANAGER,SYSTEM_PROMPTS,MULTIMODAL_CONTEXT,CHAT_MODES contextClass
    class USER_KNOWLEDGE,COMPANY_KNOWLEDGE,VECTOR_SEARCH,EMBEDDINGS knowledgeClass
    class KNOWLEDGE_EXTRACTOR,USER_PROFILER,FALLBACK_SEARCH,RAG_SYSTEM ragClass
    class NORMAL_CHAT,DOCUMENT_CHAT,IMAGE_CHAT,VOICE_CHAT,MODE_SWITCHER modeClass
    class DOC_SESSION,DOC_EDITOR,DOC_QA,DOC_ANALYZER,DOC_VERSIONING docClass2
```

## Детализация системы обработки сообщений

```mermaid
sequenceDiagram
    participant U as 👤 Пользователь
    participant TG as 📱 Telegram
    participant MA as 📲 Mini App
    participant M as 🤖 Main Bot
    participant H as 📋 Handlers
    participant AI as 🧠 AI Services
    participant DB as 💾 Database
    participant R as 📦 Redis
    participant DOC as 📄 Doc Generator

    alt Первый запуск
        U->>TG: /start
        TG->>M: Команда старт
        M->>H: Onboarding Handler
        H->>TG: GIF + Tutorial
        H->>DB: Создать Trial период 3 дня
        TG->>U: Приветствие + Trial активирован
    else Чат с ИИ
        U->>TG: Отправляет сообщение
        TG->>M: Webhook/Polling
        M->>H: Маршрутизация по типу
        H->>R: Получить контекст
        R-->>H: История диалога
        H->>AI: Запрос к ИИ
        AI-->>H: Ответ ИИ
        alt Содержит таблицу
            H->>DOC: Парсинг таблицы
            DOC-->>H: Сгенерированный документ
        end
        H->>R: Сохранить контекст
        H->>DB: Списать токены
        H->>TG: Ответ пользователю
    else Mini App функции
        U->>MA: Открывает Mini App
        MA->>M: API запрос
        alt Очистка контекста
            M->>R: Очистить историю
        else Установка роли
            M->>R: Сохранить роль
        else TTS генерация
            M->>AI: Text-to-Speech
            AI-->>MA: Аудио файл + история
        else Генерация изображения
            MA->>M: Настройки + промпт
            M->>AI: Генерация изображения
            AI-->>TG: Изображение в чат
        end
        MA->>U: Результат операции
    else Оплата подписки
        U->>TG: Выбор тарифа
        H->>DB: Проверить подписку
        H->>TG: Инвойс 99/199/399/1890₽
        TG-->>H: Успешная оплата
        H->>DB: Начислить подписку
        H->>TG: Подтверждение активации
    end
    
    TG->>U: Получает ответ
```

## Схема системы оплаты и тарифов

```mermaid
graph TB
    subgraph "Способы оплаты"
        STARS[⭐ Telegram Stars]
        YOOKASSA[💳 YooKassa]
        AUTO[🔄 Автоплатежи]
    end

    subgraph "Система тарифов"
        TRIAL_PERIOD[🎁 Trial период<br/>3 дня бесплатно]
        BASIC_99[💰 Базовый<br/>99₽/месяц]
        STANDARD_199[⚡ Стандарт<br/>199₽/месяц]
        PREMIUM_399[👑 Премиум<br/>399₽/месяц]
        YEARLY_1890[🏆 Годовой<br/>1890₽/год]
    end

    subgraph "Onboarding система"
        START_CMD[▶️ start команда]
        WELCOME_GIF[🎬 Приветственный GIF]
        TUTORIAL[📚 Короткий туториал]
        TRIAL_ACTIVATION[🎯 Активация Trial]
    end

    subgraph "Обработка платежей"
        WEBHOOK[🔗 Webhook Handler]
        PAYMENT_PROC[💰 Payment Processor]
        SUB_PROVIDER[📋 Subscription Provider]
    end

    %% Onboarding flow
    START_CMD --> WELCOME_GIF
    WELCOME_GIF --> TUTORIAL
    TUTORIAL --> TRIAL_ACTIVATION
    TRIAL_ACTIVATION --> TRIAL_PERIOD

    %% Payment flow
    STARS --> WEBHOOK
    YOOKASSA --> WEBHOOK
    AUTO --> PAYMENT_PROC
    
    WEBHOOK --> PAYMENT_PROC
    PAYMENT_PROC --> SUB_PROVIDER
    
    %% Subscription assignment
    SUB_PROVIDER --> BASIC_99
    SUB_PROVIDER --> STANDARD_199
    SUB_PROVIDER --> PREMIUM_399
    SUB_PROVIDER --> YEARLY_1890
    
    SUB_PROVIDER --> USERS_DB
    TRIAL_PERIOD --> USERS_DB

    %% Styling
    classDef trialClass fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef tariffClass fill:#fff8e1,stroke:#ff8f00,stroke-width:2px
    classDef onboardClass fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef paymentClass fill:#fce4ec,stroke:#c2185b,stroke-width:2px
    
    class TRIAL_PERIOD trialClass
    class BASIC_99,STANDARD_199,PREMIUM_399,YEARLY_1890 tariffClass
    class START_CMD,WELCOME_GIF,TUTORIAL,TRIAL_ACTIVATION onboardClass
    class STARS,YOOKASSA,AUTO,WEBHOOK,PAYMENT_PROC,SUB_PROVIDER paymentClass
```

## Архитектура Mini App

```mermaid
graph TB
    subgraph "Mini App интерфейс"
        MINI_UI[📲 Mini App UI]
        SETTINGS_UI[⚙️ Настройки]
        FUNCTIONS_UI[🛠️ Функции]
    end

    subgraph "Основные функции"
        CONTEXT_CLEAR[🧹 Очистка контекста<br/>Сброс истории диалога]
        ROLE_MANAGER[🎭 Менеджер ролей<br/>Установка системных промптов]
        SURF_TOGGLE[🌐 Web-поиск<br/>Включение/выключение Surf]
        TTS_GENERATOR[🔊 Text-to-Speech<br/>Генерация + История]
        IMAGE_SETTINGS[🎨 Настройки изображений<br/>Выбор модели генерации]
    end

    subgraph "Дополнительные сервисы"
        SHOPME_SERVICE[🛒 ShopMe<br/>Помощник покупок]
        PRESENTATION_GEN[📊 Генератор презентаций<br/>Создание слайдов]
        GHIBLI_STYLE[🎌 Studio Ghibli<br/>Стилизация изображений]
        ANTIPLAGIAT_SERVICE[📝 Антиплагиат<br/>Повышение оригинальности]
    end

    subgraph "API взаимодействие"
        MINI_API[🔌 Mini App API]
        BOT_INTEGRATION[🤖 Интеграция с ботом]
        FILE_HANDLER[📁 Обработчик файлов]
        HISTORY_MANAGER[📚 Менеджер истории]
    end

    %% UI connections
    MINI_UI --> SETTINGS_UI
    MINI_UI --> FUNCTIONS_UI

    %% Function connections
    SETTINGS_UI --> CONTEXT_CLEAR
    SETTINGS_UI --> ROLE_MANAGER
    SETTINGS_UI --> SURF_TOGGLE
    
    FUNCTIONS_UI --> TTS_GENERATOR
    FUNCTIONS_UI --> IMAGE_SETTINGS
    FUNCTIONS_UI --> SHOPME_SERVICE
    FUNCTIONS_UI --> PRESENTATION_GEN
    FUNCTIONS_UI --> GHIBLI_STYLE
    FUNCTIONS_UI --> ANTIPLAGIAT_SERVICE

    %% API connections
    CONTEXT_CLEAR --> MINI_API
    ROLE_MANAGER --> MINI_API
    SURF_TOGGLE --> MINI_API
    TTS_GENERATOR --> MINI_API
    IMAGE_SETTINGS --> MINI_API

    MINI_API --> BOT_INTEGRATION
    TTS_GENERATOR --> FILE_HANDLER
    TTS_GENERATOR --> HISTORY_MANAGER

    %% External services
    SHOPME_SERVICE --> BOT_INTEGRATION
    PRESENTATION_GEN --> BOT_INTEGRATION
    GHIBLI_STYLE --> BOT_INTEGRATION
    ANTIPLAGIAT_SERVICE --> BOT_INTEGRATION

    %% Styling
    classDef uiClass fill:#e3f2fd,stroke:#0d47a1,stroke-width:2px
    classDef functionClass fill:#f1f8e9,stroke:#33691e,stroke-width:2px
    classDef serviceClass fill:#fff3e0,stroke:#e65100,stroke-width:2px
    classDef apiClass fill:#fce4ec,stroke:#880e4f,stroke-width:2px
    
    class MINI_UI,SETTINGS_UI,FUNCTIONS_UI uiClass
    class CONTEXT_CLEAR,ROLE_MANAGER,SURF_TOGGLE,TTS_GENERATOR,IMAGE_SETTINGS functionClass
    class SHOPME_SERVICE,PRESENTATION_GEN,GHIBLI_STYLE,ANTIPLAGIAT_SERVICE serviceClass
    class MINI_API,BOT_INTEGRATION,FILE_HANDLER,HISTORY_MANAGER apiClass
```

## Схема генерации документов

```mermaid
graph TB
    subgraph "Входные данные"
        AI_RESPONSE[🧠 Ответ ИИ]
        USER_REQUEST[👤 Запрос пользователя]
        LEGACY_PARSER[📋 Legacy парсер<br/>Символы pipe в тексте]
    end

    subgraph "Система обработки"
        CONTENT_ANALYZER[🔍 Анализатор контента<br/>Определение типа документа]
        FUNCTION_ROUTER[🔀 Маршрутизатор функций<br/>Выбор генератора]
        SMART_PROCESSOR[🧠 Умный процессор<br/>ИИ-анализ структуры]
    end

    subgraph "Генераторы документов"
        EXCEL_GENERATOR[📊 Excel Generator<br/>Таблицы и графики]
        PDF_GENERATOR[📄 PDF Generator<br/>Отчёты и документы]
        DOCX_GENERATOR[📝 DOCX Generator<br/>Текстовые документы]
        POWERPOINT_GEN[📊 PowerPoint Generator<br/>Презентации]
    end

    subgraph "Выходные данные"
        DOCUMENT_FILE[📁 Готовый документ]
        DOWNLOAD_LINK[🔗 Ссылка на скачивание]
        TELEGRAM_FILE[📤 Отправка в Telegram]
    end

    %% Current flow (legacy)
    AI_RESPONSE --> LEGACY_PARSER
    LEGACY_PARSER --> DOCX_GENERATOR
    
    %% Future flow (smart)
    USER_REQUEST --> CONTENT_ANALYZER
    AI_RESPONSE --> CONTENT_ANALYZER
    CONTENT_ANALYZER --> SMART_PROCESSOR
    SMART_PROCESSOR --> FUNCTION_ROUTER
    
    FUNCTION_ROUTER --> EXCEL_GENERATOR
    FUNCTION_ROUTER --> PDF_GENERATOR
    FUNCTION_ROUTER --> DOCX_GENERATOR
    FUNCTION_ROUTER --> POWERPOINT_GEN
    
    %% Output handling
    EXCEL_GENERATOR --> DOCUMENT_FILE
    PDF_GENERATOR --> DOCUMENT_FILE
    DOCX_GENERATOR --> DOCUMENT_FILE
    POWERPOINT_GEN --> DOCUMENT_FILE
    
    DOCUMENT_FILE --> DOWNLOAD_LINK
    DOCUMENT_FILE --> TELEGRAM_FILE

    %% Styling
    classDef inputClass fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef processClass fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef generatorClass fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    classDef outputClass fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef legacyClass fill:#ffebee,stroke:#d32f2f,stroke-width:2px,stroke-dasharray: 5 5
    
    class AI_RESPONSE,USER_REQUEST inputClass
    class CONTENT_ANALYZER,FUNCTION_ROUTER,SMART_PROCESSOR processClass
    class EXCEL_GENERATOR,PDF_GENERATOR,DOCX_GENERATOR,POWERPOINT_GEN generatorClass
    class DOCUMENT_FILE,DOWNLOAD_LINK,TELEGRAM_FILE outputClass
    class LEGACY_PARSER legacyClass
```

## Схема обработки типов сообщений

```mermaid
graph TB
    subgraph "Входящие сообщения"
        TEXT_MSG[📝 Текстовое сообщение]
        VOICE_MSG[🎤 Голосовое сообщение]
        PHOTO_MSG[🖼️ Изображение/Фото]
        DOC_MSG[📄 Документ]
        VIDEO_MSG[🎬 Видео]
        STICKER_MSG[😀 Стикер]
    end

    subgraph "Предобработка"
        MSG_ROUTER[🔀 Маршрутизатор сообщений<br/>Определение типа]
        VOICE_TO_TEXT[🗣️ Speech-to-Text<br/>Whisper API]
        IMAGE_ANALYZER[👁️ Анализ изображений<br/>GPT-4 Vision]
        DOC_PARSER[📋 Парсер документов<br/>PDF, DOCX, TXT]
        VIDEO_PROCESSOR[🎞️ Обработка видео<br/>Извлечение кадров]
    end

    subgraph "ИИ обработка"
        TEXT_AI[🧠 Текстовый ИИ<br/>GPT-4, Claude, DeepSeek]
        VISION_AI[👀 Vision ИИ<br/>Анализ изображений]
        MULTIMODAL_AI[🔄 Мультимодальный ИИ<br/>Текст + изображение]
    end

    subgraph "Генерация ответов"
        TEXT_RESPONSE[📝 Текстовый ответ]
        VOICE_RESPONSE[🔊 Голосовой ответ<br/>Text-to-Speech]
        IMAGE_GENERATION[🎨 Генерация изображения<br/>DALL-E, Stable Diffusion]
        DOC_GENERATION[📄 Генерация документа<br/>PDF, DOCX, Excel]
    end

    subgraph "Отправка пользователю"
        SEND_TEXT[📤 Отправить текст]
        SEND_VOICE[📤 Отправить аудио]
        SEND_IMAGE[📤 Отправить изображение]
        SEND_DOCUMENT[📤 Отправить документ]
    end

    %% Routing
    TEXT_MSG --> MSG_ROUTER
    VOICE_MSG --> MSG_ROUTER
    PHOTO_MSG --> MSG_ROUTER
    DOC_MSG --> MSG_ROUTER
    VIDEO_MSG --> MSG_ROUTER
    STICKER_MSG --> MSG_ROUTER

    %% Processing paths
    MSG_ROUTER --> VOICE_TO_TEXT
    MSG_ROUTER --> IMAGE_ANALYZER
    MSG_ROUTER --> DOC_PARSER
    MSG_ROUTER --> VIDEO_PROCESSOR

    %% Text processing
    TEXT_MSG --> TEXT_AI
    VOICE_TO_TEXT --> TEXT_AI

    %% Image processing
    IMAGE_ANALYZER --> VISION_AI
    PHOTO_MSG --> VISION_AI

    %% Document processing
    DOC_PARSER --> TEXT_AI

    %% Video processing
    VIDEO_PROCESSOR --> VISION_AI

    %% Multimodal processing
    TEXT_AI --> MULTIMODAL_AI
    VISION_AI --> MULTIMODAL_AI

    %% Response generation
    TEXT_AI --> TEXT_RESPONSE
    TEXT_AI --> VOICE_RESPONSE
    TEXT_AI --> IMAGE_GENERATION
    TEXT_AI --> DOC_GENERATION

    VISION_AI --> TEXT_RESPONSE
    MULTIMODAL_AI --> TEXT_RESPONSE

    %% Sending responses
    TEXT_RESPONSE --> SEND_TEXT
    VOICE_RESPONSE --> SEND_VOICE
    IMAGE_GENERATION --> SEND_IMAGE
    DOC_GENERATION --> SEND_DOCUMENT

    %% Styling
    classDef inputClass fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef processClass fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef aiClass fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    classDef responseClass fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef outputClass fill:#ffebee,stroke:#c62828,stroke-width:2px
    
    class TEXT_MSG,VOICE_MSG,PHOTO_MSG,DOC_MSG,VIDEO_MSG,STICKER_MSG inputClass
    class MSG_ROUTER,VOICE_TO_TEXT,IMAGE_ANALYZER,DOC_PARSER,VIDEO_PROCESSOR processClass
    class TEXT_AI,VISION_AI,MULTIMODAL_AI aiClass
    class TEXT_RESPONSE,VOICE_RESPONSE,IMAGE_GENERATION,DOC_GENERATION responseClass
    class SEND_TEXT,SEND_VOICE,SEND_IMAGE,SEND_DOCUMENT outputClass
```

## Детальная схема обработки сообщений по типам

```mermaid
sequenceDiagram
    participant U as 👤 Пользователь
    participant TG as 📱 Telegram
    participant R as 🔀 Router
    participant P as 🔄 Preprocessor
    participant AI as 🧠 AI Engine
    participant G as 🎨 Generator
    participant DB as 💾 Database

    alt Текстовое сообщение
        U->>TG: Печатает текст
        TG->>R: Текстовое сообщение
        R->>AI: Прямо в ИИ
        AI->>G: Генерация ответа
        G->>TG: Текстовый ответ
        G->>DB: Сохранить в контекст
        TG->>U: Получает ответ
    
    else Голосовое сообщение
        U->>TG: Записывает голос
        TG->>R: Аудио файл
        R->>P: Speech-to-Text
        P->>AI: Текст из голоса
        AI->>G: Генерация ответа
        alt Текстовый ответ
            G->>TG: Текст
        else Голосовой ответ
            G->>P: Text-to-Speech
            P->>TG: Аудио файл
        end
        G->>DB: Сохранить в контекст
        TG->>U: Получает ответ
    
    else Изображение
        U->>TG: Отправляет фото
        TG->>R: Изображение
        R->>P: Анализ изображения
        P->>AI: Описание изображения
        AI->>G: Генерация ответа
        alt Текстовое описание
            G->>TG: Описание изображения
        else Генерация нового изображения
            G->>P: Создать изображение
            P->>TG: Новое изображение
        end
        G->>DB: Сохранить в контекст
        TG->>U: Получает ответ
    
    else Документ
        U->>TG: Загружает файл
        TG->>R: PDF/DOCX/TXT
        R->>P: Парсинг документа
        P->>AI: Извлеченный текст
        AI->>G: Анализ документа
        alt Текстовый анализ
            G->>TG: Анализ содержимого
        else Создание нового документа
            G->>P: Генерация документа
            P->>TG: Новый файл
        end
        G->>DB: Сохранить в контекст
        TG->>U: Получает результат
    end
```

## Система режимов чата и мультимодального контекста

```mermaid
graph TB
    subgraph "Входящий контент"
        TEXT_INPUT[📝 Текстовый ввод]
        VOICE_INPUT[🎤 Голосовой ввод]
        IMAGE_INPUT[🖼️ Изображение]
        DOC_INPUT[📄 Документ]
    end

    subgraph "Определение режима"
        CONTENT_DETECTOR[🔍 Content Detector<br/>Определение типа контента]
        MODE_SELECTOR[🎯 Mode Selector<br/>Выбор режима чата]
        CONTEXT_ANALYZER[🧠 Context Analyzer<br/>Анализ текущего контекста]
    end

    subgraph "Режимы чата"
        NORMAL_MODE[💬 Обычный режим<br/>Стандартное общение]
        DOC_MODE[📄 Документный режим<br/>Работа с файлом]
        IMAGE_MODE[🖼️ Режим изображений<br/>Анализ картинок]
        VOICE_MODE[🎤 Голосовой режим<br/>Речевое общение]
    end

    subgraph "Мультимодальный контекст"
        CONTEXT_MEMORY[🧠 Context Memory<br/>Память контекста]
        MULTIMODAL_HISTORY[📚 Multimodal History<br/>История всех типов контента]
        CONTEXT_FUSION[🔗 Context Fusion<br/>Объединение контекстов]
        RELEVANCE_TRACKER[📊 Relevance Tracker<br/>Отслеживание релевантности]
    end

    %% Определение режима
    TEXT_INPUT --> CONTENT_DETECTOR
    VOICE_INPUT --> CONTENT_DETECTOR
    IMAGE_INPUT --> CONTENT_DETECTOR
    DOC_INPUT --> CONTENT_DETECTOR

    CONTENT_DETECTOR --> MODE_SELECTOR
    CONTEXT_ANALYZER --> MODE_SELECTOR

    %% Переключение режимов
    MODE_SELECTOR --> NORMAL_MODE
    MODE_SELECTOR --> DOC_MODE
    MODE_SELECTOR --> IMAGE_MODE
    MODE_SELECTOR --> VOICE_MODE

    %% Формирование контекста
    TEXT_INPUT --> MULTIMODAL_HISTORY
    VOICE_INPUT --> MULTIMODAL_HISTORY
    IMAGE_INPUT --> MULTIMODAL_HISTORY
    DOC_INPUT --> MULTIMODAL_HISTORY

    MULTIMODAL_HISTORY --> CONTEXT_MEMORY
    CONTEXT_MEMORY --> CONTEXT_FUSION
    CONTEXT_FUSION --> RELEVANCE_TRACKER

    %% Обратная связь с анализатором
    RELEVANCE_TRACKER --> CONTEXT_ANALYZER

    %% Стили
    classDef inputClass fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef detectorClass fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef modeClass fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    classDef contextClass fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    
    class TEXT_INPUT,VOICE_INPUT,IMAGE_INPUT,DOC_INPUT inputClass
    class CONTENT_DETECTOR,MODE_SELECTOR,CONTEXT_ANALYZER detectorClass
    class NORMAL_MODE,DOC_MODE,IMAGE_MODE,VOICE_MODE modeClass
    class CONTEXT_MEMORY,MULTIMODAL_HISTORY,CONTEXT_FUSION,RELEVANCE_TRACKER contextClass
```

## Детальная схема работы с документами

```mermaid
graph TB
    subgraph "Загрузка документа"
        DOC_UPLOAD[📤 Загрузка документа<br/>PDF, DOCX, TXT, etc.]
        DOC_VALIDATION[✅ Валидация<br/>Проверка формата и размера]
        DOC_PARSING[📋 Парсинг<br/>Извлечение текста и структуры]
        DOC_INDEXING[🔍 Индексация<br/>Создание поисковых индексов]
    end

    subgraph "Режим чата с документом"
        DOC_SESSION_MGR[📋 Session Manager<br/>Управление сессией]
        DOC_CONTEXT[📄 Document Context<br/>Контекст документа]
        DOC_MEMORY[🧠 Document Memory<br/>Память о документе]
        SESSION_STATE[⚙️ Session State<br/>Состояние сессии]
    end

    subgraph "Операции с документом"
        DOC_QA_ENGINE[❓ Q&A Engine<br/>Вопросы по документу]
        DOC_EDIT_ENGINE[✏️ Edit Engine<br/>Редактирование документа]
        DOC_SUMMARY[📊 Summary Engine<br/>Создание резюме]
        DOC_SEARCH[🔍 Document Search<br/>Поиск по документу]
    end

    subgraph "Версионирование"
        VERSION_CONTROL[📚 Version Control<br/>Контроль версий]
        CHANGE_TRACKER[📝 Change Tracker<br/>Отслеживание изменений]
        DIFF_ENGINE[🔄 Diff Engine<br/>Сравнение версий]
        ROLLBACK[↩️ Rollback<br/>Откат изменений]
    end

    subgraph "Экспорт результатов"
        DOC_GENERATOR[📄 Document Generator<br/>Генерация документов]
        FORMAT_CONVERTER[🔄 Format Converter<br/>Конвертация форматов]
        DOWNLOAD_MANAGER[📥 Download Manager<br/>Управление загрузками]
    end

    %% Процесс загрузки
    DOC_UPLOAD --> DOC_VALIDATION
    DOC_VALIDATION --> DOC_PARSING
    DOC_PARSING --> DOC_INDEXING
    DOC_INDEXING --> DOC_SESSION_MGR

    %% Управление сессией
    DOC_SESSION_MGR --> DOC_CONTEXT
    DOC_SESSION_MGR --> DOC_MEMORY
    DOC_SESSION_MGR --> SESSION_STATE

    %% Операции
    DOC_CONTEXT --> DOC_QA_ENGINE
    DOC_CONTEXT --> DOC_EDIT_ENGINE
    DOC_CONTEXT --> DOC_SUMMARY
    DOC_CONTEXT --> DOC_SEARCH

    %% Версионирование
    DOC_EDIT_ENGINE --> VERSION_CONTROL
    VERSION_CONTROL --> CHANGE_TRACKER
    CHANGE_TRACKER --> DIFF_ENGINE
    VERSION_CONTROL --> ROLLBACK

    %% Экспорт
    DOC_EDIT_ENGINE --> DOC_GENERATOR
    DOC_GENERATOR --> FORMAT_CONVERTER
    FORMAT_CONVERTER --> DOWNLOAD_MANAGER

    %% Стили
    classDef uploadClass fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef sessionClass fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef operationClass fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    classDef versionClass fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef exportClass fill:#ffebee,stroke:#c62828,stroke-width:2px
    
    class DOC_UPLOAD,DOC_VALIDATION,DOC_PARSING,DOC_INDEXING uploadClass
    class DOC_SESSION_MGR,DOC_CONTEXT,DOC_MEMORY,SESSION_STATE sessionClass
    class DOC_QA_ENGINE,DOC_EDIT_ENGINE,DOC_SUMMARY,DOC_SEARCH operationClass
    class VERSION_CONTROL,CHANGE_TRACKER,DIFF_ENGINE,ROLLBACK versionClass
    class DOC_GENERATOR,FORMAT_CONVERTER,DOWNLOAD_MANAGER exportClass
```

## Схема работы режимов чата

```mermaid
sequenceDiagram
    participant U as 👤 Пользователь
    participant MD as 🔍 Mode Detector
    participant CM as 🧠 Context Manager
    participant DM as 📄 Document Mode
    participant IM as 🖼️ Image Mode
    participant VM as 🎤 Voice Mode
    participant AI as 🧠 AI Engine

    alt Отправка документа
        U->>MD: Загружает документ
        MD->>CM: Переключить в Document Mode
        CM->>DM: Активировать режим документа
        DM->>DM: Парсинг и индексация
        DM->>U: "Документ загружен. Режим работы с документом активирован"
        
        loop Работа с документом
            U->>DM: Вопрос по документу
            DM->>AI: Запрос с контекстом документа
            AI-->>DM: Ответ на основе документа
            DM->>U: Ответ с ссылками на разделы
            
            alt Редактирование
                U->>DM: "Измени раздел X"
                DM->>AI: Запрос на редактирование
                AI-->>DM: Предложенные изменения
                DM->>DM: Создать новую версию
                DM->>U: Показать изменения + версия
            end
        end
        
        U->>DM: "Экспортировать документ"
        DM->>U: Готовый файл для скачивания
    
    else Отправка изображения
        U->>MD: Загружает изображение
        MD->>CM: Переключить в Image Mode
        CM->>IM: Активировать режим изображений
        IM->>AI: Анализ изображения
        AI-->>IM: Описание изображения
        IM->>U: Описание + возможности
        
        U->>IM: Вопрос об изображении
        IM->>AI: Запрос с изображением в контексте
        AI-->>IM: Ответ об изображении
        IM->>U: Детальный ответ
    
    else Голосовое сообщение
        U->>MD: Отправляет голос
        MD->>CM: Переключить в Voice Mode
        CM->>VM: Активировать голосовой режим
        VM->>AI: Speech-to-Text + анализ
        AI-->>VM: Текстовый ответ
        VM->>VM: Text-to-Speech
        VM->>U: Голосовой ответ
    
    else Обычный текст
        U->>MD: Печатает текст
        MD->>CM: Обычный режим
        CM->>AI: Стандартный запрос
        AI-->>CM: Обычный ответ
        CM->>U: Текстовый ответ
    end
```

## Система управления контекстом и базами знаний

```mermaid
graph TB
    subgraph "Контекст нейросети"
        DIALOG_HISTORY[💬 История диалога<br/>Вопросы + Ответы ИИ]
        USER_PROMPT[👤 Промпт пользователя<br/>Текущий запрос]
        SYSTEM_PROMPT[⚙️ System промпт<br/>Командное управление]
        CONTEXT_WINDOW[🪟 Context Window<br/>Окно контекста ИИ]
    end

    subgraph "Персональная база знаний"
        USER_NAME[👤 Имя пользователя]
        USER_PREFERENCES[⚙️ Предпочтения]
        USER_HISTORY[📚 История взаимодействий]
        USER_SKILLS[🎯 Навыки и интересы]
        USER_PROJECTS[📋 Проекты пользователя]
        AUTO_EXTRACTOR[🔍 Автоизвлечение<br/>Из диалогов]
    end

    subgraph "Корпоративная база знаний"
        COMPANY_DOCS[📄 Документация]
        FAQ_BASE[❓ База FAQ]
        PRODUCT_INFO[📦 Информация о продуктах]
        POLICIES[📋 Политики и процедуры]
        KNOWLEDGE_ADMIN[👨‍💼 Администрирование БЗ]
    end

    subgraph "Векторный поиск"
        EMBEDDING_MODEL[🧠 Embedding модель<br/>text-embedding-3-large]
        VECTOR_DB[🗄️ Векторная БД<br/>Pinecone/Chroma/Weaviate]
        SIMILARITY_SEARCH[🔍 Similarity Search<br/>Cosine similarity]
        RELEVANCE_FILTER[🎯 Фильтр релевантности<br/>Threshold scoring]
    end

    subgraph "RAG Pipeline"
        QUERY_ANALYZER[🔍 Анализатор запроса<br/>Определение намерений]
        KNOWLEDGE_RETRIEVER[📚 Knowledge Retriever<br/>Поиск релевантной информации]
        CONTEXT_ENRICHER[➕ Context Enricher<br/>Обогащение контекста]
        RESPONSE_GENERATOR[🤖 Response Generator<br/>Генерация с учетом БЗ]
    end

    %% Формирование контекста
    USER_PROMPT --> CONTEXT_WINDOW
    SYSTEM_PROMPT --> CONTEXT_WINDOW
    DIALOG_HISTORY --> CONTEXT_WINDOW

    %% Автонаполнение персональной БЗ
    DIALOG_HISTORY --> AUTO_EXTRACTOR
    AUTO_EXTRACTOR --> USER_NAME
    AUTO_EXTRACTOR --> USER_PREFERENCES
    AUTO_EXTRACTOR --> USER_HISTORY
    AUTO_EXTRACTOR --> USER_SKILLS
    AUTO_EXTRACTOR --> USER_PROJECTS

    %% Векторизация данных
    USER_NAME --> EMBEDDING_MODEL
    USER_PREFERENCES --> EMBEDDING_MODEL
    USER_HISTORY --> EMBEDDING_MODEL
    USER_SKILLS --> EMBEDDING_MODEL
    USER_PROJECTS --> EMBEDDING_MODEL

    COMPANY_DOCS --> EMBEDDING_MODEL
    FAQ_BASE --> EMBEDDING_MODEL
    PRODUCT_INFO --> EMBEDDING_MODEL
    POLICIES --> EMBEDDING_MODEL

    EMBEDDING_MODEL --> VECTOR_DB

    %% RAG процесс
    USER_PROMPT --> QUERY_ANALYZER
    QUERY_ANALYZER --> KNOWLEDGE_RETRIEVER
    KNOWLEDGE_RETRIEVER --> VECTOR_DB
    VECTOR_DB --> SIMILARITY_SEARCH
    SIMILARITY_SEARCH --> RELEVANCE_FILTER
    RELEVANCE_FILTER --> CONTEXT_ENRICHER
    CONTEXT_ENRICHER --> CONTEXT_WINDOW
    CONTEXT_WINDOW --> RESPONSE_GENERATOR

    %% Стили
    classDef contextClass fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef personalClass fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef companyClass fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    classDef vectorClass fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef ragClass fill:#ffebee,stroke:#c62828,stroke-width:2px
    
    class DIALOG_HISTORY,USER_PROMPT,SYSTEM_PROMPT,CONTEXT_WINDOW contextClass
    class USER_NAME,USER_PREFERENCES,USER_HISTORY,USER_SKILLS,USER_PROJECTS,AUTO_EXTRACTOR personalClass
    class COMPANY_DOCS,FAQ_BASE,PRODUCT_INFO,POLICIES,KNOWLEDGE_ADMIN companyClass
    class EMBEDDING_MODEL,VECTOR_DB,SIMILARITY_SEARCH,RELEVANCE_FILTER vectorClass
    class QUERY_ANALYZER,KNOWLEDGE_RETRIEVER,CONTEXT_ENRICHER,RESPONSE_GENERATOR ragClass
```

## Схема работы с контекстом и знаниями

```mermaid
sequenceDiagram
    participant U as 👤 Пользователь
    participant CM as 🧠 Context Manager
    participant KE as 🔍 Knowledge Extractor
    participant VDB as 🗄️ Vector DB
    participant RAG as 🤖 RAG System
    participant AI as 🧠 AI Model

    alt Новый пользователь
        U->>CM: Первое сообщение
        CM->>KE: Извлечь данные пользователя
        KE->>VDB: Создать профиль
        Note over VDB: Автоматически сохраняется:<br/>имя, предпочтения, интересы
        VDB-->>CM: Профиль создан
    
    else Обычный запрос
        U->>CM: Отправляет сообщение
        CM->>KE: Обновить профиль
        KE->>VDB: Добавить новые данные
        
        CM->>RAG: Анализ запроса
        RAG->>VDB: Поиск в персональной БЗ
        RAG->>VDB: Поиск в корпоративной БЗ
        VDB-->>RAG: Релевантная информация
        
        RAG->>CM: Обогащенный контекст
        CM->>AI: Запрос с контекстом + БЗ
        AI-->>CM: Персонализированный ответ
        CM-->>U: Ответ с учетом истории
    
    else ИИ не знает ответ
        U->>CM: Сложный вопрос
        CM->>AI: Обычный запрос
        AI-->>CM: "Не знаю"
        
        CM->>RAG: Fallback поиск
        RAG->>VDB: Глубокий поиск в БЗ
        VDB-->>RAG: Найденная информация
        
        alt Информация найдена
            RAG->>AI: Повторный запрос + найденные данные
            AI-->>CM: Ответ на основе БЗ
            CM-->>U: Информативный ответ
        else Информация не найдена
            CM-->>U: Извинение + предложение помощи
        end
    end
```

## Система режимов чата и мультимодального контекста

```mermaid
graph TB
    subgraph "Входящий контент"
        TEXT_INPUT[📝 Текстовый ввод]
        VOICE_INPUT[🎤 Голосовой ввод]
        IMAGE_INPUT[🖼️ Изображение]
        DOC_INPUT[📄 Документ]
    end

    subgraph "Определение режима"
        CONTENT_DETECTOR[🔍 Content Detector<br/>Определение типа контента]
        MODE_SELECTOR[🎯 Mode Selector<br/>Выбор режима чата]
        CONTEXT_ANALYZER[🧠 Context Analyzer<br/>Анализ текущего контекста]
    end

    subgraph "Режимы чата"
        NORMAL_MODE[💬 Обычный режим<br/>Стандартное общение]
        DOC_MODE[📄 Документный режим<br/>Работа с файлом]
        IMAGE_MODE[🖼️ Режим изображений<br/>Анализ картинок]
        VOICE_MODE[🎤 Голосовой режим<br/>Речевое общение]
    end

    subgraph "Мультимодальный контекст"
        CONTEXT_MEMORY[🧠 Context Memory<br/>Память контекста]
        MULTIMODAL_HISTORY[📚 Multimodal History<br/>История всех типов контента]
        CONTEXT_FUSION[🔗 Context Fusion<br/>Объединение контекстов]
        RELEVANCE_TRACKER[📊 Relevance Tracker<br/>Отслеживание релевантности]
    end

    %% Определение режима
    TEXT_INPUT --> CONTENT_DETECTOR
    VOICE_INPUT --> CONTENT_DETECTOR
    IMAGE_INPUT --> CONTENT_DETECTOR
    DOC_INPUT --> CONTENT_DETECTOR

    CONTENT_DETECTOR --> MODE_SELECTOR
    CONTEXT_ANALYZER --> MODE_SELECTOR

    %% Переключение режимов
    MODE_SELECTOR --> NORMAL_MODE
    MODE_SELECTOR --> DOC_MODE
    MODE_SELECTOR --> IMAGE_MODE
    MODE_SELECTOR --> VOICE_MODE

    %% Формирование контекста
    TEXT_INPUT --> MULTIMODAL_HISTORY
    VOICE_INPUT --> MULTIMODAL_HISTORY
    IMAGE_INPUT --> MULTIMODAL_HISTORY
    DOC_INPUT --> MULTIMODAL_HISTORY

    MULTIMODAL_HISTORY --> CONTEXT_MEMORY
    CONTEXT_MEMORY --> CONTEXT_FUSION
    CONTEXT_FUSION --> RELEVANCE_TRACKER

    %% Обратная связь с анализатором
    RELEVANCE_TRACKER --> CONTEXT_ANALYZER

    %% Стили
    classDef inputClass fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef detectorClass fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef modeClass fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    classDef contextClass fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    
    class TEXT_INPUT,VOICE_INPUT,IMAGE_INPUT,DOC_INPUT inputClass
    class CONTENT_DETECTOR,MODE_SELECTOR,CONTEXT_ANALYZER detectorClass
    class NORMAL_MODE,DOC_MODE,IMAGE_MODE,VOICE_MODE modeClass
    class CONTEXT_MEMORY,MULTIMODAL_HISTORY,CONTEXT_FUSION,RELEVANCE_TRACKER contextClass
```

## Детальная схема работы с документами

```mermaid
graph TB
    subgraph "Загрузка документа"
        DOC_UPLOAD[📤 Загрузка документа<br/>PDF, DOCX, TXT, etc.]
        DOC_VALIDATION[✅ Валидация<br/>Проверка формата и размера]
        DOC_PARSING[📋 Парсинг<br/>Извлечение текста и структуры]
        DOC_INDEXING[🔍 Индексация<br/>Создание поисковых индексов]
    end

    subgraph "Режим чата с документом"
        DOC_SESSION_MGR[📋 Session Manager<br/>Управление сессией]
        DOC_CONTEXT[📄 Document Context<br/>Контекст документа]
        DOC_MEMORY[🧠 Document Memory<br/>Память о документе]
        SESSION_STATE[⚙️ Session State<br/>Состояние сессии]
    end

    subgraph "Операции с документом"
        DOC_QA_ENGINE[❓ Q&A Engine<br/>Вопросы по документу]
        DOC_EDIT_ENGINE[✏️ Edit Engine<br/>Редактирование документа]
        DOC_SUMMARY[📊 Summary Engine<br/>Создание резюме]
        DOC_SEARCH[🔍 Document Search<br/>Поиск по документу]
    end

    subgraph "Версионирование"
        VERSION_CONTROL[📚 Version Control<br/>Контроль версий]
        CHANGE_TRACKER[📝 Change Tracker<br/>Отслеживание изменений]
        DIFF_ENGINE[🔄 Diff Engine<br/>Сравнение версий]
        ROLLBACK[↩️ Rollback<br/>Откат изменений]
    end

    subgraph "Экспорт результатов"
        DOC_GENERATOR[📄 Document Generator<br/>Генерация документов]
        FORMAT_CONVERTER[🔄 Format Converter<br/>Конвертация форматов]
        DOWNLOAD_MANAGER[📥 Download Manager<br/>Управление загрузками]
    end

    %% Процесс загрузки
    DOC_UPLOAD --> DOC_VALIDATION
    DOC_VALIDATION --> DOC_PARSING
    DOC_PARSING --> DOC_INDEXING
    DOC_INDEXING --> DOC_SESSION_MGR

    %% Управление сессией
    DOC_SESSION_MGR --> DOC_CONTEXT
    DOC_SESSION_MGR --> DOC_MEMORY
    DOC_SESSION_MGR --> SESSION_STATE

    %% Операции
    DOC_CONTEXT --> DOC_QA_ENGINE
    DOC_CONTEXT --> DOC_EDIT_ENGINE
    DOC_CONTEXT --> DOC_SUMMARY
    DOC_CONTEXT --> DOC_SEARCH

    %% Версионирование
    DOC_EDIT_ENGINE --> VERSION_CONTROL
    VERSION_CONTROL --> CHANGE_TRACKER
    CHANGE_TRACKER --> DIFF_ENGINE
    VERSION_CONTROL --> ROLLBACK

    %% Экспорт
    DOC_EDIT_ENGINE --> DOC_GENERATOR
    DOC_GENERATOR --> FORMAT_CONVERTER
    FORMAT_CONVERTER --> DOWNLOAD_MANAGER

    %% Стили
    classDef uploadClass fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef sessionClass fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef operationClass fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    classDef versionClass fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef exportClass fill:#ffebee,stroke:#c62828,stroke-width:2px
    
    class DOC_UPLOAD,DOC_VALIDATION,DOC_PARSING,DOC_INDEXING uploadClass
    class DOC_SESSION_MGR,DOC_CONTEXT,DOC_MEMORY,SESSION_STATE sessionClass
    class DOC_QA_ENGINE,DOC_EDIT_ENGINE,DOC_SUMMARY,DOC_SEARCH operationClass
    class VERSION_CONTROL,CHANGE_TRACKER,DIFF_ENGINE,ROLLBACK versionClass
    class DOC_GENERATOR,FORMAT_CONVERTER,DOWNLOAD_MANAGER exportClass
```

## Схема работы режимов чата

```mermaid
sequenceDiagram
    participant U as 👤 Пользователь
    participant MD as 🔍 Mode Detector
    participant CM as 🧠 Context Manager
    participant DM as 📄 Document Mode
    participant IM as 🖼️ Image Mode
    participant VM as 🎤 Voice Mode
    participant AI as 🧠 AI Engine

    alt Отправка документа
        U->>MD: Загружает документ
        MD->>CM: Переключить в Document Mode
        CM->>DM: Активировать режим документа
        DM->>DM: Парсинг и индексация
        DM->>U: "Документ загружен. Режим работы с документом активирован"
        
        loop Работа с документом
            U->>DM: Вопрос по документу
            DM->>AI: Запрос с контекстом документа
            AI-->>DM: Ответ на основе документа
            DM->>U: Ответ с ссылками на разделы
            
            alt Редактирование
                U->>DM: "Измени раздел X"
                DM->>AI: Запрос на редактирование
                AI-->>DM: Предложенные изменения
                DM->>DM: Создать новую версию
                DM->>U: Показать изменения + версия
            end
        end
        
        U->>DM: "Экспортировать документ"
        DM->>U: Готовый файл для скачивания
    
    else Отправка изображения
        U->>MD: Загружает изображение
        MD->>CM: Переключить в Image Mode
        CM->>IM: Активировать режим изображений
        IM->>AI: Анализ изображения
        AI-->>IM: Описание изображения
        IM->>U: Описание + возможности
        
        U->>IM: Вопрос об изображении
        IM->>AI: Запрос с изображением в контексте
        AI-->>IM: Ответ об изображении
        IM->>U: Детальный ответ
    
    else Голосовое сообщение
        U->>MD: Отправляет голос
        MD->>CM: Переключить в Voice Mode
        CM->>VM: Активировать голосовой режим
        VM->>AI: Speech-to-Text + анализ
        AI-->>VM: Текстовый ответ
        VM->>VM: Text-to-Speech
        VM->>U: Голосовой ответ
    
    else Обычный текст
        U->>MD: Печатает текст
        MD->>CM: Обычный режим
        CM->>AI: Стандартный запрос
        AI-->>CM: Обычный ответ
        CM->>U: Текстовый ответ
    end
```
