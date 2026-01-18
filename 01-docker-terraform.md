# Homework 1: Docker, SQL and Terraform

Homework for Module 1: Containerization and Infrastructure as Code
[datatalks homework 1](https://courses.datatalks.club/de-zoomcamp-2026/homework/hw1)

## Question 1. Understanding docker first run 

> What's the version of pip in the python:3.13 image?

Run docker with the python:3.13 image in an interactive mode, use the entrypoint bash. $ python --version Python 3.13 <br>
```bash
docker run -it --entrypoint=bash python:3.13
```

To check the pip version in the docker image python:3.13 <br>
```bash 
pip --version
```

Answer: **pip 25.3**

## Question 2. Understanding Docker networking and docker-compose

> Given the docker-compose.yaml, what is the hostname and port that pgadmin should use to connect to the postgres database?

```bash
services:
  db:
    container_name: postgres
    image: postgres:17-alpine
    environment:
      POSTGRES_USER: 'postgres'
      POSTGRES_PASSWORD: 'postgres'
      POSTGRES_DB: 'ny_taxi'
    ports:
      - '5433:5432'
    volumes:
      - vol-pgdata:/var/lib/postgresql/data

  pgadmin:
    container_name: pgadmin
    image: dpage/pgadmin4:latest
    environment:
      PGADMIN_DEFAULT_EMAIL: "pgadmin@pgadmin.com"
      PGADMIN_DEFAULT_PASSWORD: "pgadmin"
    ports:
      - "8080:80"
    volumes:
      - vol-pgadmin_data:/var/lib/pgadmin

volumes:
  vol-pgdata:
    name: vol-pgdata
  vol-pgadmin_data:
    name: vol-pgadmin_data
```

Inside the same docker-compose network, containers talk to each other using the service name (or container name) and the internal port, not the published one.

The docker-compose.yaml Postgres service is:
<br>service name: db 
<br>container_name: postgres
<br>internal port: 5432


Answer: **db:5432** and **postgres:5432**