# Job Search Analytics with PostgreSQL

![Python](https://img.shields.io/badge/python-3.9+-blue.svg)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-13+-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

Проект для сбора и анализа вакансий с сайта hh.ru с сохранением в PostgreSQL

## Содержание
1. [Описание проекта](#описание-проекта)
2. [Функциональность](#функциональность)
3. [Технологический стек](#технологический-стек)
4. [Установка и настройка](#установка-и-настройка)
5. [Структура проекта](#структура-проекта)
6. [Примеры использования](#примеры-использования)
7. [База данных](#база-данных)
8. [Лицензия](#лицензия)

## Описание проекта

Проект предназначен для:
- Сбора данных о компаниях и вакансиях с API hh.ru
- Сохранения данных в реляционную БД PostgreSQL
- Анализа рынка вакансий
- Поиска вакансий по различным критериям

## Функциональность

- Получение данных о 10+ компаниях с hh.ru
- Сохранение в PostgreSQL:
  - Информация о компаниях
  - Список вакансий с зарплатами
- Аналитические запросы:
  - Количество вакансий по компаниям
  - Средняя зарплата
  - Вакансии с зарплатой выше средней
  - Поиск по ключевым словам

## Технологический стек

### Основные технологии
- Python 3.9+
- PostgreSQL 13+
- psycopg2 (драйвер PostgreSQL для Python)

### Библиотеки Python
- `requests` - для работы с API hh.ru
- `python-dotenv` - управление переменными окружения
- `psycopg2-binary` - взаимодействие с PostgreSQL

## Установка и настройка

### Предварительные требования
1. Установленный Python 3.9+
2. Установленный PostgreSQL 13+
3. Созданная база данных в PostgreSQL

### Шаги установки

1. Клонировать репозиторий:

git clone https://github.com/yourusername/job-search-analytics.git
cd job-search-analytics

2. Создать и активировать виртуальное окружение:
python -m venv venv
source venv/bin/activate  # Linux/MacOS
venv\Scripts\activate    # Windows

3. Установить зависимости:
pip install -r requirements.txt

4. Создать файл .env в корне проекта:
DB_PASSWORD=your_password_here

5. Запустить приложение:
python main.py

### Структура проекта

job-search-analytics/
├── .env.example            # Пример файла конфигурации
├── .gitignore
├── README.md
├── requirements.txt        # Зависимости
├── main.py                 # Точка входа
│
├── config/                 # Конфигурация
│   └── config.py           # Настройки приложения
│
├── src/                    # Исходный код
│   ├── api/                # Работа с API
│   │   └── hh_api.py       # Модуль hh.ru API
│   │
│   ├── database/           # Работа с БД
│   │   ├── db_creator.py   # Создание БД
│   │   ├── db_manager.py   # Управление БД
│   │   └── db_queries.py   # SQL-запросы
│   │
│   └── models/             # Модели данных
│       └── models.py       # Классы Employer и Vacancy
│
└── tests/                  # Тесты
    ├── test_api.py
    └── test_db.py

### Примеры использования
1. Получение списка компаний и количества вакансий
from src.database.db_manager import DBManager

db_manager = DBManager('hh_vacancies')
companies = db_manager.get_companies_and_vacancies_count()

for company in companies:
    print(f"{company['name']}: {company['vacancies_count']} вакансий")

2. Поиск вакансий по ключевому слову
python_vacancies = db_manager.get_vacancies_with_keyword('python')
for vac in python_vacancies:
    print(f"{vac['company']}: {vac['title']} - {vac['url']}")

### База данных
Проект использует 2 основные таблицы:
Таблица employers
Поле	Тип	Описание
id	VARCHAR(20)	ID компании
name	VARCHAR(100)	Название компании
url	VARCHAR(100)	Ссылка на компанию
open_vacancies	INTEGER	Количество вакансий
Таблица vacancies
Поле	Тип	Описание
id	VARCHAR(20)	ID вакансии
employer_id	VARCHAR(20)	ID компании (FK)
title	VARCHAR(100)	Название вакансии
salary_from	NUMERIC(12,2)	Минимальная зарплата
salary_to	NUMERIC(12,2)	Максимальная зарплата
currency	VARCHAR(10)	Валюта зарплаты
url	VARCHAR(100)	Ссылка на вакансию

### Лицензия
MIT

### Как создать файл в PyCharm:
1. В проекте кликните правой кнопкой в области проекта
2. Выберите "New" → "File"
3. Введите имя файла `README.md`
4. Вставьте содержимое выше
5. Сохраните (Ctrl+S / Cmd+S)

Этот README содержит всю необходимую информацию для:
- Понимания проекта
- Настройки и запуска
- Работы с функционалом
- Развития проекта