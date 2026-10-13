# Контейнеризация и оркестрация. Лабораторная работа 2

Лясин Илья

---

## Структура

- Dockerfile - файл до оптимизации
- Dockerfile.optimized - после оптимизации
- App/assist.py. Программа, которая запускается внутри контейнера
- requirements.txt - зависимости программы

## Как запустить

```bash
docker built -t myapp -f Dockerfile.optimized .

docker run -d \
  --name <фамилия>-assistant-final \
  -p <ваш_порт>:<ваш_порт> \
  -e APP_OWNER=<ваша_фамилия> \
  -e APP_SECRET=<ваш_секретный_ключ> \
  <фамилия>-assistant:final
```

## Проверка

```bash
# Проверка главной страницы
curl http://localhost:<ваш_порт>/

# Проверка персонализации
curl http://localhost:<ваш_порт>/me

# Тест заметок
curl -X POST http://localhost:<ваш_порт>/notes \
  -H "Content-Type: application/json" \
  -d '{"text": "ЛР2: сборка образа"}'

curl http://localhost:<ваш_порт>/notes

# Тест секретного эндпоинта (должен вернуть флаг!)
curl http://localhost:<ваш_порт>/secret/<ваш_секретный_ключ>
```