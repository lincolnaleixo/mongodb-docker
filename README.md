
# MongoDB Docker Setup

This repository provides a simple setup to run MongoDB using Docker.

## Prerequisites

Make sure you have the following installed on your machine:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Getting Started

1. Clone the repository:

   ```bash
   git clone https://github.com/lincolnaleixo/mongodb-docker.git
   cd mongodb-docker
   ```

2. Rename the `.env.example` file to `.env` and configure the environment variables inside the `.env` file.

   ```bash
   mv .env.example .env
   ```

   Set the appropriate values for your MongoDB instance in the `.env` file:

   ```bash
   MONGODB_NAME=your_db_name
   MONGODB_USER=your_db_user
   MONGODB_PASSWORD=your_db_password
   MONGODB_PORT=your_db_port
   MONGODB_VOLUME_PATH=your_volume_path
   MONGODB_IMAGE_VERSION=your_mongodb_image_version
   ```

   The `MONGODB_PORT` is typically `27017` for default MongoDB installations, and the `MONGODB_IMAGE_VERSION` can be set to the desired MongoDB version (e.g., `5.0`).

3. Start the MongoDB container:

   ```bash
   docker-compose up -d
   ```

   This will start MongoDB on the specified port. You can access MongoDB locally using `localhost:27017` (or the port you configured in `.env`).

4. To stop the container:

   ```bash
   docker-compose down
   ```

## Data Persistence

Data persistence is achieved through folder mapping. The MongoDB data is stored on the machine by mapping a host folder to the container's data directory. This ensures data is not lost when the container is stopped or restarted.

You can modify the folder mapping in the `docker-compose.yml` file under the `volumes` section:

```yaml
volumes:
  - ${MONGODB_VOLUME_PATH}:/data/db
```

If you need to remove the data, simply delete the contents of the folder specified in the `MONGODB_VOLUME_PATH` variable on your host machine.

## Accessing MongoDB

To access the MongoDB instance, you can either:

1. Use the Mongo shell by entering the running container:

   ```bash
   docker exec -it <container_id> mongosh
   ```

2. Use a MongoDB client like [MongoDB Compass](https://www.mongodb.com/products/compass) or connect via your application using the connection string:

   ```
   mongodb://localhost:${MONGODB_PORT}
   ```

## Environment Variables

Make sure you have correctly set up the environment variables in the `.env` file:

- `MONGODB_NAME`: The name of your MongoDB container.
- `MONGODB_USER`: The root username for MongoDB.
- `MONGODB_PASSWORD`: The root password for MongoDB.
- `MONGODB_PORT`: The port for MongoDB (default is `27017`).
- `MONGODB_VOLUME_PATH`: The folder path on your local machine to store MongoDB data.
- `MONGODB_IMAGE_VERSION`: The MongoDB image version to use (e.g., `5.0`).

These variables must be correctly defined before running the MongoDB instance.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.