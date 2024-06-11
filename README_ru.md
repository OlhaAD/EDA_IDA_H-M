# Первичный анализ данных и система рекомендаций для клиентов H&M

## Введение

Основное внимание в этом проекте уделяется первичному анализу данных и разработке системы персонализированных рекомендаций для клиентов H&M. Анализ выполняется с использованием Python и включает в себя обширный разведочный анализ данных (EDA) и начальный анализ данных (IDA).

## Как запустить проект
- Склонируйте репозиторий на свой локальный компьютер:
```sh
git clone https://github.com/your-username/your-repository.git
```
- Данные для анализа:
Данные слишком велики для хранения на GitHub. В проекте используются прямые ссылки на 3 файла с данными на мой Google Диск: ArticlesHM, CustomersHM и TransactionsHM.
- Откройте ноутбуки:
Откройте ноутбуки в папке /notebooks через Google Colab или Jupyter Notebook для просмотра и выполнения кода.
- Установите необходимые зависимости с помощью команды:
```sh
pip install -r requirements.txt
```
(Предполагается, что вы создали файл requirements.txt со списком всех необходимых библиотек).

**Пример кода для доступа к данным на Google Диске в Google Colab**
```python
from pydrive.auth import GoogleAuth
from pydrive.drive import GoogleDrive
from google.colab import auth
from oauth2client.client import GoogleCredentials
import pandas as pd

# Аутентификация и авторизация
auth.authenticate_user()
gauth = GoogleAuth()
gauth.credentials = GoogleCredentials.get_application_default()
drive = GoogleDrive(gauth)

# Загрузка файлов с Google Диска
file_ids = {
    'articles': '1H-g4oAbw1ZjYDOncx3xU3oro3tH3UIg6',
    'customers': '1KLM7Vum2O35MR17ULRLneM0uGVX61-VR',
    'transactions': '18ESMoz4VDe_ZCZzRPKKZS-UargXvrRdi'
}

for name, file_id in file_ids.items():
    downloaded = drive.CreateFile({'id': file_id})
    downloaded.GetContentFile(f'{name}.csv')
    print(f'{name}.csv downloaded')

# Чтение данных в DataFrame
df_articles = pd.read_csv('articles.csv')
df_customers = pd.read_csv('customers.csv')
df_transactions = pd.read_csv('transactions.csv')

# Отображение первых строк каждого DataFrame
print(df_articles.head())
print(df_customers.head())
print(df_transactions.head())
```
## Цели и задачи
### Цели
### Задачи
1. **Сбор и предобработка данных**
2.  **Визуализация данных**
3.  **Анализ данных**
## Подробная методология
### Инструменты и библиотеки

В данном проекте использовались следующие инструменты и библиотеки:
- **Python:** Основной язык программирования, используемый для анализа данных и построения моделей.

- **Pandas:** Библиотека для обработки и анализа данных. Использовалась для работы с датафреймами.

- **NumPy:** Библиотека для работы с массивами и выполнения численных вычислений.

- **Seaborn:** Библиотека для визуализации данных, основанная на matplotlib. Использовалась для создания статистических графиков.

- **Matplotlib:** Основная библиотека для создания графиков и визуализации данных.

### Сбор и предобработка данных
**Источник данных:**
  Данные для этого проекта взяты c https://www.kaggle.com/competitions/h-and-m-personalized-fashion-recommendations
  
**Структура базы данных:**
  База данных представлена в виде трех файлов: ArticlesHM, CustomersHM и TransactionsHM. 
  **ArticlesHM** - это таблица, которая содержит все артикулы H&M, а именно **105 542 строк**, включая следующие колонки:
  - **article_id:** id товара, тип данных - int64
  - **prod_name:** название товара, тип данных - object
  - **product_type_name:** название типа товара, тип данных - object
  - **product_group_name:** название группы товара, тип данных - object
  - **graphical_appearance_name:** название рисунка товара, тип данных - object
  - **colour_group_name:** название группы цвета, тип данных - object
  - **index_name:** название подраздела, тип данных - object
  - **index_group_name:** название раздела, тип данных - object
  - **section_name :** название секции, тип данных - object
  - **garment_group_name:** категория товара, тип данных - object
  - **detail_desc:** детали, тип данных - object

**CustomersHM** - это таблица, которая содержит информацию о клиентах H&M, а именно **1 371 979 строк**, включая следующие колонки:
  - **customer_id:** id клиента, тип данных - object
  - **Active:** , тип данных - float64
  - **club_member_status :** статус в клубе, тип данных - object
  - **fashion_news_frequency:** подписка на новости (частота), тип данных - object
  - **age:** возраст клиента, тип данных - float64
  - **postal_code:** почтовый индекс, тип данных - object

**TransactionsHM** - это таблица, которая содержит информацию о продажах H&M, а именно **31 788 323 строк**, включая следующие колонки:
  - **t_dat:** дата продажи, тип данных - object
  - **customer_id:** id клиента, тип данных - object
  - **article_id:** id товара, тип данных - int64
  - **price :** цена товара, тип данных - float64
  - **sales_channel_id:** канал продажи, тип данных - int64
