# Скилл: calendar

Показывает расписание на день из подключенного календаря. Только чтение.

## Быстрый сценарий

### Шаг 1. Проверить подключение

1. Прочитать `ZZ. Служебное/calendar-config.md`
2. Если `ics_url` заполнен - загрузить календарь:
   ```shell
   source "ZZ. Служебное/venv/.venv/bin/activate"
   python3 -c "
   import urllib.request, icalendar
   from datetime import date, datetime, timezone
   data = urllib.request.urlopen('[ICS_URL]').read()
   cal = icalendar.Calendar.from_ical(data)
   today = date.today()
   for event in cal.walk('VEVENT'):
       start = event.get('DTSTART').dt
       if hasattr(start, 'date'):
           d = start.date()
       else:
           d = start
       if d == today:
           print(f'{start} | {event.get(\"SUMMARY\")}')
   "
   ```
3. Если `ics_url` пуст - запустить onboarding (см. `calendar-config.md`, секция "Первое подключение")

### Шаг 2. Структурированный ответ

Сформировать:
- Сколько событий сегодня
- Ближайшее событие
- Окна для фокусной работы между событиями

```
# Календарь на сегодня (YYYY-MM-DD)

## События
- HH:MM-HH:MM | Название
- ...

## Окна для фокуса
- HH:MM-HH:MM (N мин)
- ...
```

### Шаг 3. Интеграция с планированием

В конце предложить:
- Показать задачи из недельного плана на сегодня
- Сохранить план дня в `01. Планирование/YYYY/MM/YYYY-MM-DD.md`

## Если календарь не подключен

Спросить: "Расскажите, какие встречи и сессии у вас сегодня?" и работать с текстовым вводом.

## Правила

- Только чтение. ICS-ссылка не позволяет менять события.
- Для клиентских событий не используй реальные ФИО - только псевдонимы/инициалы.
- Если данных нет - `[PLACEHOLDER]`, не выдумывай.
