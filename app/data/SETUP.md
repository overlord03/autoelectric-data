# Инструкция: Настройка онлайн-обновлений через GitHub Pages

## Шаг 1: Создайте репозиторий на GitHub

1. Зайдите на https://github.com/new
2. **Repository name:** `autoelectric-data`
3. **Public** (публичный)
4. **НЕ** создавайте README, .gitignore, license
5. Нажмите **Create repository**

## Шаг 2: Загрузите файлы

**Вариант А: Через веб-интерфейс (проще)**

1. В созданном репозитории нажмите **uploading an existing file**
2. Перетащите файлы из архива `data.zip`:
   - `version.json`
   - `carBrands.json`
   - `schematics.json`
   - `README.md`
3. Нажмите **Commit changes**

**Вариант Б: Через Git (если установлен)**

```bash
cd C:\bat\auto-electrician-helper\public\data
git init
git add .
git commit -m "Initial data"
git remote add origin https://github.com/ВАШ_ЛОГИН/autoelectric-data.git
git push -u origin main
```

## Шаг 3: Включите GitHub Pages

1. В репозитории: **Settings** → **Pages**
2. **Source:** Deploy from a branch
3. **Branch:** main → **Save**
4. Подождите 1-2 минуты

URL будет: `https://ВАШ_ЛОГИН.github.io/autoelectric-data/`

## Шаг 4: Настройте приложение

Откройте `lib/remote-data.ts` и замените URL:

```typescript
const DEFAULT_DATA_SOURCE: DataSource = {
  name: "AutoElectric Pro Data",
  url: "https://raw.githubusercontent.com/ВАШ_ЛОГИН/autoelectric-data/main",
  enabled: true,
};
```

Замените `ВАШ_ЛОГИН` на ваш GitHub username.

## Шаг 5: Пересоберите APK

```bash
cd C:\bat\auto-electrician-helper
build-apk.bat
```

## Шаг 6: Проверьте работу

1. Установите APK на телефон
2. Запустите приложение
3. При наличии интернета появится уведомление об обновлении данных

## Как обновлять данные в будущем

1. Отредактируйте файлы в `public/data/`
2. Увеличьте версию в `version.json` (например, `1.0.2`)
3. Загрузите изменения на GitHub (через веб или git)
4. Приложение автоматически увидит обновление

## Готово!

Теперь вы можете обновлять марки, схемы и другие данные без пересборки APK.
