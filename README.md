# Simple Notes App for TWS Community

This is a simple notes app built with **React** and **Django**. The app allows users to easily manage their notes. The deployment process is simplified using **Docker** and **Docker Compose**.

## Deployment Methods

You can deploy this app in two ways:


### Method 1: Manual Deployment on a Local or Remote Server using Docker Compose

---

This method allows you to deploy the app manually on a local or remote server using **Docker Compose**. You'll be able to manage your app with just a few simple commands.

#### Requirements:
1. **Remote server** (e.g., EC2 instance or any Linux-based server).
2. **Docker** and **Docker Compose** installed on the server -> [Install Docker](https://docs.sevenbridges.com/docs/install-docker-on-linux).

#### Steps:

1. **Clone the repository**:
   ```bash
   git clone https://github.com/anantvaid/django-notes-app.git
   cd django-notes-app
   ```
2. **Build and start the app using Docker Compose**: <br/>
   This command will build the Docker images and start the app in detached mode. It will also automatically configure Nginx (as specified in your docker-compose.yml and Dockerfile) to handle requests:
   ```bash
   docker compose up --build -d
   ```
3. **Check the app**: <br/>
   After the deployment, you can access the app via the public IP of your remote server (localhost if local machine) on port 80 (or another port if you configure it differently). For example:
   ```
   http://localhost
   http://<YOUR_SERVER_IP>
   ```
**Note**: Ensure the server's firewall allows incoming traffic on port 80 (or whichever port you're using).

### Method 2: Automated Deployment with GitHub Actions and Self-Hosted Runner
-----------------------------------------------------------------------------

This method automates the deployment using **GitHub Actions** and a **self-hosted runner** on your remote server. This allows you to deploy the app automatically whenever changes are pushed to the repository.

#### Requirements:

1.  **EC2 instance** (or any remote server).
2.  **Docker** and **Docker Compose** installed on the server.
3.  **GitHub repository** with a **self-hosted runner** configured.
4.  **GitHub Secrets** to store credentials such as Docker Hub credentials.

#### Steps:

1.  **Set up EC2 as a self-hosted runner**:

    -   Follow the official [GitHub documentation](https://docs.github.com/en/actions/hosting-your-own-runners/adding-self-hosted-runners) to set up a self-hosted runner on your EC2 instance (or any server).
2.  **Configure GitHub Actions workflow**:

    -   A pre-configured GitHub Actions workflow (`django-cicd.yaml`) is already set up in the repository. This will automatically build and push Docker images to Docker Hub and deploy the app to your self-hosted runner.
3.  **Add GitHub Secrets**:

    -   Add your **Docker Hub credentials** as GitHub Secrets (`DOCKER_USERNAME` and `DOCKER_PASSWORD`) to your repository.
4.  **Push changes**:

    -   Whenever you push changes to the `main` branch, the GitHub Actions workflow will automatically:
        -   Build and push the Docker image to Docker Hub.
        -   Deploy the app on your EC2 server using Docker Compose.
5.  **Verify the deployment**:

    -   After the workflow completes, the app will be accessible via the **public IP** of your EC2 instance or self-hosted runner.
  
Requirements
------------

To run this app, you need the following tools installed:

1.  **Docker** and **Docker Compose** (for both local and remote deployments).
2.  **Python 3.9** (for local development if you don't want to use Docker).
3.  **Node.js** (for the React frontend).

Nginx Configuration (Handled Automatically)
-------------------------------------------

The app is configured with **Nginx** as a reverse proxy within the Docker setup, so you don't need to worry about configuring it manually. The Docker Compose setup handles Nginx for you.

1.  **No need to manually edit `nginx.conf`** or any other configuration files.
2.  **Just run `docker compose up --build`**, and Nginx will automatically reverse proxy requests to the correct backend container.
