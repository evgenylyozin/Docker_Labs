Создать файл appsettings.json:
{
  "ConnectionStrings": {
    "ToDoDb": "Filename=/new-data/todo-list.db"
  }
}

Запустить контейнер со стандартного образа:
docker container run -d -p 8001:80 --name todo1 diamol/ch06-lab

Создать новый том:
docker volume create todoDB

Создать новый контейнер с новым томом:
docker container run -d -p 8002:80 -v todoDB:/new-data/ --name todo2 diamol/ch06-lab

Проверить, подключился том или нет: docker  exec -it  todo2 sh

Скопировать новые настройки в контейнер: docker container cp ./appsettings.json todo2:/app/appsettings.json

Запустить приложение и убедиться, что список задач пуст: localhost:8002

Создать несколько задач, удалить контейнер и создать его заново, чтобы убедиться, что данные сохраняются в томе:

docker container rm -f todo2
docker container run -d -p 8002:80 -v todoDB:/new-data/ --name todo2 diamol/ch06-lab
docker container cp ./appsettings.json todo2:/app/appsettings.json