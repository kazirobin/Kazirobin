# Docker Compose MongoDB and Mongo-express

This Docker Compose file sets up a MongoDB database and a Mongo Express web-based MongoDB admin interface.

To ensure that MongoDB and Mongo Express can communicate with each other, we will create a Docker network. This network will act as a private internal network for our containers.

```yaml
version: "3.8"

services:
  mongo:
    image: mongo:latest
    container_name: mongo
    restart: always
    ports:
      - "27017:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: root
      MONGO_INITDB_DATABASE: auth
    volumes:
      - mongo-data:/mongodb/data/db
    networks:
      - mongo-network

  mongo-express:
    image: mongo-express:latest
    container_name: mongo-express
    restart: always
    ports:
      - "8081:8081"
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: admin
      ME_CONFIG_MONGODB_ADMINPASSWORD: root
      ME_CONFIG_MONGODB_SERVER: mongo
      ME_CONFIG_BASICAUTH_USERNAME: admin
      ME_CONFIG_BASICAUTH_PASSWORD: root
    depends_on:
      - mongo
    networks:
      - mongo-network

volumes:
  mongo-data:
    driver: local

networks:
  mongo-network:
    driver: bridge
```