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