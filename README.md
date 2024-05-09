<!-- markdownlint-disable MD030 -->

<img width="100%" src="https://github.com/FlowiseAI/Flowise/blob/main/images/flowise.png?raw=true"></a>

# Flowise - Build LLM Apps Easily

[![Release Notes](https://img.shields.io/github/release/FlowiseAI/Flowise)](https://github.com/FlowiseAI/Flowise/releases)

<h3>Drag & drop UI to build your customized LLM flow</h3>
<a href="https://github.com/FlowiseAI/Flowise">
<img width="100%" src="https://github.com/FlowiseAI/Flowise/blob/main/images/flowise.gif?raw=true"></a>

## ⚡Quick Start
Download and Install [NodeJS](https://nodejs.org/en/download) >= 18.15.0

1. Install Flowise
    ```bash
    npm install -g flowise
    ```
2. Start Flowise

    ```bash
    npx flowise start
    ```

    With username & password

    ```bash
    npx flowise start --FLOWISE_USERNAME=user --FLOWISE_PASSWORD=1234
    ```

3. Open [http://localhost:3000](http://localhost:3000)

## 🐳 Docker

### Docker Compose

1. Go to `docker` folder at the root of the project
2. Copy `.env.example` file, paste it into the same location, and rename to `.env`
3. `docker-compose up -d`
4. Open [http://localhost:3000](http://localhost:3000)
5. You can bring the containers down by `docker-compose stop`

### Docker Image

1. Build the image locally:
    ```bash
    docker build --no-cache -t flowise .
    ```
2. Run image:

    ```bash
    docker run -d --name flowise -p 3000:3000 flowise
    ```

3. Stop image:
    ```bash
    docker stop flowise
    ```

## 👨‍💻 Developers

Flowise has 3 different modules in a single mono repository.

-   `server`: Node backend to serve API logics
-   `ui`: React frontend
-   `components`: Third-party nodes integrations

### Prerequisite

-   Install [PNPM](https://pnpm.io/installation)
    ```bash
    npm i -g pnpm
    ```

### Setup

1. Clone the repository

    ```bash
    git clone https://github.com/FlowiseAI/Flowise.git
    ```

2. Go into repository folder

    ```bash
    cd Flowise
    ```

3. Install all dependencies of all modules:

    ```bash
    pnpm install
    ```

4. Build all the code:

    ```bash
    pnpm build
    ```

5. Start the app:

    ```bash
    pnpm start
    ```

    You can now access the app on [http://localhost:3000](http://localhost:3000)

6. For development build:

    - Create `.env` file and specify the `VITE_PORT` (refer to `.env.example`) in `packages/ui`
    - Create `.env` file and specify the `PORT` (refer to `.env.example`) in `packages/server`
    - Run

        ```bash
        pnpm dev
        ```

    Any code changes will reload the app automatically on [http://localhost:8080](http://localhost:8080)

## 🔒 Authentication

To enable app level authentication, add `FLOWISE_USERNAME` and `FLOWISE_PASSWORD` to the `.env` file in `packages/server`:

```
FLOWISE_USERNAME=user
FLOWISE_PASSWORD=1234
```

## 🌱 Env Variables

Flowise support different environment variables to configure your instance. You can specify the following variables in the `.env` file inside `packages/server` folder. Read [more](https://github.com/FlowiseAI/Flowise/blob/main/CONTRIBUTING.md#-env-variables)

## 📖 Documentation
[Flowise Docs](https://docs.flowiseai.com/)

## Self Host Instructions
[GCP](https://docs.flowiseai.com/deployment/gcp)
]
## Deployment
This project is a fork of Flowise. To release a new version:

1. Pull the latest code

2. Create a new docker image with the new version tag:
```bash
docker build -t gcr.io/flowise-415803/flowise:[VERSION]
```

3. Log into Google Cloud and authenticate with the container registry (requires permissions):
```bash
gcloud auth configure-docker
```

4. Push the image
```bash
docker push gcr.io/flowise-415803/[VERSION]
```

5. Update the deployment file in [yamls/deployments](./yamls/deployment.yaml)

6. Apply the configuration
```bash
kubectl apply -f deployment.yaml -n default
```

7. Monitor deployment status
```bash
kubectl rollout status deployment/flowise -n default
```

## Cloud Resources
This project has HTTPS enabled via Google's managed certifcate service. The configuration can be found in [yamls/certificate-service](./yamls/certificate-service/)

| Project reference      | Value                                                          |
|------------------------|--------------------------------------------------------------  |
| GCP Project Location   | `aiinkwell.com > Inkwell Organization > dev`                   |
| GCP Project ID         | `flowise-415803`                                           |
| GCP Project Link       | [Cloud Console Link](https://console.cloud.google.com/welcome?project=flowise-415803) |
| Service URL            | https://flowise.aiinkwell.dev |
