docker push - чтобы запихнуть все теги в локальный регистратор докер образов
http://registry.local:5000/v2/gallery/ui/tags/list - в браузере для получения списка всех тегов

curl --head --header "Accept: application/vnd.docker.distribution.manifest.v2+json" http://registry.local:5000/v2/gallery/ui/manifests/2 - запрос на получение digest строки манифеста

sha256:aa44e5a0c738ec89693879c8cd603154b8d422bc71c5b82c107714a9841072ac - сама строка

curl -X DELETE http://registry.local:5000/v2/gallery/ui/manifests/sha256:aa44e5a0c738ec89693879c8cd603154b8d422bc71c5b82c107714a9841072ac - удаляем все теги

