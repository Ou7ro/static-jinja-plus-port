# static-jinja-plus-port
Это порт для сборки Docker-образов StaticJinjaPlus из исходного репозитория.

## Возможности

- Сборка из любой версии StaticJinjaPlus (теги, ветки, коммиты)
- Выбор базового образа (Ubuntu или Python slim)
- Автоматическая установка зависимостей

## Быстрый старт

### Сборка с Ubuntu базой (рекомендуется для продакшена)

```bash
# Сборка последней версии из main
docker build -f Dockerfile.ubuntu -t yourname/staticjinjaplus:latest .

# Сборка конкретной версии (например, v1.0.0)
docker build -f Dockerfile.ubuntu \
  --build-arg STATICJINJAPLUS_VERSION=v1.0.0 \
  -t yourname/staticjinjaplus:1.0.0-ubuntu .

# Сборка с другим базовым образом Ubuntu
docker build -f Dockerfile.ubuntu \
  --build-arg BASE_IMAGE=ubuntu:24.04 \
  -t yourname/staticjinjaplus:latest-ubuntu24 .
```

### Сборка с Python slim базой (меньший размер)

```bash
# Сборка последней версии
docker build -f Dockerfile.slim -t yourname/staticjinjaplus:latest-slim .

# Сборка конкретной версии
docker build -f Dockerfile.slim \
  --build-arg STATICJINJAPLUS_VERSION=v1.0.0 \
  -t yourname/staticjinjaplus:1.0.0-slim .

# Сборка с другим Python версией
docker build -f Dockerfile.slim \
  --build-arg BASE_IMAGE=python:3.12-slim \
  -t yourname/staticjinjaplus:latest-py312 .
```

## STATICJINJAPLUS_VERSION
Доступные значения:

main (по умолчанию) - последняя версия из основной ветки

v1.0.0, v2.1.3 - конкретные теги релизов

feature-branch - имя ветки

a1b2c3d - хэш коммита

```bash
docker build -f Dockerfile.ubuntu \
  --build-arg STATICJINJAPLUS_VERSION=v2.0.0 \
  -t myapp:2.0.0 .
```

## BASE_IMAGE
Доступные значения:

Для Ubuntu: ubuntu:22.04, ubuntu:24.04 и т.д.

Для slim: python:3.11-slim, python:3.12-slim и т.д.


## Обновление зависимостей
Для обновления зависимостей отредактируйте файл requirements.txt

### Примечания
Исходный код StaticJinjaPlus не хранится в этом репозитории

Все зависимости скачиваются во время сборки

Для работы с тегами убедитесь, что они существуют в оригинальном репозитории
