## proxy_amoCRM
___
### Ключевые тебования
### Как работает программа
### Описание структыры проекта
### Эндпоиты
### Запуск программы
### Логирование
___

### Ключевые тебования
Для работы необходим **Python 3.10.2** и выше.<br>
Файл ***requirements.txt*** содержит список всех необходимых пакетов.<br>
___
### Как работает программа
___
### Описание структуры проекта
___
### Эндпоиты
####***/TwinProxy/amoCRM/info*** - общая информация о прокси сервисе
method: **GET**
___
####***/TwinProxy/amoCRM/LoginPasswordInfo*** - требования к логину и паролю для регистрации в системе
method: **GET**
___
####***/TwinProxy/amoCRM/registration*** - регистрация нового пользователя в базе данных
method: **POST**

**Request body:**
```json
{
  "login": "real_user_01",
  "password": "Qwerty123",
  "client_id": "5555f76e2-446f-412d-b999-6a72db60b31b",
  "client_secret": "9rEXDECXnnZBAW9LGwITiMNulB9RQAtULS8CjC5BQrjQ2vmPOfrekhTeuU9Fbmt1",
  "client_link": "https://realuser1",
  "code": "def502002b5...f4afc20ab6",
  "redirect_uri": "https://bestuser.wdza.ru/"
}
```
<br>

**Response, code 200:**

```json
{
    "status": "Новый пользователь 001_user успешно зарегестрирован",
    "token": "eyJ0eXAiOi...sg0MgWF5xg",
    "refresh_token": "def5020051...1c34dc4e51",
    "ttl": 86400
}
```
<br>

**Response, code 400:**<br>
детали: код уже был успешно использован ранее для регистрации пользователя и был отозван системой amoCRM
```json
{
    "status": "Ошибка при получении данных токена. Проверьте данные.",
    "amoCRM_error_description": {
        "hint": "Authorization code has been revoked",
        "title": "Некорректный запрос",
        "type": "https://developers.amocrm.ru/v3/errors/OAuthProblemJson",
        "status": 400,
        "detail": "В запросе отсутствует ряд параметров или параметры невалидны"
    },
    "endpoint": "registration",
    "timestamp": "2022-12-23 13:55:30.627243"
}
```

<br>

**Response, code 400:**<br>
детали: ошибка в параметре *client_id*
```json
{
    "status": "Ошибка при получении данных токена. Проверьте данные.",
    "amoCRM_error_description": {
        "hint": "Check the `client_id` parameter",
        "title": "Некорректный запрос",
        "type": "https://developers.amocrm.ru/v3/errors/OAuthProblemJson",
        "status": 400,
        "detail": "В запросе отсутствует ряд параметров или параметры невалидны"
    },
    "endpoint": "registration",
    "timestamp": "2022-12-23 13:55:30.627243"
}
```

<br>

**Response, code 400:**<br>
детали: ошибка в параметре *client_secret*
```json
{
    "status": "Ошибка при получении данных токена. Проверьте данные.",
    "amoCRM_error_description": {
        "hint": "Check the `client_secret` parameter",
        "title": "Некорректный запрос",
        "type": "https://developers.amocrm.ru/v3/errors/OAuthProblemJson",
        "status": 400,
        "detail": "В запросе отсутствует ряд параметров или параметры невалидны"
    },
    "endpoint": "registration",
    "timestamp": "2022-12-23 13:55:30.627243"
}
```

<br>

**Response, code 400:**<br>
детали: ошибка в параметре *redirect_uri*
```json
{
    "status": "Ошибка при получении данных токена. Проверьте данные.",
    "amoCRM_error_description": {
        "hint": "Redirect URI is not associated with client",
        "title": "Некорректный запрос",
        "type": "https://developers.amocrm.ru/v3/errors/OAuthProblemJson",
        "status": 400,
        "detail": "В запросе отсутствует ряд параметров или параметры невалидны"
    },
    "endpoint": "registration",
    "timestamp": "2022-12-23 13:55:30.627243"
}
```

<br>

**Response, code 400:**<br>
детали: ошибка в параметре *client_link*
```json
{
    "status": "Ошибка при получении данных токена. Проверьте данные.",
    "amoCRM_error_description": {
        "hint": "Invalid account",
        "title": "Некорректный запрос",
        "type": "https://developers.amocrm.ru/v3/errors/OAuthProblemJson",
        "status": 400,
        "detail": "В запросе отсутствует ряд параметров или параметры невалидны"
    },
    "endpoint": "registration",
    "timestamp": "2022-12-23 13:55:30.627243"
}
```
<br>

