# 🚀 Инструкция по деплою AdminScale Pro

## Шаг 1 — Загрузите репозиторий на GitHub

### Способ А: через GitHub Desktop (проще)
1. Скачайте [GitHub Desktop](https://desktop.github.com/)
2. File → New Repository → назовите `adminscale-pro`
3. Скопируйте все файлы из этой папки в папку репозитория
4. Commit → Push origin

### Способ Б: через командную строку
```bash
# В папке с файлами проекта:
git init
git add .
git commit -m "Initial commit: AdminScale Pro"

# Создайте репозиторий на github.com, затем:
git remote add origin https://github.com/ВАШ_ЛОГИН/adminscale-pro.git
git branch -M main
git push -u origin main
```

---

## Шаг 2 — Включите GitHub Pages

1. Откройте репозиторий на github.com
2. Перейдите в **Settings** (шестерёнка вверху)
3. Слева выберите **Pages**
4. В разделе **Source** выберите:
   - `Deploy from a branch`
   - Branch: `main`
   - Folder: `/ (root)`
5. Нажмите **Save**
6. Через 1-2 минуты сайт будет доступен по адресу:

```
https://ВАШ_ЛОГИН.github.io/adminscale-pro/
```

> ✅ При каждом `git push` сайт обновляется автоматически через GitHub Actions!

---

## Шаг 3 — Настройте Supabase (опционально)

### 3.1 Создайте проект

1. Зайдите на [supabase.com](https://supabase.com)
2. Sign Up (бесплатно)
3. New Project → заполните название, пароль БД, регион (выберите ближайший к вам)
4. Подождите ~2 минуты пока проект создаётся

### 3.2 Создайте таблицу

1. В левом меню выберите **SQL Editor**
2. Нажмите **New query**
3. Скопируйте содержимое файла `supabase/schema.sql`
4. Нажмите **Run** (или Ctrl+Enter)
5. Внизу должно появиться: `adminscale_scales` — значит таблица создана

### 3.3 Получите ключи

1. В левом меню выберите **Settings** → **API**
2. Скопируйте:
   - **Project URL** (например: `https://abcdefgh.supabase.co`)
   - **anon public** key (длинная строка начинающаяся с `eyJ...`)
   
> ⚠️ Не используйте `service_role` key — он даёт полный доступ к БД!

### 3.4 Подключите в приложении

1. Откройте ваш сайт (GitHub Pages или локально)
2. В левом сайдбаре нажмите **☁ Supabase** (с серой точкой)
3. Вставьте Project URL и anon key
4. Нажмите **🔗 Подключить и проверить**
5. Точка станет зелёной — данные синхронизируются!

---

## Возможные проблемы

### ❌ "relation does not exist"
→ Таблица не создана. Выполните SQL из шага 3.2

### ❌ "new row violates row-level security"
→ RLS политика не создана. Проверьте что выполнили весь SQL-скрипт

### ❌ GitHub Pages показывает 404
→ Подождите 2-3 минуты после включения Pages. Проверьте что файл называется `index.html`

### ❌ "Failed to fetch" при подключении Supabase
→ Проверьте URL — он должен быть точно вида `https://xxxx.supabase.co` (без слеша в конце)

---

## Структура файлов

```
adminscale-pro/
├── index.html              ← Всё приложение
├── README.md               ← Описание проекта  
├── DEPLOY.md               ← Этот файл
├── .gitignore
├── .github/
│   └── workflows/
│       └── deploy.yml      ← Автодеплой на GitHub Pages
└── supabase/
    └── schema.sql          ← SQL для создания таблицы
```
