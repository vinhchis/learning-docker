# Prepare
1. a docker image: `mcr.microsoft.colm/mssql/server:2022-latest` (id=142...)
2. a docker volume: `vmssql` 
    - data of volume save in folder `/var/lib/docker/volumes/vmssql/_data` on local
    - with 3 folder:  
        - `data` : .ldf, .ndf, .mdf
        - `log`
        - `secrets`
3. a port (not used) : `1433`

# Install
- `docker pull mcr.microsoft.com/mssql/server:2022-latest` : pull docker image
- `docker  volume create vmssql` : create a volume

## Make MSSQL Container
Information:
- name: `c-mssql`
- docker image: `mcr.microsoft.colm/mssql/server:2022-latest` . Use Image ID = 142 
- user: `SA`
- password: `Pw12345678`
- volume: `/var/opt/mssql` (container) | `vmsql` (local)
- port: `1433` (container + local)

```bash
docker run
    --name c-mssql
    -e 'ACCEPT_EULA=Y'
    -e 'SA_PASSWORD=Pw12345678'
    -p 1433:1433 
    -v vmssql:/var/opt/mssql
    142
```

docker run --name c-mssql  -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=Pw12345678' -p 1433:1433  -v vmssql:/var/opt/mssql 142

# SQLCMD
- Start container: `docker start c-mssql`
- access terminal `c-mssql`: `docker exec -it c-mssql bash`
- sqlcmd (`/opt/mssql-tools18/bin/sqlcmd`)
    - `sqlcmd -S host -U user -P password -C`
        - host: `localhost`
        - user: `SA`
        - password : `Pw12345678`
        - Trust : `-C`
    - => `/opt/mssql-tools18/bin/sqlcmd -U SA -P Pw12345678 -C`

# Connection string
- host: `localhost`
- name: (not use instances) => no name
- port: `1433`
- password: `Pw12345678`
- certificate : `TrustServerCertificate=true`
- database: `Demo`

=> "Server=.,1433;Database=Demo;User=sa;Password=Pw12345678;TrustServerCertificate=true"`

