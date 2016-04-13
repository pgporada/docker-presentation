docker ps


# Pull several containers in 1 shot
for i in httpd nginx redis ; do docker pull $i ; docker images ; done


# Run containers and start them on various ports
docker run -d -p 9999:80 httpd
docker run -d -P nginx
docker run -d 6379:6379 redis
docker ps


# From your host, run these commands
# This should return an apache header
curl -ILk localhost:9999
curl -ILk localhost # whatever the nginx port is
# Redis should return "+PONG"
telnet localhost:6379
    ping



# We're going to kill the httpd box and check the docker processes
docker ps

# Start more nginx containers on arbritrary ports
docker run -d -P nginx
docker run -d -P nginx
docker ps
