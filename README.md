# Nginx Deployment with Dokku

This project demonstrates a simple deployment of a static HTML site using an Nginx Docker container on [Dokku](https://dokku.com/).

## Prerequisites

- [Dokku](https://dokku.com/) installed on a server.
- [Git](https://git-scm.com/) installed locally.
- Access to the Dokku server (SSH).

## Deployment Steps

Follow these steps to deploy the application to your Dokku instance.

### 1. Initialize Git (If not already initialized)

```bash
git init
git add .
git commit -m "Initial commit"
```

### 2. Configure Dokku Remote

Replace `your-dokku-server.com` with your server's domain/IP and `nginx-app` with your desired application name.

```bash
git remote add dokku dokku@your-dokku-server.com:nginx-app
```

### 3. Create the App on Dokku

Connect to your server via SSH and create the app:

```bash
ssh root@your-dokku-server.com
dokku apps:create nginx-app
```

### 4. Deploy to Dokku

Push your code to the Dokku remote. Dokku will automatically detect the `Dockerfile` and build the image.

```bash
git push dokku main
```

### 5. Access the Application

Once the deployment finishes, Dokku will provide a URL for your application. You can also view it by running:

```bash
dokku urls nginx-app
```

## How it works

This project uses a standard `Dockerfile` to package the Nginx server. Dokku detects the `Dockerfile` and builds the image using the Docker engine, making it compatible with any Docker-based deployment workflow.
