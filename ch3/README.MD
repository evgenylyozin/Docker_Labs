docker container run -it diamol/ch03-lab
vim ch03.txt
добавляем всё что надо
exit
docker container commit -a Evgeny_Lyozin [containerId] [anyNewLocalRepoName]
docker container run -it [anyNewLocalRepoName]
проверяем результат