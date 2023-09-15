# How to work with Postgres in Docker

> Take a look into `.env` and `compose.yaml` files for the details on each setting and each env variable

### Prerequisites

Docker is installed on your computer

### Run docker service locally, then run the compose

`docker compose up`

You shall see docker containers pulling 2 images: `pgadmin` and `postgres` respectively. `pgadmin` is not necessary, but just in case you prefer to work with databases in a visual manner

Then, that's how the successful start of the containers looks like:

```
[+] Running 3/3
 ✔ Network docker-pg_default  Created              0.0s
 ✔ Container postgres         Created              0.3s
 ✔ Container pgadmin          Created              0.3s
```

### Working with `pgadmin` within Docker

1. Open `localhost:5050` in your browser and login with the `pgadmin` credentials specified in the `.env` file
2. Register new server:
   - General. Name: any name you prefer
   - Connection. Host name/address: `host.docker.internal`
   - Connection. Port: port as specified in your `compose.yaml` - `services.postgres.ports`
   - Connection. Database: as specified in `.env` - `POSTGRES_DB`
   - Connection. Password: as specified in `.env` - `POSTGRES_PW`

Now you can find your server in the `pgadmin` Object Explorer

### Connect to database within Docker

In a terminal, type:
`docker exec -it <CONTAINER_NAME | CONTAINER_ID> psql -U <POSTGRES_USER> <POSTGRES_DB>`

- `CONTAINER_NAME` as specified in your `compose.yaml` file (`services.postgres.container_name`), or
- `CONTAINER_ID` is obtained using the command: `docker ps`

### To remove volumes (remove all DB data)

`docker-compose down --volumes`