**Response, code 422:**<br>
детали: пользователь с таким логином уже существует

```json
{
    "status": "Пользователь c логином 001_user уже существует. Укажите другой логин.",
    "endpoint": "registration",
    "timestamp": "2022-12-23 13:55:30.627243"
}
```
<br>

**Response, code 422:**<br>
детали: логин не соответствует предъявляемым требованиям (аналогично для пароля)

```json
{
    "status": "При валидации данных произошла ошибка. Проверьте логин и пароль на соответствие требованиям.",
    "error_description": "1 validation error for Request\nbody -> login\n  ensure this value has at least 5 characters (type=value_error.any_str.min_length; limit_value=5)",
    "endpoint": "exception_handler",
    "timestamp": "2022-12-23 13:55:30.627243"
}
```
<br>

**Response, code 500:**<br>

```json
{
  "status": "Ошибка сервера.",
  "endpoint": "registration",
  "timestamp": "2022-12-23 13:55:30.627243"
}
```
___

####***/TwinProxy/amoCRM/getToken")*** - получить токен и рефреш-токен
method: **GET**

**Request body:**
```json
{
  "login": "real_user_01",
  "password": "Qwerty123"
}
```
<br>

**Response, code 200:**<br>

```json
{
    "status": "Данные успешно получены.",
    "client_link": "https://realuser1",
    "token": "eyJ0eXAiOi...sg0MgWF5xg",
    "refresh_token": "def5020051...1c34dc4e51",
    "ttl": 86400
}
```
<br>


**Response, code 401:**<br>
детали: неправильно указан логин или пароль

```json
{
    "status": "Не удалось получить данные. Проверьте логин и пароль.",
    "error_description": "неверный логин или пароль",
    "endpoint": "getToken",
    "timestamp": "2022-12-12 15:55:30.123456"
}
```
<br>

**Response, code 422:**<br>
детали: запрос к БД выполнен, но в ответ данные не пришли

```json
{
    "status": "Не удалось получить данные. Проверьте логин и пароль.",
    "error_description": "Запрос к БД выполнен, но в ответ данные не пришли",
    "endpoint": "getToken",
    "timestamp": "2022-12-12 15:55:30.123456"
}
```
<br>

**Response, code 500:**<br>

```json
{
  "status": "Ошибка сервера.",
  "endpoint": "changePassword",
  "timestamp": "2022-12-12 15:55:30.123456"
}
```
___
####***/TwinProxy/amoCRM/deleteUser*** - удалить пользователя
method: **DELETE**

**Request body:**
```json
{
  "login": "real_user_01",
  "password": "Qwerty123",
  "client_link": "https://realuser1"
}
```
<br>

**Response, code 200:**<br>

```json
{
    "status_": "Пользователь 006_user удален."
}
```
<br>

**Response, code 401:**<br>

```json
{
    "status": "Не удалось удалить пользователя. Проверьте логин и пароль.",
    "error_description": "неверный логин или пароль",
    "endpoint": "deleteUser",
    "timestamp": "2022-12-12 15:55:30.123456"
}
```
<br>

**Response, code 422:**<br>

```json
{
    "status": "При валидации данных произошла ошибка. Проверьте логин и пароль на соответствие требованиям.",
    "error_description": "2 validation errors for Request\nbody -> login\n  ensure this value has at least 5 characters (type=value_error.any_str.min_length; limit_value=5)\nbody -> password\n  ensure this value has at least 5 characters (type=value_error.any_str.min_length; limit_value=5)",
    "endpoint": "exception_handler",
    "timestamp": "2022-12-12 15:55:30.123456"
}
```
<br>

**Response, code 500:**<br>

```json
{
  "status": "Ошибка сервера.",
  "endpoint": "deleteUser",
  "timestamp": "2022-12-23 13:55:30.627243"
}
```
___
####***/TwinProxy/amoCRM/changePassword*** - изменить пароль пользователя
method: **PATCH**

**Request body:**
```json
{
  "login": "real_user_01",
  "password": "Qwerty123",
  "new_password": "321Qwerty"
}
```
<br>

**Response, code 200:**<br>

```json
{
    "status": "Пароль успешно изменен."
}
```
<br>

**Response, code 401:**<br>

```json
{
    "status": "Не удалось изменить пароль. Проверьте логин и пароль.",
    "error_description": "неверный логин или пароль",
    "endpoint": "changePassword",
    "timestamp": "2022-12-12 15:55:30.123456"
}
```
<br>

