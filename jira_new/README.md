# README

```
mkdir jira_data
sudo chmod 777 jira_data/
```

## Install docker 

On ubuntu 24.04

```
$ sudo apt install docker.io docker-compose-v2
$ sudo usermod -aG docker ${USER}
$ sudo apt install docker-buildx
```

Logout and login again

check
```
id -nG
docker run hello-world
```

## Run
```
docker compose -f compose.yml up -d 
docker compose -f nginx.yml up -d 
```
