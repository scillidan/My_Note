## [Docker](https://www.docker.com/)

<!-- --8<-- [start:arch-linux] -->
```sh
sudo pacman -S docker
sudo systemctl enable --now docker.service
```
<!-- --8<-- [end:arch-linux] -->

<!-- --8<-- [start:ubuntu-server-arm-24] -->
```sh
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
sudo apt-get update
sudo apt-get install ca-certificates wget
sudo install -m 0755 -d /etc/apt/keyrings
sudo wget -O /etc/apt/keyrings/docker.asc https://download.docker.com/linux/ubuntu/gpg
sudo chmod a+r /etc/apt/keyrings/docker.asc
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

↪ [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

```sh
sudo mkdir -p /etc/docker
sudo vim /etc/docker/daemon.json
```

```
{
  "registry-mirrors": [
    "https://docker.1panel.top",
    "https://docker.1panel.live",
    "https://proxy.1panel.live",
    "https://dockerproxy.1panel.live"
  ]
}
```

```sh
sudo mkdir -p /etc/containers/registries.conf.d
sudo vim /etc/containers/registries.conf.d/docker.conf
```

```
unqualified-search-registries = ["docker.io"]

[[registry]]
location = "docker.io"

[[registry.mirror]]
location = "docker.1panel.top"
```

```sh
sudo systemctl daemon-reload
sudo systemctl restart docker
```

↪ [Docker / Podman 安装与换源](https://wcbing.top/linux/containers/install/)

```sh
sudo docker run -p 8080:80 --rm nginx
sudo run -d -v /mnt/nvme:/mnt/nvme <docker_image>
sudo docker ps
sudo docker stop <container_id>
```

↪ [Docker Hub - Quickstart](https://docs.docker.com/docker-hub/quickstart/)

<!-- --8<-- [end:ubuntu-server-arm-24] -->

## [Podman](https://podman.io/)

```sh
sudo apt install podman podman-compose
cd <dir>
podman-compose --help
podman-compose up --help
podman-compose up -d
podman ps
podman-compose down
```

```sh
podman run -d --name <name>_server -p 63
```

↪ [Starting Containers with systemd](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux_atomic_host/7/html/managing_containers/running_containers_as_systemd_services_with_podman#starting_containers_with_systemd)

## [audiobookshelf](https://github.com/advplyr/audiobookshelf)

```sh
mkdir -p ~/Documents/docker-audiobookshelf
cd ~/Documents/docker-audiobookshelf
wget https://raw.githubusercontent.com/advplyr/audiobookshelf/refs/heads/master/docker-compose.yml
vim docker-compose.yml
```

```yaml
    image: docker.1panel.top/advplyr/audiobookshelf:latest
```

```sh
podman-compose up -d 
# podman-compose up -d -v /mnt/nvme:/mnt/nvme
sudo ufw allow 13378
```

## [LinguaCafe](https://github.com/simjanos-dev/LinguaCafe)

```sh
mkdir -p ~/Documents/docker-linguacafe
cd ~/Documents/docker-linguacafe
wget https://raw.githubusercontent.com/simjanos-dev/LinguaCafe/refs/heads/main/docker-compose.yml
docker compose up -d
podman-compose up -d
sudo ufw allow 9191
```

## [Lobe Chat](https://github.com/lobehub/lobe-chat) (TBD)

```sh
docker run -d -p 3210:3210 -e ACCESS_CODE=lobe66 --name lobe-chat lobehub/lobe-chat
docker ps
```

↪ [Lobe Chat - Docker Deployment Guide](https://lobehub.com/docs/self-hosting/platform/docker)  
↪ [[Bug] Ollama service is unavailable](https://github.com/lobehub/lobe-chat/issues/2337)  
↪ [Hitting a Wall Trying to get Ollama to work with LobeChat or any other app (works fine in CLI in the container)](https://www.reddit.com/r/unRAID/comments/1ccxqu6/hitting_a_wall_trying_to_get_ollama_to_work_with/)

## [Khoj](https://github.com/khoj-ai/khoj)

```sh
mkdir ~/.khoj
cd ~/.khoj
wget https://raw.githubusercontent.com/khoj-ai/khoj/master/docker-compose.yml
podman-compose up -d
podman ps
```

↪ [Khoj - Self-Host](https://docs.khoj.dev/get-started/setup/?server=docker&os=linux)

## [autoflow](https://github.com/pingcap/autoflow)

↪ [Deploy with Docker & Docker Compose](https://tidb.ai/docs/deploy-with-docker)

## [Verba](https://github.com/weaviate/Verba)

```sh
git clone --depth=1 https://github.com/weaviate/Verba
cd Verba
vim .env
```

```
OLLAMA_URL=http://<ollama_host>:11434
OLLAMA_MODEL=llama3.1
OLLAMA_EMBED_MODEL=mxbai-embed-large
```

```sh
sudo docker compose --env-file .env up -d --build
```

## [autoflow](https://github.com/pingcap/autoflow)

## [AutoRAG](https://github.com/Marker-Inc-Korea/AutoRAG) (Cache)

↪ [Run AutoRAG with 🐳 Docker](https://github.com/Marker-Inc-Korea/AutoRAG/blob/main/docs/source/install.md#1-build-the-docker-image)

## [Paperless-ngx](https://github.com/paperless-ngx/paperless-ngx)

↪ [Docker using the Installation Script](https://docs.paperless-ngx.com/setup/#docker_script)

## [Sabnzbd](https://github.com/linuxserver/docker-sabnzbd) (Cache)

## [Windows](https://github.com/dockur/windows) (Cache)

## [OSX](https://github.com/dockur/macos) (Cache)