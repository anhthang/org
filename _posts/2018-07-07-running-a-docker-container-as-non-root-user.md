---
layout: post
title: "Running a Docker container as non-root user"
description: "Running a Docker container as non-root user"
date: 2018-07-07
comments: false
categories: [docker]
permalink: 2018/07/07-running-a-docker-container-as-non-root-user
---

By default, Docker container will be run as root user, this can cause us pain. We could tell Docker to run as an ordinary user instead of `root`.

We could build a Dockerfile like this:

```dockerfile
FROM node:latest

# Add user so we dont run app as root
RUN groupadd -r node && useradd -r -g node node \
    && mkdir -p /home/node/<your-app-name> \
    && chown -R node:node /home/node

WORKDIR /home/node/<your-app-name>

COPY . .
RUN npm install

USER node
EXPOSE 3000

CMD ["npm", "start"]
```

Happy building ~v~