## Create your own personal development directory
Create your own personal development directory at `/mnt/data/nict` (e.g /mnt/data/nict/tuannmd1)

## Duplicate `sample_docker_env`
Make a copy of `/home/nict/docker_envs/sample_docker_env` folder to your personal development directory created above, then change its name to your preferred environment name.

## Update `requirementx.txt`
Please update the `requirements.txt` according to your needs.

## Build your own container environment
Then run command below to build docker image, replace your-image-tag with any name you prefer:
```bash
docker build -t your-image-tag .
```

After the image is successfully built, use the following command to start an interactive container from it:
```bash
docker run -it --gpus all -v /path/to/your/project:/app your-image-tag bash 
```
or
```bash
docker run -d --name your-container-name --gpus all --shm-size=64g --restart unless-stopped -v /path/to/your/project:/app your-image-tag
```
The `-v` flag mounts a volume, which links your local project folder (the host path) to a folder inside the container.
- `/path/to/your/project`: The source directory on your machine.
- `/app`: The destination directory inside the container.
This means any files in your project folder are directly accessible at `/app` inside the container. This method is ideal for working with source code or large datasets, as it avoids the need to copy them into the image itself.


## Use the container
After starting container and getting accessed inside successfully, you can just do your normal development/experiment work without affecting system softwares/configurations.

## Temporarily exit container
If you want to detach (temporarily exit) your container and access next time without starting it again, the key sequence to do os `Ctrl + P`, followed by `Ctrl + Q`.
Press and hold `Ctrl`, press `P`, release `P`, press `Q`, and then release `Ctrl`. Your terminal will return to your local command prompt, but the container will continue running in the background.

## Re-attach (re-enter) the running container
To get back into your detached container, you'll use the `docker exec` command:
```bash
docker exec -it container-id-or-name /bin/bash
```
For example:
```bash
docker exec -it your-image-tag /bin/bash
```

## Permanently exit container
Just type 
```bash
exit
```
Or press shortcut `Ctrl + D`.
Or do command:
```bash
docker stop container-id-or-name
```

