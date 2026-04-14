# Скилл: calendar

## CRITICAL: Правила

- Прочитать `ZZ. Служебное/calendar-config.md` ПЕРВЫМ ДЕЛОМ
- Способ доступа определяется полем "Способ" в конфиге: `caldav`, `ics` или `текст`
- Если не подключен -> запустить онбординг из `calendar-config.md`
- НЕ ДОДУМЫВАТЬ содержание событий - показывать только название и время

---

## Чтение событий

### Способ: CalDAV

Запрос REPORT для получения событий на период:

```
curl -s -u "ЛОГИН:ПАРОЛЬ" -X REPORT \
  -H "Content-Type: application/xml" \
  -H "Depth: 1" \
  -d '<?xml version="1.0" encoding="UTF-8"?>
<c:calendar-query xmlns:d="DAV:" xmlns:c="urn:ietf:params:xml:ns:caldav">
  <d:prop><d:getetag/><c:calendar-data/></d:prop>
  <c:filter>
    <c:comp-filter name="VCALENDAR">
      <c:comp-filter name="VEVENT">
        <c:time-range start="YYYYMMDDT000000Z" end="YYYYMMDDT235959Z"/>
      </c:comp-filter>
    </c:comp-filter>
  </c:filter>
</c:calendar-query>' \
  "CALDAV_URL"
```

### Способ: ICS

Загрузить ICS через `fetch` и распарсить VEVENT блоки на нужную дату.

### Способ: текст

Спросить: "Какие встречи и сессии сегодня?"

---

## Добавление событий (только CalDAV)

```
curl -s -u "ЛОГИН:ПАРОЛЬ" -X PUT \
  -H "Content-Type: text/calendar" \
  -d 'BEGIN:VCALENDAR
VERSION:2.0
BEGIN:VEVENT
DTSTART:YYYYMMDDTHHMMSS
DTEND:YYYYMMDDTHHMMSS
SUMMARY:Название
UID:UNIQUE-ID@vault
END:VEVENT
END:VCALENDAR' \
  "CALDAV_URL/UNIQUE-ID.ics"
```

Если способ `ics` или `текст` -> сообщить: "Для добавления событий нужен CalDAV. Хотите настроить?"

---

## Формат ответа

```
# Календарь на сегодня (YYYY-MM-DD)

## События
- HH:MM-HH:MM | Название
- ...

## Окна для фокуса
- HH:MM-HH:MM (N мин)
```

## Правила

- Для клиентских событий не использовать реальные ФИО
- Если данных нет - `[PLACEHOLDER]`, не выдумывать
