# Тестовое задание на _Python_-программиста

В этом репозитории реализовано API приложения для планирования пикников, состоящие из сущностей:
 - Город
 - Пикник
 - Пользователь
 - Регистрация пользователя на пикник

## Задание
 Тестовое задание подразумевает изменение представленного здесь кода для достижения следующих задач:

### Минимальный уровень
  1. Запустить проект и ознакомиться с его документацией на странице `http://127.0.0.1:8000/redoc/`
     или `http://127.0.0.1:8000/docs/` 
     и выполнить каждый из запросов
  2. Изменить код проекта для получения дополнительных возможностей:
     - Добавить поиск городов аргументом `q` в запросе `/get-cities/`
     - Добавить возможность фильтрации пользователей по возрасту(минимальный/максимальный) в запросе `users-list`
     - Поправить ошибку в запросе `picnic-add`
     - Добавить метод регистрации на пикник `picnic-register`
  3. Высказать идеи рефакторинга файла `external_requests.py`
  4. Описать возможные проблемы при масштабировании проекта


     
### Продвинутый уровень
  1. Привести к нормальному виду:
     - Методы обращения к эндпойнтам
     - Названия эндпойнтов
     - Архитектуру и пути обращения к эндпойнтам
  2. Расписать все входные/выходные поля в документации (`/redoc/` или `/docs/`), описав их классами
  3. Оптимизировать работу с базой данных в запросе `/all-picnics/`
  4. Сменить базу данных с SQLite на PostgreSQL
  5. Отрефакторить файл `external_requests.py`
  6. Написать тесты


### Дополнительные задания
  - Сделать логирование в файл, который не будет очищаться после перезапуска в докере
  - Описать правильную архитектуру для проекта


## Результат выполнения задания
Результат выполнения должен быть выложен в _общедоступном_ репозитории,
 история коммитов должна показывать выполненную работу
_Комментарии в коде тоже приветствуются_


## Решение
- Добавил поиск городов аргументом `q` в запросе `/get-cities/`
- Добавил возможность фильтрации пользователей по возрасту(минимальный/максимальный) в запросе `users-list`
- Поправил ошибку в запросе `picnic-add`
- Добавил метод регистрации на пикник `picnic-register`
Высказать идеи рефакторинга файла `external_requests.py`
- В представленном файле external_requests.py есть несколько возможных улучшений и рефакторингов:

1. Уменьшение дублирования кода: Код для выполнения запросов к API погоды дублируется в классах GetWeatherRequest и CheckCityExisting. Вы можете вынести общий функционал в отдельный класс или функции и использовать его в обоих классах. Это уменьшит дублирование и облегчит будущие изменения.

2. Использование параметров конфигурации: Вместо хранения API-ключа внутри класса, можно передавать его как параметр конструктора. Это сделает код более гибким и удобным для тестирования.

3. Использование исключений: Вместо просто возврата None в случае ошибки запроса, можно использовать исключения, такие как requests.exceptions.RequestException, чтобы более точно обрабатывать ошибки.

