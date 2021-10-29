docker network create --driver overlay num-net

docker service create --detach --name numbers-api --network num-net --publish 8081:80 --replicas 3 diamol/ch08-numbers-api:v3

docker service create --detach --name numbers-web --network num-net --publish 8082:80 --replicas 3 diamol/ch08-numbers-web:v3