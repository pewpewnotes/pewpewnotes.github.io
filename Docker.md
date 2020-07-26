1) docker images -> Lists docker images
2) docker run -itd --name kek alpine alpine:latest ash ( d is daemon mode )
3) docker exec -it alpine ash ( it -> interactive tty )
4) docker save ubuntu > ubuntu_save.tar -> saves the container (doesnt saves the insides and directory structor)
5) docker export ubuntu > ubuntu_export.tar -> saves container with directory structure
6) docker stop ubuntu 
7) docker rm ubuntu
8) docker rmi alpine:latest
9) docker load < ubuntu_save.tar
10) cat ubuntu_export.tar | docker import - alpine:latest 
docker run -itd --name ubuntu ubuntu:18.04 /bin/bash
docker exec -it ubuntu bash


