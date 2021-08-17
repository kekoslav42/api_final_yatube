# api_final
REST API для социальной сети блогеров Yatube, созданной в рамках учебного курса Яндекс.Практикум

Аутентификация по JWT-токену

Поддерживает методы GET, POST, PUT, PATCH, DELETE

# Технологии
Django v2.2.6

REST framework v3.12.4

Авторизация по токену djangorestframework-simplejwt v4.7.2
  
# Запуск на компьтере
1. Клонировать репозиторий
```bash
git clone https://github.com/leks20/api_yatube
```
2. Создать виртуальное окружение и установить зависимости
```bash
python3 -m venv venv
venv/bin/activate
pip install -r requirements.txt
```
3. Выполните миграции
```bash
python manage.py migrate
```
4. Создайте супер пользователя
```bash
python manage.py createsuperuser
```
5. Запустите локальный сервер
```bash
python manage.py runserver
```

Ваш проект запустился на http://127.0.0.1:8000/

Полная документация (redoc.yaml) доступна по адресу http://127.0.0.1:8000/redoc/

# Как работает API
<h3>Пример 1.</h3>

Запрос к API создания поста:
```python
url = 'http://127.0.0.1/api/v1/posts/'
data = {'text': 'POST'}
headers = {'Authorization': 'Bearer TOKEN'}
request = requests.post(url, data=data, headers=headers)
```
Ответ от API:
```json
{
  "id": 0,
  "text": "string",
  "author": "string",
  "pub_date": "2020-08-20T14:15:22Z"
}
```

<h3>Пример 2.</h3>

Запрос к API просмотра подписок:
```python
url = 'http://127.0.0.1:8000/api/v1/follow/'
headers = {'Authorization': 'Bearer TOKEN'}
request = requests.get(api, headers=headers)
```
Ответ от API:
```json
[
  {
    "user": "string",
    "following": "string"
  }
]
```

# Аутентификация 
Для получения токена для работы с API нужно перейти на 
```http://127.0.0.1:8000/jwt/create/```
и передать в запросе username/password.

API вернет токен в виде:
```json
{
    "refresh": "",
    "access": ""
}
```
Токен вернётся в поле access, а данные из поля refresh нужны для обновления токена
