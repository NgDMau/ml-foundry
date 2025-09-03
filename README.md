# ml-foundry
This repository contains essential resources for setting up and managing a robust machine learning development environment, with a focus on Docker and common tooling. This guide will help you with Docker setup, resource management, and troubleshooting common issues.

## Setting up Your Development Environment with Docker

This guide walks you through the process of building and running a Docker image for your project. This setup ensures that your development environment is consistent and isolated from your host system.

-----

### Step 1: Building the Docker Image

The first step is to build a Docker image from your project's `Dockerfile`. This command reads the instructions in your `Dockerfile` and creates a runnable image. Make sure you are in the directory containing your `Dockerfile` (e.g., `sample_docker_env`).

```bash
docker build . -t maund-env-image
```

  * `docker build`: The command to build a Docker image.
  * `.`: This tells Docker to use the current directory as the build context.
  * `-t maund-env-image`: This flag tags the image with a human-readable name, in this case, `maund-env-image`, making it easy to reference later.

-----

### Step 2: Running the Container

Once the image is built, you can run it as a container. If your project uses a `docker-compose.yml` file, this is the most efficient way to manage and run your services.

```bash
docker compose up -d
```

  * `docker compose up`: This command reads the `docker-compose.yml` file and starts the services defined within it.
  * `-d`: This flag runs the containers in **detached mode**, meaning they run in the background, freeing up your terminal.

This process ensures that your application runs in a consistent environment, from development to production.

## Docker Memory Management
Managing **memory and disk space** is crucial for maintaining a healthy and efficient Docker environment. Over time, unused images, containers, and volumes can consume significant resources. Here are some key commands to help you monitor and manage your Docker resources effectively.

### Monitoring Docker Resources

To get a quick overview of your Docker system's disk usage, including images, containers, and volumes, you can use the `docker system df` command. It provides a summary, showing how much space is used and how much can be reclaimed.

```bash
sudo docker system df
```

For more specific insights into your Docker volumes, you can check the memory consumed by each one. This command targets the Docker volumes directory, sorts the results by size, and helps identify which volumes are taking up the most space.

```bash
sudo du -h --max-depth=2 /var/lib/docker/volumes | grep '_data' | sort -hr
```

To inspect the content within a specific volume, you can list its contents. This is useful for understanding what is being stored and whether it's necessary. Remember to replace `<volume_name>` with the actual name of your volume.

```bash
sudo ls -lh /var/lib/docker/volumes/<volume_name>/_data
```

If you need to check the disk usage of the content inside a volume, you can use a similar command. This provides a detailed breakdown of the space used by files and directories within that specific volume.

```bash
sudo du -h --max-depth=1 /var/lib/docker/volumes/<volume_name>/_data | sort -hr
```

-----

### Reclaiming Space

The most common way to free up space is by removing unused images. The `docker image prune` command is a powerful tool for this. The `-a` flag removes all unused images, not just dangling ones, which can reclaim a substantial amount of disk space.

```bash
sudo docker image prune -a
```

To comprehensively clean up your entire Docker system, including unused containers, networks, and dangling images, you can use `docker system prune`. This is a more aggressive option and is highly effective for a full cleanup.

```bash
sudo docker system prune
```


## VS Code Cannot Connect to Remote Server via SSH
A common issue occurs when the root (`/`) directory on the remote server runs out of space. In this case, VS Code cannot install the VS Code Server, and the SSH connection from VS Code fails to initialize properly.

To resolve this, you can instruct VS Code to install the VS Code Server in a different directory that has more available space. By default, the VS Code Server is installed at `/home/<username>/.vscode-server`. The recommended solution is to move this directory to another location with sufficient space, and then create a symbolic link pointing back to the original location. This way, VS Code continues to function as expected, but the data is actually stored in the new directory.

### Steps:

1. **Move the `.vscode-server` directory to the new location:**
    ```bash
    mv ~/.vscode-server /mnt/data/yourusername/.vscode-server
    ```

2. **Create a symbolic link from the original location to the new directory:**
    ```bash
    ln -s /mnt/data/yourusername/.vscode-server ~/.vscode-server
    ```

3. **Restart your local VS Code and reconnect using Remote SSH.**

After completing these steps, VS Code should be able to connect via SSH and install the VS Code Server in the new location without issues.

