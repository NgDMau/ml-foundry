# ml-foundry
A centralized repo containing resources for ml development env setup

## Setup & Development
1. First, build the image:
```bash
cd sample_docker_env
docker built . -t maund-env-image
```

2. To run the container from built image:
```bash
cd sample_docker_env
docker compose up -d
```

## Memory Management
Some popular commands to monitor and manage Docker memory usage:
Check Docker memory usage:
```bash
sudo docker system df
```

Remove unused images:
```bash
sudo docker image prune -a
```

Check memory used by each volume:
```bash
sudo du -h --max-depth=2 /var/lib/docker/volumes | grep '_data' | sort -hr
```

Check content inside a volume:
```bash
sudo ls -lh /var/lib/docker/volumes/<volume_name>/_data
```

Check disk usage of content inside a volume:
```bash
sudo du -h --max-depth=1 /var/lib/docker/volumes/<volume_name>/_data | sort -hr
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

