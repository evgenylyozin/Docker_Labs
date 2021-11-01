# Полезные команды

docker container rm --force $(docker container ls --all --quiet) -> Удалить все контейнеры в системе, находящиеся в любом состоянии

docker image rm --force $(docker image ls --all --quiet) -> Удалить все образы в системе

docker volume rm --force $(docker volume ls --quiet) -> Удалить все тома докера в системе

docker volume prune -> удалить все тома докера, которые на данный момент не используются ни одним контейнером

docker network rm $(docker network ls --quiet) -> Удалить все сети, созданные докером

docker stack rm $(docker stack ls) -> Удалить все стаки

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

docker container run -it [image] -> Запустить контейнер в интерактивном режиме (сразу внутри контейнера в командной строке) - ИНОГДА МОЖЕТ ПОДКЛЮЧАТЬСЯ К STDOUT РАБОТАЮЩЕГО ПРИЛОЖЕНИЯ, НАПРИМЕР СЕРВЕРА!

docker exec -it [container] sh -> Получить доступ к консоли работающего контейнера

docker image tag [image] [newImageName]:[tag] -> Добавить новую ссылку (новое имя и тег) на существующий образ

docker info -> Показать полезную информацию о Докере в системе

docker container cp [pathToFileInContainer] [pathToFileWhereToCopyIt] -> Скопировать файлы из контейнера в хост машину или в другой контейнер, или наоборот

docker container exec [containerNameOrId] [actualCommandToExec] -> Выполнить любую скрипт команду внутри контейнера

docker volume create [volumeName] -> Создать том с конкретным наименованием

docker container run -v [volumeName]:[pathWhereToStoreTheValumeInAContainer] [image] -> Создать контейнер и подключить к нему конкретный том

docker container run --mount [type],source=[pathOnHostMachine],target=[targetPathInTheContainer] [image] -> Привязать директорию на хосте к директории внутри контейнера

docker network create [networkName] -> создать сеть с определенным наименованием

docker-compose logs --tail=1 [serviceName] -> получить последнюю лог запись из каждого работающего контейнера сервиса с соответствующим наименованием

docker-compose up --scale [serviceName]=[number] -> изменить число контейнеров соответствующего сервиса до определенного числа

docker-compose down - полностью убрать вызванное приложение со всеми контейнерами (их не будет в списке отсановленных контейнеров)
docker-compose stop - остановить приложение с возможностью вернуть его обратно в том же состоянии (например, с несколькими контейнерами на одном сервисе)

docker-compose ps -> получить список всех контейнеров, которые являются частью текущего приложения

docker-compose -f [pathToFirstComposeFile] -f [pathToSecondComposeFile] config -> Получить результат слияния нескольких файлов docker-compose.yml

docker-compose -f [pathToFirstComposeFile] -f [pathToSecondComposeFile] -f... -p [projectName] up -> Запустить процесс создания и запуска контейнеров на основе нескольких файлов docker compose (путём слияния файлов)

docker-compose -f [pathToFirstComposeFile] -f [pathToSecondComposeFile] -f... -p [projectName] down -> Остановить и удалить контейнеры, созданные на основе нескольких файлов docker compose (путём слияния файлов)


.. Docker Swarm ..

docker swarm init -> перейти в режим оркестратора контейнеров и сделать текущую машину менеджером

docker swarm join-token worker -> получить токен для подключения серверов-работников к кластеру текущего менеджера 

docker swarm join-token manager -> получить токен для подключения серверов-менеджеров к кластеру

docker node ls -> Получить список всех серверов (узлов), подключенных к кластеру

docker service create --name [name] --replicas [number] [image] -> Создать сервис, который будет работать внутри кластера

docker service ls -> получить список всех работающих сервисов в кластере

docker service ps [serviceName] -> получить список всех реплик конкретного сервиса

docker service logs -> получить логи сервисов

docker service inspect [serviceName] -> получить подробные сведения о конкретном сервисе в кластере

docker service update --[someParams] [serviceName] -> Обновить спецификацию сервиса (например, использовать новый образ)

docker service update --rollback [serviceName] -> откатить последнее обновление назад

docker network create --driver overlay [networkName] -> создать наложенную сеть (доступна всем узлам кластера)

docker stack deploy -c [pathToYml] [stackName] -> Запустить стак сервисов и других ресурсов из yml файла

docker stack ls -> показать все запущенные стаки

docker stack services [stackName] -> Показать все сервисы, которые запущены в конкретном стаке

docker config create [configObjectName] [pathToConfigFile] -> Создать объект конфигурации из файла конфигурации

docker config ls -> показать все объекты конфигураций в кластере

docker config inspect --pretty [configObjectName] -> показать содержание объекта конфигурации

docker secret create [nameOfTheSecret] [pathToTheSecret] -> создать секрет из файла с секретами

docker node update --label-add storage=raid $(docker node ls -q) -> пометить конкретный узел конкретной строкой, чтобы затем указать этот узел в deploy: placement: constraints: в compose файле

 docker node promote [node] -> Повысить ноду до уровня менеджера
 docker node demote [node] -> Понизить менеджера до уровня рабочего