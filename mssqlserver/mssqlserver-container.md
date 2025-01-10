# Configure Docker
- image: `mcr.microsoft.colm/mssql/server:2022-latest` (id=142...)
- docker volume: `vmssql` (/var/lib/docker/volumes/vmssql)
- folder `/var/lib/docker/volumes/vmssql/_data` container
    - `data` : .ldf, .ndf, .mdf
    - `log`
    - `secrets`
- port : 1433
# MSSQL Container
- user: `SA`
- password: `Password789`
- database: `/var/opt/mssql` (container)
- port: `1433`

> Make `c-mssql` container (auto start - first)
```bash
docker run
    --name c-mssql
    -e 'ACCEPT_EULA=Y'
    -e 'SA_PASSWORD=Password789'
    -p 1433:1433 
    -v vmssql:/var/opt/mssql
    142
```
Start container: `docker start c-mssql`
# SQLCMD
- access terminal `c-mssql`: `docker exec -it c-mssql bash`
- sqlcmd (/opt/mssql-tools18/bin/sqlcmd)
    - `sqlcmd -S host -U user -P password -C`
        - host: `localhost`
        - user: `SA`
        - password : `Password789`
        - Trust : `-C`
    - => `/opt/mssql-tools18/bin/sqlcmd -U SA -P Password789 -C`

# Connection string
- host: `localhost`
- name: 
- port: `1433`
- password: `Password789`
- certificate : `TrustServerCertificate=true`
- database: `Demo`

=> "Server=.,1433;Database=Demo;User=sa;Password=Password789;TrustServerCertificate=true"`

