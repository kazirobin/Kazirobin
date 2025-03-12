# Write a Dockerfile

A Dockerfile is a text-based document that's used to create a container image. It provides instructions to the image builder on the commands to run, files to copy, startup command, and more.

As an example, the following Dockerfile would produce a ready-to-run Node.js application:

```docker
FROM node:alpine
WORKDIR /app

# Install the application dependencies
COPY package.json /app
RUN npm install

# Copy the application code
COPY . /app
EXPOSE 3000

# Start the application
CMD ["npm", "start"]
```

## Common instructions

Some of the most common instructions in a `Dockerfile` include:

- `FROM <image>` - this specifies the base image that the build will extend.
- `WORKDIR <path>` - this instruction specifies the "working directory" or the path in the image where files will be copied and commands will be executed.
- `COPY <host-path> <image-path>` - this instruction tells the builder to copy files from the host and put them into the container image.
- `RUN <command>` - this instruction tells the builder to run the specified command.
- `ENV <name> <value>` - this instruction sets an environment variable that a running container will use.
- `EXPOSE <port-number>` - this instruction sets configuration on the image that indicates a port the image would like to expose.
- `USER <user-or-uid>` - this instruction sets the default user for all subsequent instructions.
- `CMD ["<command>", "<arg1>"]` - this instruction sets the default command a container using this image will run.

