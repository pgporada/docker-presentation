# Start some arbitrary containers

docker run -d httpd
docker exec -it $CID

# docker forks the filesystem as we will see
# FROM INSIDE THE CONTAINER. COMMENTING OUT FOR YOUR OWN SAFETY!
# rm -rf /var /etc /bin

# Check out your web browser.

# Kill the now useless container
docker kill $CID

# Let's start another httpd container to prove a point
docker run -d httpd
docker exec -it $CID

# Trash this container as well
# FROM INSIDE THE CONTAINER. COMMENTING OUT FOR YOUR OWN SAFETY!
# rm -rf / --no-preserve-root
docker kill $CID


# Show disk usage of docker
df -h
docker rmi -f $(docker images | grep 'none>' | awk '{print $3}')
df -h

# Note that we still have containers named <none> if we `docker images -a`. This is because they are children of containers stored on our system.
