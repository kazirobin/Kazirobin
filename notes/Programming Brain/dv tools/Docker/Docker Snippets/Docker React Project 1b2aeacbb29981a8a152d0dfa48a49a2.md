# Docker React Project

This docker react project snippets include docker file, docker ignore, and compose file

Create a file name `/Dockerfile`

```docker
FROM node:20.18.0-alpine
WORKDIR /react-project

COPY package.json .
RUN npm install

COPY . .
EXPOSE 5173

CMD ["npm", "run", "dev"]
```

Create a file name `/.dockerignore`

```docker
node_modules
node_modules/*
npm-debug.log
logs/
.git
*.md
.cache
.vscode
.idea
.gitignore
```

Create a file name `/docker-compose.yaml`

```yaml
version: "3.8"

services:
  react-project:
    container_name: react-project-container
    image: react-project
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "5173:5173"
    volumes:
      - .:/react-project
      - /react-project/node_modules
    command: npm run dev
```