# Local Development & Testing Guide

This is a walkthrough on how to set up and run the application locally for development and testing. Alternatively if there are problems with server deployment, the application can be hosted locally on a local network as a last resort.

> **Important:** These local configuration changes are required to match the host machine's network configurations. Do **not** commit or push these infrastructure modifications to branches (`dev` or `main`) unless specifically needed.

## 1. Backend Setup (`docker-compose.yml`)

To test the backend services and database locally, you need to modify the `docker-compose.yml` file so that services expose the correct ports to your host machine and build from your local source code.

### Required Local Modifications
Open `docker-compose.yml` and apply the following changes:

1. **Database Binding:** Limit PostgreSQL exposure to your local loopback interface to avoid port collisions and external access.
2. **Local Build Context:** Switch the backend service from using the remote GitHub Container Registry image (`ghcr.io/...`) to a local build.
3. **Port Forwarding:** Change the public-facing port to standard HTTP `8080`.

#### Changes in Compose File:
```yaml
  postgres:
    # ... env variables ...
    ports:
      - "127.0.0.1:5432:5432" # Bind safely to localhost

  backend:
    build: .                  # Build from your local codebase
    # image: ghcr.io/...      # Comment out the remote registry image
    restart: unless-stopped
    # ... deploy ...
    ports:
      - "8080:8080"           # Map host port 8080 to container port 8080
```
#### Starting the Container
```
# IF for whatver reason, the flyway scripts were modified instead of creating a new one to overlay on top of the older ones. The checksum of the scripts will differ and the application will throw an error preventing deployment. Either revert the changes, or if that is no longer an option then clear the container volume. This should only be done if it the contents of the DB can be deleted safely with no reprecautions.
docker compose down -v

# Start the containers in the background
docker compose up -d --build

# View real-time logs for debugging
docker compose logs -f backend
```
## 2. Frontend Setup (`docker-compose.yml`)

### Step 1 - Find your IPv4 Address
Open CMD and run `ipconfig`, then note down your IPv4 address

### Step 2 - Update local.properties in the frontend
Update the line `SERVER_URL=Your IPv4 address:8080`. The file can be found in the root directory of the frontend project.
