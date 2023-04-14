# Docker "Multi containers" Example

Docker example that shows how networks work.

## Prerequisites

Before you get started, you need to have the following tools installed:

- Docker

## Build the frontend and backend images

Navigate to the root directory of the cloned repository:

Build the backend image:

```bash
docker build -t backend ./backend/.
```

Build the backend image:

```bash
docker build -t frontend ./frontend/.
```

## Running the Containers

Create docker network:

```bash
docker network create multi-containers
```

Run mongo db container in the created network `multi-containers`:

```bash
docker run -d --name multi-containers-db -v multi-containers-db:/data/db --rm  --network multi-containers mongo
```

Run the backend container in the same network:

```bash
docker run -d -p 8089:80 --rm --network multi-containers --name backend backend
```

Run the frontend container (no need to specify the network because the front app run in browser, not in docker directly who resolve network):

```bash
# the front app needs a pseudo terminal `it` to keep running
docker run -d -p 8090:3000 --rm -it --name frontend frontend
```
