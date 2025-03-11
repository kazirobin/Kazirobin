# Docker Compose MySQL and phpmyadmin

This Docker Compose file sets up a mySQL database and a phpmyadmin web-based mysql admin interface.

```yaml
version: "3.8"

services:
  mysql:
    image: mysql:latest
    container_name: mysql
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: admin
      MYSQL_USER: admin
      MYSQL_PASSWORD: root
    ports:
      - "3306:3306"
    volumes:
      - mysql-data:/var/lib/mysql
    networks:
      - mysql-network

  phpmyadmin:
    image: phpmyadmin/phpmyadmin:latest
    container_name: phpmyadmin
    environment:
      PMA_HOST: mysql
      PMA_PORT: 3306
      PMA_USER: admin
      PMA_PASSWORD: root
    ports:
      - "8081:80"
    depends_on:
      - mysql
    networks:
      - mysql-network

volumes:
  mysql-data:
    driver: local

networks:
  mysql-network:
    driver: bridge
```