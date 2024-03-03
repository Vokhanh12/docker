# docker

```bash
// run docker and create sql server
sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=Aa@123456789' -p 15432:1433 --name sqlserverlocaldev --hostname sqlserverlocaldev -v '/home/vokhanh/development/docker/sqlserver/data:/var/opt/mssql/data' -v '/home/vokhanh/development/docker/sqlserver/log:/var/opt/mssql/log' -v '/home/vokhanh/development/docker/sqlserver/secrets:/var/opt/mssql/secrets' -d mcr.microsoft.com/mssql/server:2022-latest

// remove docker
sudo docker rm sqlserverlocaldev

// check list docker
sudo docker ps -a

//Connect to run command line sqlserver
sudo docker exec -it sqlserverlocaldev<name_sql_server> "bash"

// Login database
/opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P <password>"Aa@123456789"

```


```bash
Copy the SQL file into the Docker container:
docker cp ~/file your_sql_server_container:/path/in/container

un the SQL script inside the Docker container:
docker exec -it your_sql_server_container /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P YourPassword -d YourDatabase -i /path/in/container/qlsv.sql


docker exec -it sqlserverlocaldev id
sudo docker exec -u 10001<id> -it sqlserverlocaldev mkdir -p /tmp/fileSql<create file>

run script create database => master
sudo docker exec -it sqlserverlocaldev /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P 'Aa@123456789' -d master -i /tmp/fileSql/QLSinhVien.sql

```



<h4>Create Dockerfile to build image</h4>
```bash
Use straight command on docker bash
docker exec -u o -it [name_container] [command_bash]

create image
docker commit [docker_id] [new_name]

Run new container from new image with new mapping port
example
docker run -p 0.0.0.0:NEW_PORT:5432/tcp --name my-postgres-container-updated -e POSTGRES_PASSWORD=mysecretpassword -d my-postgres-image

```bash
# Sử dụng một image golang đã có sẵn
FROM golang:latest

# Sao chép mã nguồn vào container
COPY . /app

# Thiết lập thư mục làm việc
WORKDIR /app

# Build ứng dụng Golang
RUN go build -o server .

# Thiết lập biến môi trường cho kết nối PostgreSQL
ENV PGHOST=rssagg
ENV PGPORT=5432
ENV PGDATABASE=mydatabase
ENV PGUSER=myuser
ENV PGPASSWORD=Aa@123456789

# Chạy ứng dụng khi container được khởi chạy
CMD ["./server"]
```

```bash
// build docker image in folder app
docker build -t name-image:tag .
```

<h4>Create and Run container</h4>

```bash
docker run --name name-container -d ten-image:tag
```

<h4>check log run container</h4>

```bash
docker logs name-container
```

<h4>show ip of docker</h4>


```bash
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' name-container
```








```

