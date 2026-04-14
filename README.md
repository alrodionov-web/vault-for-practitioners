# Хранилище помогающего практика

Персональное хранилище знаний для психологов, коучей, тренеров и консультантов. Работает в редакторе Zed с AI-ассистентом.

## Быстрый старт

### 1. Установить Zed

Бесплатный редактор с встроенным AI-ассистентом. Скачайте и установите:

- **Mac (Apple Silicon - M1/M2/M3/M4):** [скачать .dmg](https://github.com/zed-industries/zed/releases/latest/download/Zed-aarch64.dmg)
- **Mac (Intel):** [скачать .dmg](https://github.com/zed-industries/zed/releases/latest/download/Zed-x86_64.dmg)
- **Windows (ARM):** [скачать .exe](https://github.com/zed-industries/zed/releases/latest/download/Zed-aarch64.exe)
- **Windows (Intel/AMD):** [скачать .exe](https://github.com/zed-industries/zed/releases/latest/download/Zed-x86_64.exe)

Не знаете какой Mac? Меню Apple () -> "Об этом Mac" -> если написано "Apple M..." - выбирайте Apple Silicon.

На Mac: откройте скачанный `.dmg` и перетащите Zed в папку Applications. Запустите Zed. При первом запуске появится экран настроек - включите **Trust All Projects By Default** и нажмите **Finish Setup**.

### 2. Скачать хранилище

1. Перейдите на [github.com/alrodionov-web/vault-for-practitioners](https://github.com/alrodionov-web/vault-for-practitioners)
2. Нажмите зеленую кнопку **Code** -> **Download ZIP**
3. Распакуйте архив (двойной клик на Mac, правый клик -> "Извлечь все" на Windows)
4. Переименуйте папку `vault-for-practitioners-main` в удобное название (например, `Моя практика`)
5. Переместите папку в удобное место (например, `Документы/`)

### 3. Подключить AI-модель

Хранилище работает с DeepSeek через [ProxyAPI](https://proxyapi.ru) - сервис доступа к AI-моделям с оплатой в рублях, без VPN.

**Шаг 1.** В Zed откройте файл настроек: меню `Zed -> Settings -> Open Settings File` (Mac) или `File -> Settings -> Open Settings File` (Windows/Linux). Откроется файл `settings.json` с комментариями и базовыми настройками.

**Шаг 2.** Выделите все содержимое файла (`Cmd+A` на Mac, `Ctrl+A` на Windows) и замените на блок ниже (скопируйте его целиком):

```json
{
  "language_models": {
    "openai_compatible": {
      "proxyapi_deepseek": {
        "api_url": "https://openai.api.proxyapi.ru/v1",
        "available_models": [
          {
            "name": "openrouter/deepseek/deepseek-v3.2",
            "display_name": "DeepSeek V3.2 (ProxyAPI)",
            "max_tokens": 128000
          },
          {
            "name": "openrouter/deepseek/deepseek-r1",
            "display_name": "DeepSeek R1 (ProxyAPI)",
            "max_tokens": 128000
          }
        ]
      }
    }
  },
  "agent": {
    "default_model": {
      "provider": "proxyapi_deepseek",
      "model": "openrouter/deepseek/deepseek-v3.2"
    },
    "tool_permissions": {
      "default": "allow"
    }
  },
  "git": {
    "git_gutter": "hide",
    "inline_blame": { "enabled": false }
  },
  "scrollbar": { "git_diff": false },
  "tabs": { "git_status": false },
  "project_panel": { "git_status": false },
  "git_panel": { "button": false, "starts_open": false }
}
```

**Шаг 3.** Сохраните файл (`Cmd+S` на Mac, `Ctrl+S` на Windows). Закройте и снова откройте Zed.

**Шаг 4.** На экране Welcome нажмите **Open Project** -> выберите папку хранилища, которую скачали на шаге 2.

**Шаг 5.** Откройте [proxyapi.ru](https://proxyapi.ru), создайте аккаунт и пополните баланс (от 100 руб, DeepSeek стоит ~0.5-2 руб за запрос). Скопируйте API-ключ (начинается с `sk-`).

**Шаг 6.** Вернитесь в Zed. Нажмите иконку с искрой (✦) в правом нижнем углу - откроется панель AI-ассистента. Теперь нужно ввести API-ключ:
1. В нижней части панели нажмите на название модели
2. В появившемся окне нажмите **Configure**
3. Найдите в списке **proxyapi_deepseek** и раскройте его (нажмите на стрелку)
4. Вставьте скопированный API-ключ в поле ввода и нажмите Enter
5. Ключ сохранится, повторно вводить не нужно

### 4. Начать работу

Напишите в панели ассистента что хотите - AI сам определит нужный процесс:

| Что сказать AI | Статус |
|----------------|--------|
| "спланируй неделю", "план на день", "статус на сегодня", "итоги месяца", "поставь цели" | готов |
| "что в календаре", "добавь встречу в календарь" | готов |
| "запиши оплату", "сколько заработал", "отчет за месяц" | в планах |
| "у меня идея", "придумать", "что если" | в планах |
| "напиши пост", "упакуй услугу" | в планах |
| "новый клиент", "запиши сессию" | в планах |
| "новый тренинг", "план занятия" | в планах |
| "расшифруй аудио", "обнови хранилище" | в планах |

**Доступные модели:**

| Модель | Для чего |
|--------|---------|
| DeepSeek V3.2 | Основная - быстрая, хорошо работает с текстом и планированием |
| DeepSeek R1 | Для сложных задач, требующих рассуждения (медленнее, но глубже) |

## Полезные программы

- [OpenWhispr](https://openwhispr.com) - голосовой ввод для вашего AI-ассистента. Работает локально и бесплатно - просто говорите вместо того, чтобы печатать.
- [Obsidian](https://obsidian.md) - удобный просмотрщик вашего хранилища. Zed - это "дверь" для AI-агента в ваше хранилище, Obsidian - для вас. Откройте ту же папку в Obsidian, чтобы удобно читать и редактировать заметки.

## Конфиденциальность

- API-ключ хранится в системной связке ключей, не в файлах
- Данные хранилища остаются на вашем компьютере
- AI-провайдер получает только текст, который вы отправляете в чат

## Файлы-примеры

В папках хранилища есть файлы с `[example]` в названии - это образцы, показывающие как выглядят заполненные документы. Можете использовать их как шаблон или просто удалить.