## Описать возможные проблемы при масштабировании проекта
- При масштабировании проекта, особенно в разработке программного обеспечения, могут возникнуть различные проблемы. Ниже перечислены некоторые из них:
- Сложность управления кодом: С ростом проекта количество кода и его сложность могут увеличиваться. Это может сделать управление и поддержку проекта более сложными задачами, особенно если нет хорошей организации кода.
- Сложности в разделении обязанностей: По мере роста проекта, разработчики могут столкнуться с трудностями в разделении обязанностей и определении, кто отвечает за какую часть кода.
- Производительность: С увеличением объема данных и запросов к базам данных производительность может стать проблемой. Неправильная архитектура базы данных или неэффективные запросы могут привести к ухудшению производительности.
- Масштабирование баз данных: При увеличении нагрузки на проект может потребоваться масштабирование базы данных. Это может быть сложной задачей, особенно если база данных не была изначально спроектирована с учетом горизонтального масштабирования.
- Управление зависимостями: С ростом проекта количество зависимостей может расти. Управление версиями зависимостей и обновлениями может стать сложной задачей.
- Тестирование и обеспечение качества: С ростом проекта увеличивается сложность тестирования. Необходимо разрабатывать и поддерживать надежные тесты, чтобы избежать регрессий и ошибок.
- Управление конфигурациями: Управление конфигурациями и средами разработки может стать сложным, особенно если не соблюдаются лучшие практики управления конфигурациями.
- Коммуникация и согласование: С ростом команды разработчиков и числа проектных участников становится сложнее обеспечивать хорошую коммуникацию и согласование работ.
- Безопасность: Рост проекта также увеличивает угрозы в области безопасности. Необходимо уделять больше внимания обеспечению безопасности и защите от атак.
- Поддержка и обслуживание: Чем больше проект, тем больше усилий требуется для его поддержки и обслуживания. Это включает в себя обновления, устранение ошибок и реагирование на отзывы пользователей.
### Высказать идеи рефакторинга файла `external_requests.py`
1. Именование методов обращения к эндпойнтам:
```python
# Было:
@app.get('/create-city/', summary='Create City', description='Создание города по его названию')
def create_city(city: str = Query(description="Название города", default=None)):

# Стало:
@app.post('/cities', summary='Create City', description='Создание нового города')
def create_city(city_name: str = Query(description="Название города", default=None)):

```
2. Изменение названий эндпойнтов:
```python
# Было:
@app.post('/get-cities/', summary='Get Cities')
def cities_list(q: str = Query(description="Название города", default=None)):

# Стало:
@app.get('/cities', summary='Get Cities', description='Получение списка городов')
def get_cities(city_name_query: str = Query(description="Название города", default=None)):
```
3. Уточнение архитектуры и путей обращения к эндпойнтам:
```python
# Было:
@app.post('/users-list/', summary='Список пользователей')
def users_list(min_age: int = Query(description="Минимальный возраст", default=None),
               max_age: int = Query(description="Максимальный возраст", default=None)):

# Стало:
@app.get('/users', summary='Get Users List', description='Получение списка пользователей')
def get_users_list(min_age_query: int = Query(description="Минимальный возраст", default=None),
                   max_age_query: int = Query(description="Максимальный возраст", default=None)):
```
### Расписать все входные/выходные поля в документации (`/redoc/` или `/docs/`), описав их классами
Путем уточнения названий и структуры путей, 
а также использования семантически более точных названий методов и параметров, 
можно сделать код более читаемым и понятным для других разработчиков, 
а также улучшить его обслуживаемость.

`/create-city/:`
```python
from pydantic import BaseModel

class CreateCityRequest(BaseModel):
    city: str

class CreateCityResponse(BaseModel):
    id: int
    name: str
    weather: str
   ```
`/get-cities/:`
```python
from pydantic import BaseModel

class GetCitiesRequest(BaseModel):
    q: str

class CityInfo(BaseModel):
    id: int
    name: str
    weather: str

class GetCitiesResponse(BaseModel):
    cities: List[CityInfo]
   ```
`/users-list/:`
```python
from pydantic import BaseModel

class UsersListRequest(BaseModel):
    min_age: int
    max_age: int

class UserInfo(BaseModel):
    id: int
    name: str
    surname: str
    age: int

class UsersListResponse(BaseModel):
    users: List[UserInfo]
   ```
`/register-user/:````
```python
from pydantic import BaseModel

class RegisterUserRequest(BaseModel):
    name: str
    surname: str
    age: int

class RegisterUserResponse(BaseModel):
    id: int
    name: str
    surname: str
    age: int
   ```
`/all-picnics/:`
```python
from pydantic import BaseModel

class AllPicnicsRequest(BaseModel):
    datetime: datetime
    past: bool

class PicnicUser(BaseModel):
    id: int
    name: str
    surname: str
    age: int

class PicnicInfo(BaseModel):
    id: int
    city: str
    time: datetime
    users: List[PicnicUser]

class AllPicnicsResponse(BaseModel):
    picnics: List[PicnicInfo]
   ````
`/picnic-add/:`
```python
from pydantic import BaseModel

class PicnicAddRequest(BaseModel):
    city_id: int
    datetime: datetime

class PicnicAddResponse(BaseModel):
    id: int
    city: str
    time: datetime
   ```
