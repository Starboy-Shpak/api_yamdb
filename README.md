
# API_YAMDB

REST API проект для сервиса YAMDB — платформа для сбора отзывов о фильмах, книгах, музыке и чего угодно еще.

## Что проект умеет?

YAMDB собирает отзывы пользователей на произведения. Произведения делятся на категории: «Книги», «Фильмы», «Музыка» и т.д. Список категорий можно расширить.

### Технологии
Python, DRF, JWT

### Как запустить проект:
- Клонировать репозиторий и перейти в него в командной строке:
```
git clone git@github.com:Starboy-Shpak/api_yamdb.git
cd api_yamdb/
``` 
- Cоздать и активировать виртуальное окружение:
```
python -m venv env
source env/Scripts/activate
``` 
- Установить зависимости из файла requirements.txt:
```
python -m pip install --upgrade pip
pip install -r requirements.txt
``` 
- Перейти в каталог и выполнить миграции:
```
cd api_yamdb/
python manage.py migrate
``` 
- Запустить проект:
```
python manage.py runserver
``` 
### REST API
REST API для примера описан ниже.
- ### Регистрация нового пользователя:

Получить код подтверждения на переданный email. Права доступа: Доступно без токена.

### Request
    POST /api/v1/auth/signup/
```
application/json
{
  "email": "string",
  "username": "string"
}
```
### Response 
```
application/json
{
  "email": "string",
  "username": "string"
}
```
- ### Получение JWT-токена:

Получение JWT-токена в обмен на username и confirmation code. Права доступа: Доступно без токена.

### Request
    POST /api/v1/auth/token/
```
application/json
{
  "username": "string",
  "confirmation_code": "string"
}
```
### Response 
```
application/json
{
  "token": "string"
}
```
- ###  Получение списка всех категорий:

Получить список всех категорий. Права доступа: Доступно без токена.

### Request
    GET /api/v1/categories/

### Response 
```
application/json
[
  {
    "count": 0,
    "next": "string",
    "previous": "string",
    "results": [
      {
        "name": "string",
        "slug": "string"
      }
    ]
  }
]
```
- ### Добавление новой категории:

Создать категорию. Права доступа: Администратор.

### Request
    POST /api/v1/categories/
``` 
application/json
{
  "name": "string",
  "slug": "string"
}
```
### Response 
```
application/json
{
  "name": "string",
  "slug": "string"
}
```
- ### Удаление категории:

Удалить категорию. Права доступа: Администратор.

### Request
    DELETE /api/v1/categories/{slug}/

- ### Получение списка всех жанров:

Получить список всех жанров. Права доступа: Доступно без токена.

### Request
    GET /api/v1/genres/
    
### Response 
```
application/json
[
  {
    "count": 0,
    "next": "string",
    "previous": "string",
    "results": [
      {
        "name": "string",
        "slug": "string"
      }
    ]
  }
]
```
- ### Добавление жанра:

Добавить жанр. Права доступа: Администратор.

### Request
    POST /api/v1/genres/
```
application/json
{
  "name": "string",
  "slug": "string"
}
```
### Response 
```
application/json
{
  "name": "string",
  "slug": "string"
}
```
- ### Удаление категории:

Удалить категорию. Права доступа: Администратор.

### Request
    DELETE /api/v1/genres/{slug}/

- ### Получение списка всех произведений:

Получить список всех объектов. Права доступа: Доступно без токена.

### Request
    GET /api/v1/titles/

### Response 
```
[
  {
    "count": 0,
    "next": "string",
    "previous": "string",
    "results": [
      {
        "id": 0,
        "name": "string",
        "year": 0,
        "rating": 0,
        "description": "string",
        "genre": [
          {
            "name": "string",
            "slug": "string"
          }
        ],
        "category": {
          "name": "string",
          "slug": "string"
        }
      }
    ]
  }
]
```
- ### Добавление произведения:

Добавить новое произведение. Права доступа: Администратор.

### Request
    POST /api/v1/titles/
```
application/json
{
  "name": "string",
  "year": 0,
  "description": "string",
  "genre": [
    "string"
  ],
  "category": "string"
}
```
### Response 
```
application/json
{
  "id": 0,
  "name": "string",
  "year": 0,
  "rating": 0,
  "description": "string",
  "genre": [
    {
      "name": "string",
      "slug": "string"
    }
  ],
  "category": {
    "name": "string",
    "slug": "string"
  }
}
```
- ### Получение информации о произведении:

