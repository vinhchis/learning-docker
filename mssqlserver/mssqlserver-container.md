# Add Image
docker pull mcr.microsoft.com/mssql/server:2022-latest

# build
`docker run -e 'ACCEPT_EULA=Y' --name c-mssql -e 'MSSQL_SA_PASSWORD=Password789' -p 1433:1433 -v vmssql:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2022-latest`

`/opt/mssql-tools18/bin/sqlcmd -S localhost -U SA -P 'Password789' -C`
-C = trust the server's self-signed certificate without verifying it

# volume
/var/lib/docker/volumes/vmssql/_data
  - /data
  - /log
  - /secrets

# connection string
- host : localhost, ip
- name (instance)
- port : 8080 (default)
- password
- certificate : `TrustServerCertificate=true`
- database: 
SQL Server


`"Server=.,1433;Database=Demo;User=sa;Password=Password789;TrustServerCertificate=true"`

