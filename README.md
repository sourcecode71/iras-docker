# Docker Tutorial: Running a Node.js App on Windows with WSL
This tutorial will guide you through setting up a simple Docker container for a Node.js application, creating a Docker image, and pushing it to Docker Hub.

## Why Use Docker Hub?

Docker Hub is a cloud-based repository where you can store, share, and distribute Docker images. It allows you to:

- **Easily share images** with your team or make them available to the public.
- **Deploy applications** across various environments consistently.
- **Maintain version control** for your Docker images using tags.
- **Automate** image builds and integrate them with CI/CD pipelines.

With Docker Hub, you can access your images from anywhere, making it easy to set up and deploy containers on different systems without needing to manually recreate or configure them.

## Prerequisites

- **Docker Desktop** installed on Windows.
- A **Docker Hub account**. If you don’t have one, sign up at [hub.docker.com](https://hub.docker.com/).

## Setting Up WSL and Ubuntu

### Step 1: Open Command Prompt (as Administrator)

Press `Windows + X` and select **Command Prompt (Admin)** or **Windows Terminal (Admin)**.

### Step 2: Install WSL and Ubuntu

```bash
wsl --install -d Ubuntu
```

After installation, restart your system if prompted.

### Step 3: Launch Ubuntu and Update

```bash
sudo apt update
sudo apt upgrade -y
```

## Project Structure

```plaintext
iras-docker/
│
├── app.js
├── Dockerfile
└── README.md
```

### `app.js`

```javascript
let scope = 5;

while (scope > 0) {
    console.log(`Scope output: ${scope}`);
    scope--;
}
```

### `Dockerfile`

```dockerfile
# Use the official Node.js image with a lightweight version of Node.js
FROM node:alpine

# Set the working directory inside the container
WORKDIR /app

# Copy all files from the current directory to the container
COPY . /app

# Command to run the app
CMD ["node", "app.js"]
```

## Step-by-Step Guide to Docker

### 1. Build the Docker Image

Run the following command in the terminal (Windows Command Prompt, PowerShell, or Ubuntu WSL):

```bash
docker build -t iras-docker .
```

- `-t iras-docker`: Tags the image with the name `iras-docker`.
- `.`: Specifies that Docker should look for the `Dockerfile` in the current directory.

### 2. Log in to Docker Hub

Before pushing the image, log in to your Docker Hub account:

```bash
docker login
```

You will be prompted to enter your Docker Hub **username** and **password**.

### 3. Tag the Docker Image
```bash
docker tag iras-docker iras-docker/iras-docker:latest
```

- `iras-docker/iras-docker`: The format for images on Docker Hub is `username/repository_name`.
- `latest`: This is the image tag. You can use different tags like `v1`, `v2` to specify versions.

### 4. Push the Docker Image to Docker Hub

After tagging the image, push it to Docker Hub:

```bash
docker push iras-docker/iras-docker:latest
```

Replace `iras-docker` with your Docker Hub username.

### 5. Verify the Image on Docker Hub

- Go to [hub.docker.com](https://hub.docker.com/) and log in.
- Navigate to your repositories under your profile.
- You should see `iras-docker` listed with the `latest` tag.

### 6. Pull the Image from Docker Hub (Optional)

To test if the image is available on Docker Hub, you can pull it to any machine using:

```bash
docker pull iras-docker/iras-docker:latest
```

This will download the image from Docker Hub to your local machine.

### Example: Full Process

```bash
# Step 1: Build the Docker image
docker build -t iras-docker .

# Step 2: Log in to Docker Hub
docker login

# Step 3: Tag the Docker image
docker tag iras-docker iras-docker/iras-docker:latest

# Step 4: Push the image to Docker Hub
docker push iras-docker/iras-docker:latest
```

## Additional Resources

- [Docker Documentation](https://docs.docker.com/)
- [Node.js Documentation](https://nodejs.org/en/docs/)
- [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/)
- [WSL Documentation](https://docs.microsoft.com/en-us/windows/wsl/)

## Contributing

Feel free to submit issues or pull requests if you find any bugs or have suggestions for improvement.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