Информация о произведении. Права доступа: Доступно без токена

### Request
    GET /api/v1/titles/{titles_id}/

### Response 
```
application/json
{
  "id": 0,
  "name": "string",
  "year": 0,
  "rating": 0,
  "description": "string",
  "genre": [
    {
      "name": "string",
      "slug": "string"
    }
  ],
  "category": {
    "name": "string",
    "slug": "string"
  }
}
```
- ### Частичное обновление информации о произведении:

Обновить информацию о произведении. Права доступа: Администратор.

### Request
    PATCH /api/v1/titles/{titles_id}/
```
application/json
{
  "name": "string",
  "year": 0,
  "description": "string",
  "genre": [
    "string"
  ],
  "category": "string"
}
```
### Response 
```
application/json
{
  "id": 0,
  "name": "string",
  "year": 0,
  "rating": 0,
  "description": "string",
  "genre": [
    {
      "name": "string",
      "slug": "string"
    }
  ],
  "category": {
    "name": "string",
    "slug": "string"
  }
}
```
- ### Удаление произведения по id:

Удалить произведение. Права доступа: Администратор.

### Request
    DELETE /api/v1/titles/{titles_id}/

- ### Получение списка всех отзывов:

Получить список всех отзывов. Права доступа: Доступно без токена.

### Request
    GET /api/v1/titles/{title_id}/reviews/

### Response 
```
application/json
[
  {
    "count": 0,
    "next": "string",
    "previous": "string",
    "results": [
      {
        "id": 0,
        "text": "string",
        "author": "string",
        "score": 1,
        "pub_date": "2019-08-24T14:15:22Z"
      }
    ]
  }
]
```
- ### Добавление нового отзыва:

Добавить новый отзыв. Пользователь может оставить только один отзыв на произведение. Права доступа: Аутентифицированные пользователи.

### Request
    POST /api/v1/titles/{title_id}/reviews/
```
application/json
{
  "text": "string",
  "score": 1
}
```
### Response 
```
application/json
{
  "id": 0,
  "text": "string",
  "author": "string",
  "score": 1,
  "pub_date": "2019-08-24T14:15:22Z"
}
```
- ### Получение отзыва по id:

Получить отзыв по id для указанного произведения. Права доступа: Доступно без токена

### Request
    GET /api/v1/titles/{title_id}/reviews/{review_id}/

### Response 
```
application/json
{
  "id": 0,
  "text": "string",
  "author": "string",
  "score": 1,
  "pub_date": "2019-08-24T14:15:22Z"
}
```
- ### Частичное обновление отзыва по id:

Частично обновить отзыв по id. Права доступа: Автор отзыва, модератор или администратор.

### Request
    PATCH /api/v1/titles/{title_id}/reviews/{review_id}/
```
application/json
{
  "text": "string",
  "score": 1
}
```
### Response 
```
application/json
{
  "id": 0,
  "text": "string",
  "author": "string",
  "score": 1,
  "pub_date": "2019-08-24T14:15:22Z"
}
```
- ### Удаление отзыва по id:

Удалить отзыв. Права доступа: Автор отзыва, модератор или администратор.

### Request
    DELETE /api/v1/titles/{title_id}/reviews/{review_id}/

- ### Получение списка всех комментариев к отзыву:

Получить список всех комментариев к отзыву по id. Права доступа: Доступно без токена.

### Request
    GET /api/v1/titles/{title_id}/reviews/{review_id}/comments/

### Response 
```
application/json
[
  {
    "count": 0,
    "next": "string",
    "previous": "string",
    "results": [
      {
        "id": 0,
        "text": "string",
        "author": "string",
        "pub_date": "2019-08-24T14:15:22Z"
      }
    ]
  }
]
```
- ### Добавление комментария к отзыву:

Добавить новый комментарий для отзыва. Права доступа: Аутентифицированные пользователи.

### Request
    POST /api/v1/titles/{title_id}/reviews/{review_id}/comments/
