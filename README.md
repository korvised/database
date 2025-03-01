# Database for development
## Included mariadb, postgresql, mongodb, redis, rabbitmq

```shell
docker-compose up -d
```

```yaml
version: "3.9"
name: databases
services:
  mariadb:
    container_name: Mariadb
    image: mariadb:10.6.9
    restart: always
    environment:
      TZ: Asia/Bangkok
      MYSQL_ROOT_PASSWORD: root
      # MYSQL_DATABASE: DB_GATEWAY_APB
      MYSQL_USER: user
      MYSQL_PASSWORD: password
    volumes:
      - ./data/mariadb:/var/lib/mysql
    ports:
      - "3306:3306"
  postgres:
    container_name: Postgres
    image: postgres:14.1-alpine
    restart: always
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
      - POSTGRES_DB=postgres
    ports:
      - "5432:5432"
    volumes:
      - ./data/postgres/:/var/lib/postgresql/data/
  mongodb:
    container_name: MongoDB
    image: mongo:latest
    ports:
      - "27017:27017"
    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
      - MONGO_INITDB_ROOT_PASSWORD=password
    volumes:
      - ./data/mongodb:/data/db
    restart: always
  redis:
    container_name: Redis
    image: redis:6.2-alpine
    ports:
      - "6379:6379"
    #    command: redis-server --save 20 1 --loglevel warning --requirepass password
    volumes:
      - ./data/redis:/data
    restart: always
  rabbitmq:
    container_name: Rabbitmq
    image: rabbitmq:3.11.28-management
    hostname: my-rabbit
    ports:
      - "15672:15672"
      - "5672:5672"
    environment:
      RABBITMQ_DEFAULT_USER: guest
      RABBITMQ_DEFAULT_PASS: guest
    volumes:
      - ./data/rabbitmq:/var/lib/rabbitmq
    restart: always

```
