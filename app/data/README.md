# AutoElectric Pro — Данные для онлайн-обновлений

## Что это

Этот репозиторий содержит данные для приложения AutoElectric Pro. Приложение загружает эти данные при запуске, что позволяет обновлять контент без пересборки APK.

## Структура

```
data/
├── version.json      # Версия данных
├── carBrands.json    # Марки и модели автомобилей
├── schematics.json   # Электрические схемы
├── scanners.json     # Диагностические сканеры
└── scenarios.json    # Сценарии диагностики
```

## Как обновлять данные

1. Отредактируйте нужный файл (например, `carBrands.json`)
2. Увеличьте версию в `version.json` (например, `1.0.2`)
3. Закоммитьте и запушьте изменения:
   ```bash
   git add .
   git commit -m "Update car brands"
   git push
   ```
4. Приложение автоматически увидит обновление при следующем запуске

## Формат данных

### version.json
```json
{
  "version": "1.0.1",
  "updatedAt": "2026-11-02T00:00:00Z"
}
```

### carBrands.json
Массив марок с моделями:
```json
[
  {
    "id": "toyota",
    "name": "Toyota",
    "models": [
      {"id": "camry", "name": "Camry", "years": "2006-2024"}
    ]
  }
]
```

### schematics.json
Массив схем с привязкой к марке/модели:
```json
[
  {
    "id": "car-starting",
    "carBrandId": "universal",
    "carModelIds": [],
    "category": "starting-charging",
    "title": "Система запуска",
    "diagrams": [...]
  }
]
```

## Настройка в приложении

В файле `lib/remote-data.ts` замените URL на ваш:

```typescript
const DEFAULT_DATA_SOURCE: DataSource = {
  name: "AutoElectric Pro Data",
  url: "https://raw.githubusercontent.com/ВАШ_ЛОГИН/autoelectric-data/main",
  enabled: true,
};
```

После изменения URL пересоберите APK:
```bash
build-apk.bat
```
