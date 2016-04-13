docker run -d httpd
docker exec -it $CID

rm -rf /var /etc /bin

Check out your web browser.

docker kill $CID

docker run -d nginx

docker exec -it $CID
rm -rf / --no-preserve-root
docker kill $CID


df -h
docker rmi -f $(docker images | grep 'none>' | awk '{print $3}')
df -h

Note that we still have containers named <none> if we `docker images -a`. This is because they are children of containers stored on our system.