**Response, code 422:**<br>

```json
{
    "status": "При валидации данных произошла ошибка. Проверьте логин и пароль на соответствие требованиям.",
    "error_description": "2 validation errors for Request\nbody -> login\n  ensure this value has at least 5 characters (type=value_error.any_str.min_length; limit_value=5)\nbody -> password\n  ensure this value has at least 5 characters (type=value_error.any_str.min_length; limit_value=5)",
    "endpoint": "exception_handler",
    "timestamp": "2022-12-12 15:55:30.123456"
}
```
<br>

**Response, code 500:**<br>

```json
{
  "status": "Ошибка сервера.",
  "endpoint": "changePassword",
  "timestamp": "2022-12-12 15:55:30.123456"
}
```
___
####***/TwinProxy/amoCRM/changeClientLink*** - изменить ссылку клиента (client_link) пользователя
method: **PATCH**

**Request body:**
```json
{
  "login": "real_user_01",
  "password": "Qwerty123",
  "new_client_link": "5555f76e2-446f-412d-b999-6a72db60b31b",
  "new_client_id": "5555f76e2-446f-412d-b999-6a72db60b31b",
  "new_client_secret": "9rEXDECXnnZBAW9LGwITiMNulB9RQAtULS8CjC5BQrjQ2vmPOfrekhTeuU9Fbmt1",
  "new_redirect_uri": "https://bestuser.wdza.ru/",
  "code": "def502002b5...f4afc20ab6"
}
```
<br>

**Response, code 200:**<br>

```json
{
    "status": "Ссылка клиента успешно изменена",
    "client_link": "https://realuser1",
    "token": "eyJ0eXAiOi...sg0MgWF5xg",
    "refresh_token": "def5020051...1c34dc4e51",
    "ttl": 86400
}
```
<br>

<br>

**Response, code 400:**<br>
детали: код уже был успешно использован ранее для регистрации пользователя и был отозван системой amoCRM
```json
{
    "status": "Ошибка при получении данных токена. Проверьте данные.",
    "amoCRM_error_description": {
        "hint": "Authorization code has been revoked",
        "title": "Некорректный запрос",
        "type": "https://developers.amocrm.ru/v3/errors/OAuthProblemJson",
        "status": 400,
        "detail": "В запросе отсутствует ряд параметров или параметры невалидны"
    },
    "endpoint": "registration",
    "timestamp": "2022-12-12 15:55:30.123456"
}
```

<br>

**Response, code 400:**<br>
детали: ошибка в параметре *client_id*
```json
{
    "status": "Ошибка при получении данных токена. Проверьте данные.",
    "amoCRM_error_description": {
        "hint": "Check the `client_id` parameter",
        "title": "Некорректный запрос",
        "type": "https://developers.amocrm.ru/v3/errors/OAuthProblemJson",
        "status": 400,
        "detail": "В запросе отсутствует ряд параметров или параметры невалидны"
    },
    "endpoint": "registration",
    "timestamp": "2022-12-12 15:55:30.123456"
}
```

<br>

**Response, code 400:**<br>
детали: ошибка в параметре *client_secret*
```json
{
    "status": "Ошибка при получении данных токена. Проверьте данные.",
    "amoCRM_error_description": {
        "hint": "Check the `client_secret` parameter",
        "title": "Некорректный запрос",
        "type": "https://developers.amocrm.ru/v3/errors/OAuthProblemJson",
        "status": 400,
        "detail": "В запросе отсутствует ряд параметров или параметры невалидны"
    },
    "endpoint": "registration",
    "timestamp": "2022-12-12 15:55:30.123456"
}
```

<br>

**Response, code 400:**<br>
детали: ошибка в параметре *redirect_uri*
```json
{
    "status": "Ошибка при получении данных токена. Проверьте данные.",
    "amoCRM_error_description": {
        "hint": "Redirect URI is not associated with client",
        "title": "Некорректный запрос",
        "type": "https://developers.amocrm.ru/v3/errors/OAuthProblemJson",
        "status": 400,
        "detail": "В запросе отсутствует ряд параметров или параметры невалидны"
    },
    "endpoint": "registration",
    "timestamp": "2022-12-12 15:55:30.123456"
}
```

<br>

**Response, code 400:**<br>
детали: ошибка в параметре *client_link*
```json
{
    "status": "Ошибка при получении данных токена. Проверьте данные.",
    "amoCRM_error_description": {
        "hint": "Invalid account",
        "title": "Некорректный запрос",
        "type": "https://developers.amocrm.ru/v3/errors/OAuthProblemJson",
        "status": 400,
        "detail": "В запросе отсутствует ряд параметров или параметры невалидны"
    },
    "endpoint": "registration",
    "timestamp": "2022-12-12 15:55:30.123456"
}
```
<br>

