<h4>Реализованная функциональность</h4>
<ul>
    <li>Telegram бот;</li>
    <li>Сайт;</li>
</ul> 
<h4>Особенность проекта в следующем:</h4>
<ul>
 <li>Управление созданием заданий через телеграм бота;</li>
 <li>Отслеживание техники на карте в реальном времени;</li>
 <li>2 Варианта создания заданий и редактирования их;</li>
 <li>2 Варианта создания работников, техники и редактирования их;</li>
 </ul>
<h4>Основной стек технологий:</h4>
<ul>
	<li>HTML, CSS, JavaScript</li>
	<li>React (Next.js)</li>
	<li>Git</li>
	<li>Python, Django, DRF</li>
 </ul>
<h4>Демо</h4>
<p>Демо сервиса доступно по адресу: http://aero.webjox.ru/ </p>



СРЕДА ЗАПУСКА
------------
1) развертывание сервиса производится на debian-like linux (debian 9+);
2) требуется установленный web-сервер с поддержкой PHP(версия 7.4+) интерпретации (apache, nginx);
3) требуется установленная СУБД postgresql;
4) требуется установленный пакет name1 для работы с...;


УСТАНОВКА
------------
### Установка пакетов для запуска django сервера

Выполните 
~~~
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install postgresql postgresql-contrib
pip3 install psycopg2
pip3 install psycopg2-binary
pip3 install django
pip3 install djangorestframework
...
~~~

### Установка пакетов для запуска telegram бота

Выполните 
~~~
pip3 install pytelegrambotapi
Необходимо создать бота через @BotFather.
После создания бота в файл /Aero/manager/telegram bot/settings.py в поле token поместить токен бота.
...
~~~

### База данных

Необходимо создать пустую базу данных, а подключение к базе прописать в конфигурационный файл сервиса по адресу: папка_сервиса/...
~~~
Установим пароль для пользователя postgres
su - postgres
psql -c "ALTER USER postgres WITH PASSWORD 'новый_пароль';"

systemctl restart postgresql
sudo -u postgres psql

CREATE DATABASE air;
\q
exit или quit
~~~
### Выполнение миграций
В файле Aero/settings.py в поле DATABASES прописать название базы данных(в нашем случае мы создали air), пользователя(postgres), пароль который вы придумали, хост(localhost или '127.0.0.1'), порт(5432)
В файле /Aero/manager/telegram bot/db.py заполнить поля usr, passwd, host, db

Для заполнения базы данных системной информацией выполните в папке с файлом manage.py: 
~~~
python3 manage.py makemigration
python3 manage.py migrate
~~~
и согласитесь с запросом

### Заполнение данными

Для заполнения таблиц с пользователями, техникой и типами проблем можно перейти в панель администратора. 

Выполните данные действия
~~~
python3 manage.py createsuperuser
Введите данные
python3 manage.py runserver
Перейдите по ссылке http://127.0.0.1:8000/admin
Введите логин и пароль который вы придумали на первом шаге
~~~

После данных действий в интерфейсе появятся данные.
В телеграм боте при создании задачи будут списки возможных проблем, техники и рабочих которые могут приступить к работе. 
