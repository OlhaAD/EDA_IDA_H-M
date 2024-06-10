# Персональные рекомендации H&M по моде

## Введение

Этот проект ориентирован на анализ и прогнозирование персонализированных рекомендаций для клиентов H&M. Анализ выполняется с использованием Python и включает в себя обширный исследовательский анализ данных (EDA) и анализ исходных данных (IDA).

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
