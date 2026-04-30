# Nginx Deployment with Dokku

This project demonstrates a simple deployment of a static HTML site using an Nginx Docker container on [Dokku](https://dokku.com/).

## Prerequisites

- [Dokku](https://dokku.com/) installed on a server.
- [Git](https://git-scm.com/) installed locally.
- Access to the Dokku server (SSH).

## Deployment Methods

You can deploy this application using two different methods:

### Method 1: Manual Git Push (Direct to Dokku)

Follow these steps to deploy the application manually from your local machine to your Dokku instance.

#### 1. Initialize Git (If not already initialized)

```bash
git init
git add .
git commit -m "Initial commit"
```

#### 2. Configure Dokku Remote

Replace `your-dokku-server.com` with your server's domain/IP and `nginx-app` with your desired application name.

```bash
git remote add dokku dokku@your-dokku-server.com:nginx-app
```

#### 3. Create the App on Dokku

Connect to your server via SSH and create the app:

```bash
ssh root@your-dokku-server.com
dokku apps:create nginx-app
```

#### 4. Deploy to Dokku

Push your code to the Dokku remote. Dokku will automatically detect the `Dockerfile` and build the image.

```bash
git push dokku main
```

#### 5. Access the Application

Once the deployment finishes, Dokku will provide a URL for your application. You can also view it by running:

```bash
dokku urls nginx-app
```

### Method 2: Automated Deployment via GitHub Actions

This project is pre-configured with a GitHub Actions workflow (`.github/workflows/deploy.yml`) that automatically deploys the `main` branch to Dokku whenever you push to GitHub.

#### Setup Instructions:

1. Go to your GitHub repository **Settings**.
2. Navigate to **Secrets and variables** > **Actions**.
3. Click **New repository secret** and add the following two secrets:
   - `DOKKU_HOST`: The domain or IP address of your Dokku server (e.g., `your-dokku-server.com`).
   - `SSH_PRIVATE_KEY`: An SSH private key that has deployment access to your Dokku server (the corresponding public key must be added to your Dokku server's `~/.ssh/authorized_keys` for the `dokku` user).
4. Update the `git_remote_url` inside `.github/workflows/deploy.yml` if your Dokku app name is not `myapp`.
5. Once configured, simply push your changes to the `main` branch:

```bash
git push origin main
```

GitHub Actions will take over and handle the deployment process automatically.

## How it works

This project uses a standard `Dockerfile` to package the Nginx server. Dokku detects the `Dockerfile` and builds the image using the Docker engine, making it compatible with any Docker-based deployment workflow.
