# AdminScale Pro

> Веб-приложение для работы с Административной шкалой по методологии Л. Рона Хаббарда.  
> Полностью автономное — один HTML-файл, без сборки и зависимостей.

![AdminScale Pro](https://img.shields.io/badge/AdminScale-Pro-c9a84c?style=flat-square)
![Supabase](https://img.shields.io/badge/Supabase-Cloud%20Sync-3ecf8e?style=flat-square&logo=supabase)
![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Live-blue?style=flat-square&logo=github)

## 🚀 Быстрый старт

### Вариант 1 — GitHub Pages (рекомендуется)

1. Сделайте форк этого репозитория
2. Перейдите в **Settings → Pages**
3. Source: `Deploy from a branch` → branch `main` → folder `/root`
4. Через минуту сайт будет доступен по адресу:  
   `https://YOUR_USERNAME.github.io/adminscale-pro/`

### Вариант 2 — Локально

```bash
git clone https://github.com/YOUR_USERNAME/adminscale-pro.git
cd adminscale-pro
# Просто откройте index.html в браузере
open index.html
```

## ☁ Подключение Supabase (облачное хранение)

Без Supabase данные хранятся в `localStorage` браузера.  
С Supabase — синхронизируются между всеми устройствами.

### 1. Создайте проект на supabase.com

- Перейдите на [supabase.com](https://supabase.com) → New project
- Запомните **Project URL** и **anon/public key** (Settings → API)

### 2. Создайте таблицу

Откройте **SQL Editor** в Supabase и выполните:

```sql
create table if not exists adminscale_scales (
  id text primary key,
  user_id text not null default 'anonymous',
  data jsonb not null,
  updated_at timestamptz default now()
);

alter table adminscale_scales enable row level security;

create policy "allow_anon_all" on adminscale_scales
  for all using (true) with check (true);

create index if not exists idx_scales_user_id
  on adminscale_scales(user_id);
```

### 3. Подключите в приложении

В приложении нажмите **☁ Supabase** в сайдбаре → введите URL и ключ → **Подключить и проверить**.

> ⚠️ Используйте **anon key**, не service_role! Ключи хранятся только в вашем браузере.

## 📐 Структура проекта

```
adminscale-pro/
├── index.html          # Всё приложение в одном файле
├── README.md           # Этот файл
├── .github/
│   └── workflows/
│       └── deploy.yml  # Автодеплой на GitHub Pages
└── supabase/
    └── schema.sql      # SQL-схема для Supabase
```

## ✨ Возможности

| Функция | Описание |
|--------|----------|
| 📋 10-уровневая шкала | Цель → Замыслы → Политика → Планы → Программы → Проекты → Приказы → Идеальная картина → Статистики → ЦКП |
| ⚡ Программы и задачи | Правильная логика: шаг программы = задача с типом |
| 🔧 Проекты | Добавляются к шагу когда тот слишком сложный |
| 📊 5 типов задач | Первоочередные, жизненно важные, условные, текущие, производственные |
| ☁ Supabase sync | Облачное хранение и синхронизация |
| 📄 Экспорт Word | Полный документ с таблицами задач |
| 🧠 Mind-карта | SVG-визуализация с экспортом |
| 💾 JSON export/import | Полный бэкап данных |
| 📚 Справочник | Встроенное руководство по методологии |
| 4 готовых шаблона | Вечер с женой, Экскурсии WISE, Маркетинговое агентство, ТИПы |

## 🧠 Ключевая логика

```
Цель
 └── Замыслы
      └── Политика
           └── Планы
                └── Программы
                     └── Шаги программы (= Задачи)
                          └── Проект (только если шаг слишком сложный)
                               └── Шаги проекта → Приказы
```

**Порядок типов задач — критичен:**
1. 👥 Первоочередные (организация, коммуникации — чаще всего пропускают!)
2. ⚠ Жизненно важные (после инспекции)  
3. 🔍 Условные (если…то — разведка)
4. ⚙ Текущие рабочие (основная масса действий)
5. 📊 Производственные (квоты — ТОЛЬКО после всех остальных!)

## 📝 Лицензия

MIT
