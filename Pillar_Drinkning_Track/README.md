# 🏛️ Pillar — Track Control

> **RU** | [EN ↓](#-pillar--track-control-en)

---

## 🏛️ Pillar — Трекер Привычек и Дел

Минималистичный трекер повседневных привычек и задач с гибким расписанием, историей выполнения и встроенным календарём. Работает полностью в браузере — без серверов, без регистрации, без зависимостей.

---

### 📋 Содержание

- [Возможности](#-возможности)
- [Скриншот / Превью](#-превью)
- [Быстрый старт](#-быстрый-старт)
- [Как пользоваться](#-как-пользоваться)
- [Структура расписания](#-структура-расписания)
- [Хранение данных](#-хранение-данных)
- [Технологии](#-технологии)
- [Структура проекта](#-структура-проекта)
- [Совместимость](#-совместимость)

---

### ✨ Возможности

| Функция | Описание |
|---|---|
| ➕ **Добавление дел** | Создание задачи с названием (до 40 символов) и выбором расписания |
| 📅 **Гибкое расписание** | По дням недели (Пн–Вс) или каждые N дней (интервальный режим) |
| ✅ **Отметка выполнения** | Тап по карточке или кнопке — мгновенное переключение с анимацией |
| 🔵 **История за 7 дней** | Цветные точки: ✓ выполнено · ✗ пропущено · ● сегодня · пусто = не запланировано |
| 📆 **Встроенный календарь** | Цветовая раскраска дней: зелёный / красный / золотой / серый по статусу |
| 🔢 **Счётчик прогресса** | Бейдж «X/Y сделано» в шапке, обновляется в реальном времени |
| 🗂️ **Фильтрация** | Вкладки: Все · Ожидают · Сделаны |
| ⚙️ **Управление делами** | Просмотр всех задач, удаление с подтверждением |
| 🌙 **Автообновление** | Список автоматически сбрасывается в полночь без перезагрузки страницы |
| 💾 **Локальное хранение** | Все данные сохраняются в `localStorage` браузера — никаких серверов |
| ♿ **Доступность** | ARIA-атрибуты, навигация с клавиатуры, метки для скринридеров |
| 📱 **Mobile-first** | Оптимизировано для тач-экранов, safe-area insets, overscroll-behavior |

---

### 🖼️ Превью

Интерфейс использует тёмную тему (`#0C0C0C`) с золотыми акцентами (`#C9A84C`). Карточки дел анимируются при появлении, отметка выполнения сопровождается ripple-эффектом.

**Цветовой код истории и календаря:**

| Цвет | Значение |
|---|---|
| 🟢 Зелёный | Выполнено |
| 🔴 Красный | Пропущено |
| 🟡 Золотой | Ожидается (сегодня) |
| ⚫ Серый | Нет в расписании |

---

### 🚀 Быстрый старт

Никаких установок не требуется.

```bash
# Просто откройте файл в браузере:
open Pillar__Track_Control.html

# Или разместите на GitHub Pages / любом статичном хостинге
```

Файл полностью самодостаточен. Единственная внешняя зависимость — шрифты Google Fonts (загружаются при наличии интернета; без сети используется системный sans-serif).

---

### 📖 Как пользоваться

#### Добавить дело
1. Нажмите кнопку **«+ Добавить»** внизу экрана.
2. Введите название (например: «Утренняя зарядка»).
3. Выберите расписание — **по дням недели** или **каждые N дней**.
4. Нажмите **«Сохранить»**.

#### Отметить выполнение
- Тапните на карточку задачи (на тач-устройствах) или кликните (на ПК).
- Карточка становится полупрозрачной, золотая галочка подтверждает выполнение.
- Повторный тап снимает отметку.

#### Просмотр истории
- Под каждой задачей — строка из 7 точек, показывающая статус за последние 7 дней.
- Ниже — дата следующего запланированного выполнения.

#### Работа с календарём
- Нажмите 📅 в правом верхнем углу, чтобы открыть/закрыть панель.
- Навигация по месяцам стрелками ◀ ▶.
- Тап на день с делами показывает тост-уведомление: «N/M сделаны».

#### Управление делами
- Нажмите ⚙️ — откроется список всех задач с кнопкой «Удалить».
- Удаление необратимо и очищает всю историю выполнений для задачи.

---

### 📐 Структура расписания

Каждое дело хранит один из двух типов расписания:

**Еженедельное (`weekly`)**
```json
{
  "scheduleType": "weekly",
  "days": [1, 3, 5]
}
```
`days` — массив чисел от 0 (Вс) до 6 (Сб), соответствующих `Date.getDay()`.

**Интервальное (`interval`)**
```json
{
  "scheduleType": "interval",
  "interval": 3,
  "startDate": "2025-01-01"
}
```
Задача показывается, если `(текущая дата - startDate) % interval === 0`.

---

### 💾 Хранение данных

Данные хранятся в двух ключах `localStorage`:

| Ключ | Содержимое |
|---|---|
| `pt_pillars` | JSON-массив всех задач (название, расписание, ID) |
| `pt_completions` | JSON-объект `{ "YYYY-MM-DD": ["id1", "id2"] }` — выполнения по датам |

Данные **не покидают устройство**. Очистить их можно через DevTools → Application → Local Storage.

---

### 🛠️ Технологии

| Технология | Версия / Детали |
|---|---|
| HTML5 | Семантическая разметка, ARIA |
| CSS3 | CSS-переменные, Grid, Flexbox, анимации, `@keyframes` |
| JavaScript | Vanilla ES6+, `localStorage` API |
| Google Fonts | Playfair Display (700), DM Sans (400/500/600) |
| Зависимости | **Нет** (нулевые npm/CDN зависимости, кроме шрифтов) |

---

### 📁 Структура проекта

```
Pillar__Track_Control.html   ← единственный файл, всё внутри
│
├── <head>
│   ├── Google Fonts (Playfair Display, DM Sans)
│   └── <style> — все стили (CSS-переменные, компоненты, анимации)
│
├── <body>
│   ├── .header — шапка (дата, прогресс-бейдж, кнопки)
│   ├── .calendar-section — раскрывающийся календарь
│   ├── .main — список карточек дел
│   ├── .fab — кнопка «Добавить»
│   ├── #addModal — модалка создания дела
│   └── #manageModal — модалка управления делами
│
└── <script>
    ├── Хранение: loadData / savePillarsToStorage / saveCompletionsToStorage
    ├── Логика: shouldShowOnDate / pillarDueToday / getNextDose
    ├── Рендер: renderHeader / renderPillars / renderCalendar / renderHistoryHTML
    └── UI: openAddModal / closeAddModal / savePillar / deletePillar / showToast
```

---

### 🌐 Совместимость

| Среда | Статус |
|---|---|
| Chrome (Android/Desktop) | ✅ Полная поддержка |
| Safari (iOS/macOS) | ✅ Полная поддержка |
| Firefox | ✅ Полная поддержка |
| Samsung Internet | ✅ Полная поддержка |
| Termux + браузер | ✅ Работает (локальный файл) |
| GitHub Pages | ✅ Готов к деплою без изменений |

---

---

## 🏛️ Pillar — Track Control (EN)

A minimalist habit and task tracker with flexible scheduling, 7-day history, and a built-in calendar. Runs entirely in the browser — no server, no account, no dependencies.

---

### 📋 Table of Contents

- [Features](#-features)
- [Quick Start](#-quick-start)
- [How to Use](#-how-to-use)
- [Schedule Types](#-schedule-types)
- [Data Storage](#-data-storage)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Browser Compatibility](#-browser-compatibility)

---

### ✨ Features

| Feature | Description |
|---|---|
| ➕ **Add Tasks** | Create a task with a name (up to 40 chars) and a schedule |
| 📅 **Flexible Scheduling** | Weekly (by day of week) or every N days (interval mode) |
| ✅ **Completion Toggle** | Tap a card to mark done/undone with ripple animation |
| 🔵 **7-Day History** | Colored dots: ✓ done · ✗ missed · ● today · dot = not scheduled |
| 📆 **Built-in Calendar** | Days color-coded: green / red / gold / grey by completion status |
| 🔢 **Progress Counter** | "X/Y done" badge in the header, updated in real time |
| 🗂️ **Filtering** | Tabs: All · Pending · Done |
| ⚙️ **Task Management** | View all tasks, delete with confirmation |
| 🌙 **Auto-refresh** | List resets at midnight without a page reload |
| 💾 **Local Storage** | All data saved in the browser's `localStorage` — no server needed |
| ♿ **Accessibility** | ARIA attributes, keyboard navigation, screen reader labels |
| 📱 **Mobile-first** | Optimized for touch screens, safe-area insets, overscroll-behavior |

---

### 🚀 Quick Start

No installation required.

```bash
# Simply open the file in any browser:
open Pillar__Track_Control.html

# Or deploy to GitHub Pages / any static host
```

The file is fully self-contained. The only external dependency is Google Fonts — loaded when online; falls back to system sans-serif when offline.

---

### 📖 How to Use

#### Add a Task
1. Tap the **"+ Add"** button at the bottom of the screen.
2. Enter a name (e.g. "Morning Run").
3. Choose a schedule — **by days of the week** or **every N days**.
4. Tap **"Save"**.

#### Mark as Done
- Tap a task card (on touch devices) or click (on desktop).
- The card fades, and a gold checkmark confirms completion.
- Tap again to undo.

#### View History
- Below each task is a row of 7 dots showing status over the last 7 days.
- Below that is the date of the next scheduled occurrence.

#### Calendar Panel
- Tap 📅 in the top-right to toggle the calendar.
- Navigate months with ◀ ▶ arrows.
- Tapping a day with tasks shows a toast: "N/M done".

#### Manage Tasks
- Tap ⚙️ to open the full task list.
- Each entry has a "Delete" button — deletion is permanent and removes all history for that task.

---

### 📐 Schedule Types

Each task stores one of two schedule types:

**Weekly (`weekly`)**
```json
{
  "scheduleType": "weekly",
  "days": [1, 3, 5]
}
```
`days` is an array of integers 0 (Sun) – 6 (Sat), matching `Date.getDay()`.

**Interval (`interval`)**
```json
{
  "scheduleType": "interval",
  "interval": 3,
  "startDate": "2025-01-01"
}
```
A task appears when `(currentDate - startDate) % interval === 0`.

---

### 💾 Data Storage

Data is persisted in two `localStorage` keys:

| Key | Contents |
|---|---|
| `pt_pillars` | JSON array of all tasks (name, schedule, ID) |
| `pt_completions` | JSON object `{ "YYYY-MM-DD": ["id1", "id2"] }` — completions by date |

Data **never leaves the device**. To clear it: DevTools → Application → Local Storage.

---

### 🛠️ Tech Stack

| Technology | Details |
|---|---|
| HTML5 | Semantic markup, ARIA roles |
| CSS3 | Custom properties, Grid, Flexbox, `@keyframes` animations |
| JavaScript | Vanilla ES6+, `localStorage` API |
| Google Fonts | Playfair Display (700), DM Sans (400/500/600) |
| Dependencies | **None** (zero npm/CDN, fonts only) |

---

### 📁 Project Structure

```
Pillar__Track_Control.html   ← single file, everything inside
│
├── <head>
│   ├── Google Fonts (Playfair Display, DM Sans)
│   └── <style> — all styles (CSS variables, components, animations)
│
├── <body>
│   ├── .header — top bar (date, progress badge, action buttons)
│   ├── .calendar-section — collapsible calendar panel
│   ├── .main — task card list
│   ├── .fab — "Add" floating action button
│   ├── #addModal — task creation bottom sheet
│   └── #manageModal — task management bottom sheet
│
└── <script>
    ├── Storage: loadData / savePillarsToStorage / saveCompletionsToStorage
    ├── Logic: shouldShowOnDate / pillarDueToday / getNextDose
    ├── Render: renderHeader / renderPillars / renderCalendar / renderHistoryHTML
    └── UI: openAddModal / closeAddModal / savePillar / deletePillar / showToast
```

---

### 🌐 Browser Compatibility

| Environment | Status |
|---|---|
| Chrome (Android / Desktop) | ✅ Full support |
| Safari (iOS / macOS) | ✅ Full support |
| Firefox | ✅ Full support |
| Samsung Internet | ✅ Full support |
| Termux + mobile browser | ✅ Works (local file) |
| GitHub Pages | ✅ Deploy-ready with no changes |

---

<p align="center">
  Built with vanilla HTML · CSS · JS &nbsp;·&nbsp; Zero dependencies &nbsp;·&nbsp; Single file
</p>
