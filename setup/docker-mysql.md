docker pull mysql:latest

docker run --name c-mysql \
   -p 3306:3306 \
   -e MYSQL_ROOT_PASSWORD=Pw12345678 \
   -e MYSQL_DATABASE=enterprisedb \
   -e MYSQL_USER=vinhchis \
   -e MYSQL_PASSWORD=1234 \
   -v mysql-data:/var/lib/mysql \
   -d mysql:latest


   