`/picnic-register/:`
```python
from pydantic import BaseModel

class PicnicRegisterRequest(BaseModel):
    picnic_id: int
    user_id: int

class PicnicRegisterResponse(BaseModel):
    registration_id: int
    user_name: str
    picnic_id: int
    picnic_time: datetime
```
## Оптимизировать работу с базой данных в запросе `/all-picnics/`
Для оптимизации работы с базой данных в запросе /all-picnics/, 
вы можете использовать подход, который называется "жадная загрузка" (eager loading) 
для избегания избыточных запросов к базе данных. Это особенно важно, 
когда вы должны получить связанные объекты из базы данных, такие как пользователи, 
участвующие в пикнике.

Жадная загрузка позволяет выполнить единственный запрос к базе данных, 
чтобы получить все необходимые данные. В вашем случае, это поможет избежать множества 
дополнительных запросов при обращении к связанным объектам.

Для этого вам потребуется использовать SQLALchemy и его функциональность жадной 
загрузки (eager loading). Вот как вы можете оптимизировать код в запросе /all-picnics/:

```python
from sqlalchemy.orm import joinedload

@app.get('/all-picnics/', summary='All Picnics', tags=['picnic'])
def all_picnics(datetime: dt.datetime = Query(default=None, description='Время пикника (по умолчанию не задано)'),
                past: bool = Query(default=True, description='Включая уже прошедшие пикники')):
    """
    Список всех пикников с оптимизацией жадной загрузки
    """
    # Оптимизированный запрос с жадной загрузкой пользователей и городов
    picnics = Session().query(Picnic) \
        .options(joinedload(Picnic.city), joinedload(Picnic.registrations).joinedload(PicnicRegistration.user))

    if datetime is not None:
        picnics = picnics.filter(Picnic.time == datetime)
    if not past:
        picnics = picnics.filter(Picnic.time >= dt.datetime.now())

    # Теперь при доступе к связанным объектам (например, city и user), SQLAlchemy не будет выполнять дополнительные запросы.
    return [{
        'id': pic.id,
        'city': pic.city.name,  # Данные о городе доступны через жадную загрузку
        'time': pic.time,
        'users': [
            {
                'id': registration.user.id,
                'name': registration.user.name,
                'surname': registration.user.surname,
                'age': registration.user.age,
            }
            for registration in pic.registrations],  # Данные о пользователях доступны через жадную загрузку
    } for pic in picnics]
```

## Сменить базу данных с SQLite на PostgreSQL

Для смены базы данных с SQLite на PostgreSQL в вашем FastAPI приложении, 
вам потребуется внести несколько изменений. Вот общий план того, 
как это можно сделать:

Установите библиотеку SQLAlchemy и драйвер для PostgreSQL:
Вы можете установить их с помощью pip:
```
pip install sqlalchemy psycopg2
```
Настройте параметры подключения к PostgreSQL:
Вам потребуется добавить информацию о подключении к вашей PostgreSQL базе данных. 
Эти параметры обычно хранятся в отдельном файле конфигурации. 
В FastAPI, вы можете использовать переменные окружения для хранения конфиденциальной 
информации, такой как имя пользователя, пароль и адрес сервера PostgreSQL.

Измените создание сессии SQLAlchemy:
Вместо использования SQLite, вы должны настроить сессию SQLAlchemy для работы с 
PostgreSQL. Это может быть сделано следующим образом:
```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker

DATABASE_URL = "postgresql://username:password@localhost/dbname"  # Замените параметры на свои

engine = create_engine(DATABASE_URL)
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
```
Здесь DATABASE_URL - это строка подключения к вашей PostgreSQL базе данных. 
Замените параметры на соответствующие для вашей базы данных.

Миграция данных из SQLite в PostgreSQL:
Если у вас уже есть данные в SQLite, вам придется перенести их в PostgreSQL. 
Вы можете использовать инструменты миграции данных, такие как Alembic, 
для выполнения этой задачи.

Измените модели и запросы:
Возможно, вам потребуется внести некоторые изменения в SQL-запросы и модели, 
чтобы они соответствовали синтаксису PostgreSQL. 
Например, PostgreSQL может использовать различный синтаксис для операций, 
таких как LIKE и регистрозависимых сравнений.

Повторно запустите приложение и тестируйте:
После всех изменений перезапустите ваше приложение и убедитесь, 
что оно успешно подключается к PostgreSQL и работает корректно.

Обратите внимание, что эти шаги являются общими указаниями, 
и реальные детали могут зависеть от вашей среды и конкретных потребностей. 
Не забудьте создать резервную копию ваших данных, прежде чем вносить изменения в 
базу данных.