```
application/json
{
  "text": "string"
}
```
### Response 
```
application/json
{
  "id": 0,
  "text": "string",
  "author": "string",
  "pub_date": "2019-08-24T14:15:22Z"
}
```
- ### Получение комментария к отзыву:

Получить комментарий для отзыва по id. Права доступа: Доступно без токена

### Request
    GET /api/v1/titles/{title_id}/reviews/{review_id}/comments/{comment_id}/

### Response 
```
application/json
{
  "id": 0,
  "text": "string",
  "author": "string",
  "pub_date": "2019-08-24T14:15:22Z"
}
```
- ### Частичное обновление комментария к отзыву:

Частично обновить комментарий к отзыву по id. Права доступа: Автор комментария, модератор или администратор.

### Request
    PATCH /api/v1/titles/{title_id}/reviews/{review_id}/comments/{comment_id}/
```
application/json
{
  "text": "string"
}
```
### Response
```
application/json
{
  "id": 0,
  "text": "string",
  "author": "string",
  "pub_date": "2019-08-24T14:15:22Z"
}
```
- ### Удаление комментария к отзыву:

Удалить комментарий к отзыву по id. Автор комментария, модератор или администратор.

### Request
    DELETE /api/v1/titles/{title_id}/reviews/{review_id}/comments/{comment_id}/

- ### Получение списка всех пользователей:

Получить список всех пользователей. Права доступа: Администратор.

### Request
    GET /api/v1/users/

### Response 
```
application/json
[
  {
    "count": 0,
    "next": "string",
    "previous": "string",
    "results": [
      {
        "username": "string",
        "email": "user@example.com",
        "first_name": "string",
        "last_name": "string",
        "bio": "string",
        "role": "user"
      }
    ]
  }
]
```
- ### Добавление пользователя:

Добавить нового пользователя. Права доступа: Администратор.

### Request
    POST /api/v1/users/
```
application/json
{
  "username": "string",
  "email": "user@example.com",
  "first_name": "string",
  "last_name": "string",
  "bio": "string",
  "role": "user"
}
```
### Response 
```
application/json
{
  "username": "string",
  "email": "user@example.com",
  "first_name": "string",
  "last_name": "string",
  "bio": "string",
  "role": "user"
}
```
- ### Получение пользователя по username:

Получить пользователя по username. Права доступа: Администратор.

### Request
    GET /api/v1/users/{username}/

### Response 
```
application/json
{
  "username": "string",
  "email": "user@example.com",
  "first_name": "string",
  "last_name": "string",
  "bio": "string",
  "role": "user"
}
```
- ### Изменение данных пользователя по username:

Изменить данные пользователя по username. Права доступа: Администратор.

### Request
    PATCH /api/v1/users/{username}/
```
application/json
{
  "username": "string",
  "email": "user@example.com",
  "first_name": "string",
  "last_name": "string",
  "bio": "string",
  "role": "user"
}
```
### Response 
```
application/json
{
  "username": "string",
  "email": "user@example.com",
  "first_name": "string",
  "last_name": "string",
  "bio": "string",
  "role": "user"
}
```
- ### Удаление пользователя по username:

Удалить пользователя по username. Права доступа: Администратор.

### Request
    DELETE /api/v1/users/{username}/

- ### Получение данных своей учетной записи:

Получить данные своей учетной записи. Права доступа: Любой авторизованный пользователь.

### Request
    GET /api/v1/users/me/
    
### Response 
```
application/json
{
  "username": "string",
  "email": "user@example.com",
  "first_name": "string",
  "last_name": "string",
  "bio": "string",
  "role": "user"
}
```
- ### Изменение данных своей учетной записи:

Изменить данные своей учетной записи. Права доступа: Любой авторизованный пользователь.

### Request
    PATCH /api/v1/users/me/
```
application/json
{
  "username": "string",
  "email": "user@example.com",
  "first_name": "string",
  "last_name": "string",
  "bio": "string"
}
```
### Response 
```
application/json
{
  "username": "string",
  "email": "user@example.com",
  "first_name": "string",
  "last_name": "string",
  "bio": "string",
  "role": "user"
}
```
### Команда разработчиков:
Кокушин Александр,
Остапюк Ярослав,
Шпак Вадим
---
Автор: Вадим Шпак. Связаться со мной можно в [телеграм](https://t.me/starboy_shpak/)
