Basic "How to" that includes all of the steps needed to create the employess table in your Docker container using PostgreSQL

# scotts-postgres

Overview
=========

To build the image and run the container use the following commands:

$ docker build -t my-postgres .
$ docker run -d -p 5432:5432 --name my-postgres-container my-postgres


The first command builds the image and tags it as my-postgres.

The second command runs the container and maps port 5432 on the host to port 5432 in the container. The container will be named my-postgres-container. The -d flag stands for "detached" mode and it runs the container in the background. This allows you to run other commands in the same shell while the container is still running. It's up to you.

Connect to client on local machine. For linux users psql is fine.

$ psql -h localhost -U scott -d mydatabase

You'll be prompted for the password, which is tiger in this example.