**Response, code 401:**<br>

```json
{
    "status": "Не удалось изменить ссылку клиента. Проверьте логин и пароль.",
    "error_description": "неверный логин или пароль",
    "endpoint": "changeClientLink",
    "timestamp": "2022-12-12 15:55:30.123456"
}
```
<br>

**Response, code 422:**<br>

```json
{
    "status": "При валидации данных произошла ошибка. Проверьте логин и пароль на соответствие требованиям.",
    "error_description": "2 validation errors for Request\nbody -> login\n  ensure this value has at least 5 characters (type=value_error.any_str.min_length; limit_value=5)\nbody -> password\n  ensure this value has at least 5 characters (type=value_error.any_str.min_length; limit_value=5)",
    "endpoint": "exception_handler",
    "timestamp": "2022-12-12 15:55:30.123456"
}
```
<br>

**Response, code 500:**<br>

```json
{
  "status": "Ошибка сервера.",
  "endpoint": "changeClientLink",
  "timestamp": "2022-12-12 15:55:30.123456"
}
```
___




___
### Запуск программы

Запуск осуществляется из модуля ***main.py*** и ***auto_update_token_data.py***.<br>

Модуль ***main.py*** следует запускать в обычном режиме. API постоянно слушает запросы.
Модуль ***auto_update_token_data.py*** следует запускать с помощью планировщика задач Cron раз 10 часов.<br>


Блок кода, отвечающий за запуск программыи из модуля ***main.py*** для тестирования на локальной машине:
```python
# Запуск API (для тестирования на локальной машине)
HOST = "127.0.0.1"
PORT = 8000

if __name__ == "__main__":
    uvicorn.run("main:app", reload=True, host=HOST, port=PORT)
```
Запуск ***main.py*** на сервере подразумевается производить с помощью контейнера с настройками.

<br>Блок кода, отвечающий за запуск бота ***auto_update_token_data.py***:
```python
# Запуск бота
if __name__ == "__main__":
    logger.info(f"\n{'--Запуск цикла обновления token, refresh_token--'.center(170, '-')}\n")
    token_refresh_token_update()
    logger.info(f"\n{'--Завершение цикла обновления token, refresh_token--'.center(170, '-')}\n")

```
___

### Логирование
Для отслеживания работы программы включено логирование данных.
Логирование реализовано с помощью библиотеки [loguru](https://loguru.readthedocs.io/en/stable/index.html#)

Настройка системы логирования осуществляется в модуле ***logger_config.py*** и модуле ***functions.py.***<br><br>

Блок кода из модуля ***logger_config.py***, отвечающий за логироване:<br>
```python
"""
Параметры:
    format - формат для регистрации записи логов;
    level - установленный уровень логирования;
    rotation - отвечает за максимальный размер файла и ротацию после достижения заданного размера;
    retention - максимальное количество файлов логирования для сохранения, более старые файлы будут удаляться;
    compression - архивирование файлов после ротации.

    logger.add("logs/debag.log",
           format=LOG_FORMAT,
           level=LOG_LEVEL,
           rotation=LOG_ROTATION,
           retention=LOG_RETENTION,
           compression=LOG_COMPRESSION)
"""

logger_config = {"LOG_FORMAT": "{time} | {level} | {message}",
                 "LOG_LEVEL": "DEBUG",
                 "LOG_ROTATION": "100 MB",
                 "LOG_RETENTION": 5,
                 "LOG_COMPRESSION": "zip"
                 }
```


<br>Блок кода из модуля ***functions.py**, отвечающий за логироване:<br>
```python
"""
Настройки системы логирования:
Все лог-файлы находяться в директрории logs
Параметры:
    format - формат для регистрации записи логов
    level - установленный уровень логирования
    rotation - отвечает за максимальный размер файла и ротацию после достижения заданного размера
    retention - максимальное количество файлов логирования для сохранения, более старые файлы будут удаляться
    compression - архивирование файлов после ротации
"""
# Настройка системы логирования
logger.add("logs/debag.log",
           format=logger_config["LOG_FORMAT"],
           level=logger_config["LOG_LEVEL"],
           rotation=logger_config["LOG_ROTATION"],
           retention=logger_config["LOG_RETENTION"],
           compression=logger_config["LOG_COMPRESSION"]
           )
```
___