To read through all of the instructions or go into greater detail, check out the [Dockerfile reference](https://docs.docker.com/engine/reference/builder/).

## Creating the Dockerfile

Now that you have the project, you’re ready to create the `Dockerfile`.

1. Create a file named `Dockerfile` in the same folder as the file `package.json`.
2. In the `Dockerfile`, define your base image by adding the following line:
    
    ```docker
    FROM node:20-alpine
    ```
    

1. Now, define the working directory by using the `WORKDIR` instruction. This will specify where future commands will run and the directory files will be copied inside the container image.
    
    ```docker
    WORKDIR /app
    ```
    

1. Copy all of the files from your project on your machine into the container image by using the `COPY` instruction:
    
    ```docker
    COPY . .
    ```
    

1. Install the app's dependencies by using the `yarn` CLI and package manager. To do so, run a command using the `RUN` instruction:
    
    ```docker
    RUN yarn install --production
    ```
    

1. Finally, specify the default command to run by using the `CMD` instruction:
    
    ```docker
    CMD ["node", "./src/index.js"]
    ```
    

And with that, you should have the following Dockerfile:

```docker
FROM node:20-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "./src/index.js"]
```

## Build, tag, and publish an image

In this guide, you will learn the following:

- Building images - the process of building an image based on a `Dockerfile`
- Tagging images - the process of giving an image a name, which also determines where the image can be distributed
- Publishing images - the process to distribute or share the newly created image using a container registry

## Building images

Most often, images are built using a Dockerfile. The most basic `docker build` command might look like the following:

```bash
docker build .
```

The final `.` in the command provides the path or URL to the build context. At this location, the builder will find the `Dockerfile` and other referenced files.

When you run a build, the builder pulls the base image, if needed, and then runs the instructions specified in the Dockerfile.

With the previous command, the image will have no name, but the output will provide the ID of the image. As an example, the previous command might produce the following output:

```bash
docker build .
[+] Building 103.0s (11/11) FINISHED                                                                                                        docker:desktop-linux
 => [internal] load build definition from Dockerfile                                                                                                        0.0s
 => => transferring dockerfile: 260B                                                                                                                        0.0s
 => [internal] load metadata for docker.io/library/node:alpine                                                                                              3.6s
 => [auth] library/node:pull token for registry-1.docker.io                                                                                                 0.0s
 => [internal] load .dockerignore                                                                                                                           0.0s
 => => transferring context: 2B                                                                0.0s
 => [1/5] FROM docker.io/library/node:alpine@sha256:1467ea23cce893347696b155b9e00e7f0ac7d21555eb6f27236f1328212e045e                                       86.8s
 => => resolve docker.io/library/node:alpine@sha256:1467ea23cce893347696b155b9e00e7f0ac7d21555eb6f27236f1328212e045e                                        0.0s
 => => sha256:15929fe50b42a226c1ffcbf061b9446ceefb6fc7ae3201e53aaaf6109b719d46 445B / 445B                                                                  0.6s
 => => sha256:453ca8c35a6710c3a236b7f3e68f3688ef04449b59a2b80ad92abc69b7c4c718 50.85MB / 50.85MB                                                           84.0s
 => => sha256:7a291b8a7b575b411b08e82b066a02d5d73db2377f324d619e07141f3169937c 1.39MB / 1.39MB                                                              4.1s
 => => extracting sha256:453ca8c35a6710c3a236b7f3e68f3688ef04449b59a2b80ad92abc69b7c4c718                                                                   2.5s
 => => extracting sha256:7a291b8a7b575b411b08e82b066a02d5d73db2377f324d619e07141f3169937c                                                                   0.1s
 => => extracting sha256:15929fe50b42a226c1ffcbf061b9446ceefb6fc7ae3201e53aaaf6109b719d46                                                                   0.0s
 => [internal] load build context                                                                                                                           1.5s
 => => transferring context: 2.26MB                                                                                                                         1.5s
 => [2/5] WORKDIR /app                                                                                                                                      0.3s
 => [3/5] COPY package.json /app                                                                                                                            0.1s
 => [4/5] RUN npm install                                                                                                                                   9.9s
 => [5/5] COPY . /app                                                                                                                                       0.4s
 => exporting to image                                                                                                                                      1.5s
 => => exporting layers                                                                                                                                     0.6s
 => => exporting manifest sha256:8a2cc08b454dde5c4330420041dd3c24c97d56ad0c7653707fa75f525ebe00c8                                                           0.0s
 => => exporting config sha256:bc325ca7646e8948d16267ea42896d1e0f8ea0aba24755db91c305b73963cd70                                                             0.0s
 => => exporting attestation manifest sha256:8022fbfd54a5b15e4ab20d6b821a805635be71157ef80746877062052f31e088                                               0.0s
 => => exporting manifest list sha256:766629f01e745b7a11e778524df73e2e071d2c42f00b89383c3de1f0c1ccd86d                                                      0.0s
 => => naming to moby-dangling@sha256:766629f01e745b7a11e778524df73e2e071d2c42f00b89383c3de1f0c1ccd86d                                                      0.0s
 => => unpacking to moby-dangling@sha256:766629f01e745b7a11e778524df73e2e071d2c42f00b89383c3de1f0c1ccd86d 
```

With the previous output, you could start a container by using the referenced image:

```bash
docker run sha256:766629f01e745b7a11e778524df73e2e071d2c42f00b89383c3de1f0c1ccd86d
```

That name certainly isn't memorable, which is where tagging becomes useful.

## Tagging images

Tagging images is the method to provide an image with a memorable name. However, there is a structure to the name of an image. A full image name has the following structure:

```bash
[HOST[:PORT_NUMBER]/]PATH[:TAG]
```

- `HOST`: The optional registry hostname where the image is located. If no host is specified, Docker's public registry at `docker.io` is used by default.
- `PORT_NUMBER`: The registry port number if a hostname is provided
- `PATH`: The path of the image, consisting of slash-separated components. For Docker Hub, the format follows `[NAMESPACE/]REPOSITORY`, where namespace is either a user's or organization's name. If no namespace is specified, `library` is used, which is the namespace for Docker Official Images.
- `TAG`: A custom, human-readable identifier that's typically used to identify different versions or variants of an image. If no tag is specified, `latest` is used by default.

Some examples of image names include:

- `nginx`, equivalent to `docker.io/library/nginx:latest`: this pulls an image from the `docker.io` registry, the `library` namespace, the `nginx` image repository, and the `latest` tag.
- `docker/welcome-to-docker`, equivalent to `docker.io/docker/welcome-to-docker:latest`: this pulls an image from the `docker.io` registry, the `docker` namespace, the `welcome-to-docker` image repository, and the `latest` tag
- `ghcr.io/dockersamples/example-voting-app-vote:pr-311`: this pulls an image from the GitHub Container Registry, the `dockersamples` namespace, the `example-voting-app-vote` image repository, and the `pr-311` tag

To tag an image during a build, add the `-t` or `--tag` flag:

```bash
docker build -t my-username/my-image .
```

If you've already built an image, you can add another tag to the image by using the `docker image tag` command:

```bash
docker image tag my-username/my-image another-username/another-image:v1
```

## Publishing images

Once you have an image built and tagged, you're ready to push it to a registry. To do so, use the `docker push` command:

```bash
docker push my-username/my-image
```

Within a few seconds, all of the layers for your image will be pushed to the registry.

Before you're able to push an image to a repository, you will need to be authenticated. To do so, simply use the `docker login` command.

## Exposing ports

Publishing a port provides the ability to break through a little bit of networking isolation by setting up a forwarding rule. As an example, you can indicate that requests on your host’s port `3000` should be forwarded to the container’s port `3000`. Publishing ports happens during container creation using the `-p` (or `--publish`) flag with `docker run`. The syntax is:

```bash
docker run -p HOST_PORT:CONTAINER_PORT image_name
```

- `HOST_PORT`: The port number on your host machine where you want to receive traffic
- `CONTAINER_PORT`: The port number within the container that's listening for connections

For example, to publish the container's port `3000` to host port `3000`:

```bash
docker run -p 3000:3000 nginx
```

Now, any traffic sent to port `3000` on your host machine will be forwarded to port `3000` within the container.

## Use docker compose

Create a new directory and inside that directory, create a `compose.yaml` file with the following contents

```docker
services:
  app:
    image: image_name
    ports:
      - 3000:8080
```

The `ports` configuration accepts a few different forms of syntax for the port definition. In this case, you’re using the same `HOST_PORT:CONTAINER_PORT` used in the `docker run` command.

1. Open a terminal and navigate to the directory you created in the previous step.
2. Use the `docker compose up` command to start the application.
3. Open your browser to http://localhost:3000.

## Docker detached mode

Detached mode, shown by the option `--detach` or `-d`, means that a Docker container runs in the background of your terminal. It does not receive input or display output.

```bash
docker run -d -p 3000:3000 nginx
```