# ml-foundry
A centralized repo containing resources for ml development env setup

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