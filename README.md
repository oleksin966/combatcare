# CombatCare

Веб-платформа для координації волонтерської допомоги військовим. Система дозволяє волонтерам керувати складом, обробляти замовлення та спілкуватися з військовими в режимі реального часу.

## Технології

- **Backend:** Django 4.x + Django Channels (WebSocket)
- **Server:** Daphne (ASGI)
- **Database:** PostgreSQL
- **Proxy:** Nginx
- **Containerization:** Docker + Docker Compose
- **SSL:** Let's Encrypt

## Функціонал

- Управління складом (товари, категорії, підкатегорії)
- Система замовлень
- Чат в реальному часі (WebSocket)
- Ролі користувачів: військовий, волонтер, кур'єр
- Відстеження доставки з геолокацією (Google Maps)
- Кошик

## Структура проекту

```
combatcare/
├── accounts/        # Користувачі та авторизація
├── cartitem/        # Кошик
├── chat/            # Чат (WebSocket)
├── combatecare/     # Налаштування Django (settings, urls, asgi)
├── delivery/        # Доставка
├── ordering/        # Замовлення
├── warehouse/       # Склад
├── static/          # Статичні файли
├── media/           # Медіафайли (фото товарів)
├── Dockerfile
├── docker-compose.yml
├── nginx.conf
└── requirements.txt
```

## Запуск через Docker

### 1. Клонуй репозиторій

```bash
git clone https://github.com/oleksin966/combatcare.git
cd combatcare
```

### 2. Створи файл .env

```bash
cp .env.example .env
```

Заповни значення в `.env`:

```
SECRET_KEY=your_secret_key
DEBUG=False
ALLOWED_HOSTS=your_domain.com

DB_NAME=combatcare
DB_USER=postgres
DB_PASSWORD=your_password
DB_HOST=db
DB_PORT=5432
```

### 3. Отримай SSL сертифікат

```bash
sudo apt install certbot -y
sudo certbot certonly --standalone -d your_domain.com
```

### 4. Запусти проект

```bash
docker-compose up --build -d
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py collectstatic --noinput
docker-compose exec web python manage.py createsuperuser
```

## Доступ

- Сайт: `https://combatcare.pp.ua`
- Адмін панель: `https://combatcare.pp.ua/admin`

## Змінні оточення (.env.example)

```
SECRET_KEY=
DEBUG=
ALLOWED_HOSTS=

DB_NAME=
DB_USER=
DB_PASSWORD=
DB_HOST=db
DB_PORT=5432
```

## Вимоги

- Docker
- Docker Compose
- Certbot (для SSL)
