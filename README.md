# scotts-postgres

## Basic "How to" that includes all of the steps needed to create the employees table in your Docker container using PostgreSQL
Directed at an experienced database professional now using docker for the first time.


### Requirements

- Have docker installed.

- Have a user to run the docker commands (other than root)

- Have db client such as psql installed on local machine (For windows users DBeaver will probably work. I haven't tested yet. )

### Step One
Create a folder on your local machine. Call it postgres or scotts-postgress for example. The folder name represents the project name. 
Inside that folder create a file and call it Dockerfile. Next copy this text into the newly created Dockerfile.

```
FROM postgres:latest

ENV POSTGRES_USER scott
ENV POSTGRES_PASSWORD tiger
ENV POSTGRES_DB mydatabase

EXPOSE 5432


```
Stay in the same directory to run the following two commands using the command line. 

### Step two

To build the image and run the container use the following commands:

```
$ docker build -t scotts-postgres .
$ docker run -d -p 5432:5432 --name scotts-postgres-container scotts-postgres
```


The first command builds the image and tags it as scotts-postgres.

The second command runs the container and maps port 5432 on the host to port 5432 in the container. The container will be named scotts-postgres-container. The -d flag stands for "detached" mode and it runs the container in the background. This allows you to run other commands in the same shell while the container is still running. It's up to you.

### Step three
Connect to client on local machine. For linux users psql is fine.


```
$ psql -h localhost -U scott -d mydatabase
```

You'll be prompted for the password, which is tiger in this example.

## PostgreSQL 101

### Step four
In fact Scott, it's much like the Oracle that you are so familar with :)

```
$ psql -h localhost -U scott -d mydatabase
Password for user scott:
psql (13.4, server 15.1 (Debian 15.1-1.pgdg110+1))
WARNING: psql major version 13, server major version 15.
         Some psql features might not work.
Type "help" for help.
```
From inside psql create a table using SQL.
```
mydatabase=# CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    age INTEGER NOT NULL,
    address VARCHAR(255) NOT NULL
);
CREATE TABLE
```
Using \dt 
```

mydatabase=# \dt
         List of relations
 Schema |   Name    | Type  | Owner
--------+-----------+-------+-------
 public | employees | table | scott
(1 row)
```
### Using SQL Insert
```
mydatabase=# INSERT INTO employees (name, age, address) VALUES ('John Doe', 25, '123 Main St');
INSERT 0 1
mydatabase=# \dt
         List of relations
 Schema |   Name    | Type  | Owner
--------+-----------+-------+-------
 public | employees | table | scott
(1 row)
```
### Using SQL Select

```

mydatabase=# SELECT * FROM employees;
 id |   name   | age |   address
----+----------+-----+-------------
  1 | John Doe |  25 | 123 Main St
(1 row)

```


## Tips 

You can check if your container is running by using the docker ps command. This command will list all the running containers and you should see the scotts-postgres-container in the list.

```
docker ps
```

You can also stop or restart the container by using docker stop scotts-postgres-container and docker start scotts-postgres-container command respectively.

```
$ docker stop scotts-postgres-container
$ docker start scotts-postgres-container
```

You can also use docker logs to check the container logs.

```
docker logs scotts-postgres-container
```

Use docker exec -it scotts-postgres-container bash to open an interactive shell session inside the container

```
docker exec -it scotts-postgres-container bash
```

