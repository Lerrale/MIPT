1. Для запуска nginx использовать:

- docker build -t nginx_44 .
- docker run --rm -it nginx_44


2. Для запуска posgresql использовать:

- docker build -t student44_postgres .
- docker run -p 5432:5432 -e POSTGRES_DB=test -e POSTGRES_USER=test -e POSTGRES_PASSWORD=testpassword student44_postgres