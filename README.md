# jira-nginx
Dockerized Jira product behind reverse proxy with nginx proxy manager

Docker image and atlassian-agent are based on [haxqer/jira](https://github.com/haxqer/jira) repository.
This is persistance installation of Jira with docker as we mapped current directory to store **jira_data** and **mysql_data** to docker container.
You can change them in real production environemt.

In this file replace all occurance of `jira.example.com` with your domain.

## Initialization

Inside `server.xml` file change `jira.example.com` to your FQDN.
You can get a free domain from `https://www.noip.com/`
After getting domain, resolve it to your public IP in noip.com panel.

For example `jira.sample.com -> 1.2.3.4`


## Run
```
docker compose up -d
```

## Configure nginx proxy manager
In Web Browse Open `your_ip:81` to access nginx proxy manager web UI.
login with below crendentioal
```
admin@example.com
changeme
```

In first loging chage your password to more secure one.
For any issue referes to original page
[nginxproxymanager](https://nginxproxymanager.com/setup/)

Create new Proxy Host config

Here is correct configs
```
Domain name: jira.example.com
Scheme: http
Forward Hostname / IP: jira-srv
Forward Port: 8080
```
Also in SSL tab
Request for new ssl certificate remember to set `jira.example.com` as domain


## Access
Open `127.0.0.1:8080` or `jira.example.com` to start jira installation.
MySQL configs
```
driver=mysql8.0
host=mysql-jira
port=3306
db=jira
user=root
passwd=123456
```

## Generate license
Replace your jira instance id with last argument `you-server-id-xxxx`

```
docker exec jira-srv java -jar /var/agent/atlassian-agent.jar \
    -d \
    -p jira \
    -m Hello@world.com \
    -n Hello@world.com \
    -o your-org \
    -s you-server-id-xxxx
```

