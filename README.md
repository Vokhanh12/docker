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
/opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P "Aa@123456789"

```
