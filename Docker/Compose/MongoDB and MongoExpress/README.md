# MongoDB with Mongo Express using Docker Compose

This repository contains a `docker-compose.yaml` file to set up a **MongoDB database** along with **Mongo Express**, a web-based MongoDB admin interface.

## Features

- **MongoDB** (Database Service)
  - Runs a MongoDB container with persistent data storage.
  - Accessible via port `27017`.
  - Uses environment variables for authentication.
- **Mongo Express** (Web Admin Interface)
  - Runs a web-based MongoDB UI.
  - Accessible via port `8081`.
  - Connects to the MongoDB container automatically.

## Prerequisites

Ensure that you have:

- [Docker](https://www.docker.com/get-started) installed
- [Docker Compose](https://docs.docker.com/compose/install/) installed

## How to Run

1. Clone the repository (or save the `docker-compose.yaml` file).

   ```sh
   git clone <repository-url>
   cd <repository-folder>
   ```

2. Start the containers using Docker Compose:

   ```sh
   docker-compose up -d
   ```

   The `-d` flag runs the services in detached mode (in the background).

3. **Access MongoDB:**

   - Use a MongoDB client (e.g., Compass, Robo 3T) to connect to:
     ```
     mongodb://nk_admin:9130@localhost:27017/
     ```

4. **Access Mongo Express:**

   - Open your browser and go to: [http://localhost:8081](http://localhost:8081)

## Stopping and Removing Containers

To stop and remove all containers, use:

```sh
docker-compose down
```

This will remove the running containers but **preserve the database data** stored in the `mymongo-data` volume.

To remove all data permanently, run:

```sh
docker-compose down -v
```

## Docker-Compose Configuration

```yaml
version: "3"
services:
  mongodb:
    image: mongo
    restart: always
    ports:
      - "27017:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: nk_admin
      MONGO_INITDB_ROOT_PASSWORD: 9130
    volumes:
      - mymongo-data:/data/db
  mongo-express:
    image: mongo-express
    restart: always
    ports:
      - "8081:8081"
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: nk_admin
      ME_CONFIG_MONGODB_ADMINPASSWORD: 9130
      ME_CONFIG_MONGODB_SERVER: mongodb
volumes:
  mymongo-data:
    driver: local
```

## Notes

- **Persistent Storage**: The `mymongo-data` volume ensures data is not lost when restarting containers.
- **Authentication**: The MongoDB credentials are set via environment variables. Change them as needed.
- **Security**: This setup is for local development. Avoid using weak credentials in production.

## License

This project is open-source and available under the MIT License.

\~ Nikhil Kamble

