# DoubleSmart | Premium Smart Store

Интернет-магазин электроники с клиентским интерфейсом, панелью администратора, программой лояльности, клиентским хранилищем на **IndexedDB** и серверной архитектурой верифицированных отзывов (**PostgreSQL + Express controller**).

## Структура и функционал

- **Витрина магазина (`index.html`, `style.css`, `script.js`):**
  - Каталог товаров, блок программы лояльности (`#loyalty`), раздел отзывов (`#reviews`), оформление заказов и переключение ролей/тем.
- **Панель администратора (`admin.html`, `admin.js`, `admin.css`):**
  - Разделы управления товарами (фильтрация, модальное редактирование), пользователями, заказами и модерацией отзывов (`renderProducts`, `renderUsers`, `renderOrders`, `renderReviews`), переключение светлой/тёмной темы.
- **Локальное хранилище (`database.js`):**
  - Обёртка над **IndexedDB** (`open`, `replace`, `all`) для клиентской персистентности данных.
- **Backend-архитектура отзывов (`reviews-api.js`, `review-schema.md`):**
  - **PostgreSQL-схема (`review-schema.md`):** тип `review_status` (`PENDING`, `APPROVED`, `HIDDEN`), таблица `reviews` с `UUID`, `JSONB photo_urls`, флагом `verified_purchase` и уникальным индексом `(user_id, item_id)`.
  - **Контроллер отзывов (`reviews-api.js`):** проверка авторизации, запрет на публикацию отзывов от имени администратора (`403 ADMIN_REVIEW_FORBIDDEN`), серверная проверка оплаченного заказа (`COMPLETED`/`PAID`) перед публикацией отзыва и защита от дубликатов (`409 REVIEW_ALREADY_EXISTS`).

## Запуск

- Откройте `index.html` или `admin.html` через любой локальный HTTP-сервер (например, `npx serve .` или Live Server в VS Code).
- SQL-схема для PostgreSQL находится в [`review-schema.md`](review-schema.md), логика API-контроллера — в [`reviews-api.js`](reviews-api.js).
