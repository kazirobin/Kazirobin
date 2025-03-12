# Docker Compose PostgreSQL and pgadmin

This Docker Compose file sets up a PostgreSQL database and a pgadmin web-based postgresql admin interface.

```yaml
version: "3.8"

services:
  postgres:
    container_name: postgres
    image: postgres
    hostname: localhost
    ports:
      - "5432:5432"
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: root
      POSTGRES_DB: test
    volumes:
      - postgres-data:/postgresql/data/db
    restart: always

  pgadmin:
    container_name: pgadmin
    image: dpage/pgadmin4
    depends_on:
      - postgres
    ports:
      - "5050:80"
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@admin.com
      PGADMIN_DEFAULT_PASSWORD: root
    restart: always

volumes:
  postgres-data:
    driver: local
```