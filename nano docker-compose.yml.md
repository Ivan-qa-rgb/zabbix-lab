version: '3.8'

services:
  zabbix-db:
    image: mysql:8.0
    container_name: zabbix-mysql
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
      MYSQL_DATABASE: zabbix
      MYSQL_USER: zabbix
      MYSQL_PASSWORD: zabbixpass
    volumes:
      - zabbix-db-data:/var/lib/mysql
    command: --character-set-server=utf8mb4 --collation-server=utf8mb4_bin

  zabbix-server:
    image: zabbix/zabbix-server-mysql:alpine-7.0-latest
    container_name: zabbix-server
    environment:
      DB_SERVER_HOST: zabbix-db
      MYSQL_DATABASE: zabbix
      MYSQL_USER: zabbix
      MYSQL_PASSWORD: zabbixpass
      MYSQL_ROOT_PASSWORD: rootpass
    ports:
      - "10051:10051"
    depends_on:
      - zabbix-db

  zabbix-web:
    image: zabbix/zabbix-web-nginx-mysql:alpine-7.0-latest
    container_name: zabbix-web
    environment:
      ZBX_SERVER_HOST: zabbix-server
      DB_SERVER_HOST: zabbix-db
      MYSQL_DATABASE: zabbix
      MYSQL_USER: zabbix
      MYSQL_PASSWORD: zabbixpass
      PHP_TZ: Europe/Moscow
    ports:
      - "8080:8080"
    depends_on:
      - zabbix-server
      - zabbix-db

  zabbix-agent:
    image: zabbix/zabbix-agent:alpine-7.0-latest
    container_name: zabbix-agent
    environment:
      ZBX_HOSTNAME: "zabbix-server"
      ZBX_SERVER_HOST: "zabbix-server"
    depends_on:
      - zabbix-server

volumes:
  zabbix-db-data:
