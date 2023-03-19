## Проект api_yamdb
REST API проект для сервиса YaMDb - сбор отзывов о фильмах, книгах или музыке.

## Описание
Проект YaMDb собирает отзывы пользователей на различные произведения.
Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.

Произведения делятся на категории, такие как «Книги», «Фильмы», «Музыка». Например, в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и «Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы «Жуки» и вторая сюита Баха. Список категорий может быть расширен (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»). 

Произведению может быть присвоен жанр из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»). 

Добавлять произведения, категории и жанры может только администратор.

Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (целое число). На одно произведение пользователь может оставить только один отзыв.

Пользователи могут оставлять комментарии к отзывам.

Добавлять отзывы, комментарии и ставить оценки могут только аутентифицированные пользователи.

## Как запустить проект
Все описанное ниже относится к ОС Linux.
Клонировать репозиторий и перейти командной строкой 
```
git clone git@github.com:madina-zvezda/infra_sp2.git
cd infra_sp2
cd api_yamdb
```
Создать и активировать виртуальное окружение
```
python3 -m venv venv

source venv/bin/activate
```
Установить зависимости из файла requirements.txt:
```
python3 -m pip install --upgrade pip

pip3 install -r requirements.txt
```
Перейти в папку с файлом docker-compose.yaml:
```
docker-compose up -d --build
```
Выполнить миграции: 
```
docker-compose exec web python manage.py migrate 
```
Создать суперпользователя
```
docker-compose exec web python manage.py createsuperuser
```

Собрать статику
```
docker-compose exec web python manage.py collectstatic --no-input
```
Создать дамп базы данных
```
docker-compose exec web python manage.py dumpdata > dumpPostgreSQL.json
```
Остановить контейнеры
```
docker-compose down -v
```

### Шаблон наполнения .env - путь infra/.env

```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
```

Документация API: http://localhost/redoc/
