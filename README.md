# Docker Tutorial: Running a Node.js App on Windows with WSL

This tutorial will guide you through setting up Windows Subsystem for Linux (WSL), enabling virtualization, creating a simple Node.js app, writing a `Dockerfile`, and running your app inside a Docker container on Windows.

## Prerequisites

- **Docker Desktop** installed on Windows. If you haven't installed it yet, download and install from [Docker's official site](https://www.docker.com/products/docker-desktop).
- **Windows Subsystem for Linux (WSL)** set up on your system.
- **Git** installed on your system.

## Setting Up WSL and Ubuntu

### Step 1: Open Command Prompt (as Administrator)

Press `Windows + X` and select **Command Prompt (Admin)** or **Windows Terminal (Admin)**.

### Step 2: Check WSL Version

To check if WSL is already enabled, run the following command:

```bash
wsl --list --online
```

If WSL is not installed, proceed to the next step.

### Step 3: Install WSL and Ubuntu

To install WSL with Ubuntu, run the following command:

```bash
wsl --install -d Ubuntu
```

This command will:
- Enable the required Windows features for WSL and virtualization.
- Download and install the Ubuntu distribution.
- Set up Ubuntu as the default WSL environment.

After the installation, restart your computer if prompted.

### Step 4: Launch Ubuntu

Once your computer restarts, open the Ubuntu terminal by searching for **Ubuntu** in the Start menu.

### Step 5: Update and Upgrade Ubuntu

In the Ubuntu terminal, run the following commands to update your package list and upgrade packages:

```bash
sudo apt update
sudo apt upgrade -y
```

### Step 6: Install Docker in WSL (Optional)

If you prefer to run Docker directly within the WSL environment, you can follow [Docker's official guide for Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/). However, using Docker Desktop is recommended as it integrates seamlessly with WSL.

## Enabling Virtualization in Windows

Docker requires virtualization to be enabled on your Windows system. Here’s how to ensure it’s turned on:

1. **Enable Virtualization in BIOS:**
   - Restart your computer and enter the BIOS/UEFI settings (typically by pressing `F2`, `F10`, `Delete`, or `Esc` during startup).
   - Look for **Virtualization Technology** (Intel VT-x or AMD-V) and enable it.
   - Save and exit the BIOS settings.

2. **Enable Virtualization Features in Windows:**
   - Press `Windows + R`, type `optionalfeatures`, and press **Enter**.
   - In the **Windows Features** window, check:
     - **Virtual Machine Platform**
     - **Windows Subsystem for Linux**
   - Click **OK** and restart your computer if prompted.

## Project Structure

```plaintext
my-docker-app/
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

### 1. Clone the Repository

Clone this repository to your local machine:

```bash
git clone https://github.com/yourusername/my-docker-app.git
cd my-docker-app
```

Replace `yourusername` with your GitHub username.

### 2. Build the Docker Image

Run the following command in the terminal (Windows Command Prompt, PowerShell, or Ubuntu WSL):

```bash
docker build -t iras-docker .
```

- `-t iras-docker`: Tags the image with the name `iras-docker`.
- `.`: The `.` indicates that Docker should look for the `Dockerfile` in the current directory.

### 3. Run the Docker Container

Once the image is built, you can run a container from it:

```bash
docker run iras-docker
```

You should see the following output in your terminal:

```plaintext
Scope output: 5
Scope output: 4
Scope output: 3
Scope output: 2
Scope output: 1
```

### 4. Check Docker Images and Containers

- To list all Docker images:

  ```bash
  docker images
  ```

- To list all running containers:

  ```bash
  docker ps
  ```

- To list all containers (including stopped ones):

  ```bash
  docker ps -a
  ```

### 5. Stop and Remove the Docker Container

If you want to stop a running container, use the following command:

```bash
docker stop <container_id>
```

To remove the container:

```bash
docker rm <container_id>
```

Replace `<container_id>` with the actual ID of the container, which you can find using `docker ps -a`.

## Additional Resources

- [Docker Documentation](https://docs.docker.com/)
- [Node.js Documentation](https://nodejs.org/en/docs/)
- [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/)
- [WSL Documentation](https://docs.microsoft.com/en-us/windows/wsl/)

## Contributing

Feel free to submit issues or pull requests if you find any bugs or have suggestions for improvement.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

