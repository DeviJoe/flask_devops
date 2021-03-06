# ДЗ №1 - Составление Dockerfile

К вам пришел разработчик с просьбой создать ему Dockerfile для быстрого
разворачивания приложения у него на ПК для тестов. Ваша задача, помочь ему
это сделать.  Dockerfile - это файл с с 
инструкциями, как собрать образ. 

Описание приложения: 
* Прогрмма написана на языке Python, использовать версию 3.9
* Приложение написано на фреймворке Flask
* Все доп.зависимости находятся в файле requirements.txt
* Необходимо определить внутри переменные окружения 
  * _YOUR_NAME_ - Ваше имя (строка)
  * _DATA_FILE_PATH_ - Путь до файла, в котором хранится количество посещений сайта (строка)
* Необходимо поместить в контейнер файл visiters.txt, в котором лежит количество посетителей, путь до файла передается через переменную окружения
* При рестарте контейнера количество посещений *НЕ ДОЛЖНО СБРАСЫВАТЬСЯ*

КАК СОЗДАВАТЬ ДОКЕРФАЙЛ:
* Базовый образ - python 3.9
* Сначала создать рабочую директорию (Пусть будет `/app` )
* Скопировать файлы
* Установить зависимости из файла requirements.txt
* Обьявить переменные среды 
  * FLASK_APP - путь до исполняемого файла с приложением, в нашем случае [app.py](app.py)
  * FLASK_ENV - среда исполнения, поставить development
  * FLASK_DEBUG - при значении 0 отладка выключена, при 1 - включена. На продуктивных серверах ее обязательно нужно выключать
  * YOUR_NAME - ваше имя
  * DATA_FILE_PATH - путь в контейнере до файла с количеством посещений [visitors.txt](data/visiters.txt)
* Для запуска приложения выполнить команду `python3 app.py`

Для сборки образа использовать команду:
```shell
docker build -t 'flask-app:v1' .
```

Для запуска контейнера: 
```shell
docker run -p 8080:5000 --name flask_container -d --mount type=bind,source="$(pwd)"/data,target='/app/data' flask-app:v1
```
