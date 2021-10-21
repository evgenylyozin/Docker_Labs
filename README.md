# Полезные команды

docker container rm --force $(docker container ls --all --quiet) -> Удалить все контейнеры в системе, находящиеся в любом состоянии

docker image rm --force $(docker image ls --all --quiet) -> Удалить все образы в системе

docker container stats [id] -> Получить информацию о том, сколько системных ресурсов использует контейнер

docker container logs [id] -> Получить логи приложения, запущенного в контейнере

docker container inspect [id] -> получить полные сведения о контейнере

docker container top [id] -> получить данные о запущенных процессах внутри контейнера

docker container run --detach --publish 8088:80 [image] -> Вариант запуска контейнера, который будет висеть в режиме ожидания запросов

docker image pull [image] -> Скачать конкретный образ

docker container run --env [VARIABLE=value] --env [VARIABLE=value] [image] -> Установить конкретное значение конкретной переменной окружения при создании контейнера

docker image build --tag [imageName] . -> построить образ из докер файла в текущей директории

docker image history [image] -> получить данные об истории создания образа

docker system df -> получить данные о физически занятой Докером памяти

docker container run -it [image] -> Запустить контейнер в интерактивном режиме (сразу внутри контейнера в командной строке)