# Build the docker container by itself
docker build -t myfirstcontainer .


# Remove the container
docker rm myfirstcontainer
docker rmi #whatever the heck the ID is for that thing

# Now try using a compose file
docker-compose up
ctrl-c

# Daemonize the process
docker-compose up -d

# Check the logs
docker-compose logs -f

# Stop the compose file
docker-compose stop
