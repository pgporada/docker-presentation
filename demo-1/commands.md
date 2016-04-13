docker ps



for i in httpd nginx redis ; do docker pull $i ; docker images ; done



docker run -d -p 9999:80 httpd
docker run -d -P nginx
docker run -d 6379:6379 redis



curl -ILk localhost:9999



curl -ILk localhost # whatever the nginx port is



telnet localhost:6379
    ping



We're going to kill the httpd box
docker ps


docker run -d -P nginx
docker run -d -P nginx
docker ps
