FROM debian:bullseye

COPY ./tools/config.sh ./config.sh

RUN apt update && apt upgrade -y && apt install mariadb-server -y

ENTRYPOINT [ "sh", "./config.sh" ]

CMD [ "mysqld --bind-address=0.0.0.0" ]
