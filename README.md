SSH 
```bash
sudo systemctl status ssh
```

IP
```bash
ip a
```

Config SSH Listen on an address
```bash
sudo nano /etc/ssh/sshd_config
```

Restart SSH
```bash
sudo systemctl restart ssh
```

Enable Firewall
```bash
sudo ufw enable
```

Allow SSH From Firewall
```bash
sudo ufw allow "OpenSSH"
```

Update && Upgrade
```bash
sudo apt update && sudo apt upgrade
```

See Timezone
```bash
timedatectl
```

Edit TimeSync
```bash
sudo nano /etc/systemd/timesyncd.conf
```

NTP
```bash
NTP=fw.eng.ku.ac.th time.uni.net.th
```

Restart TimeSync
```bash
sudo systemctl restart systemd-timesyncd.service
```

Edit Timezone
```bash
sudo dpkg-reconfigure tzdata
```

Create Group 
```bash
sudo groupadd -g 20000 webDeveloper && sudo groupadd -g 20001 dbDeveloper
```

Create User webAdmin
```bash
sudo useradd webAdmin
```

Setting Password webAdmin
```bash 
sudo passwd webAdmin
```

Create User dbAdmin
```bash
sudo useradd dbAdmin
```

Setting Password dbAdmin
```bash 
sudo passwd dbAdmin
```

Make Sure User was created
```bash
sudo cat /etc/passwd
```

Add User To Group
```bash
sudo usermod -aG webDeveloper webAdmin
```

Manage Permission webAdmin
```bash
sudo mkdir webAdmin
```

Manage Permission dbAdmin
```bash
sudo mkdir dbAdmin
```

Chown WebAdmin
```bash
sudo chown webAdmin:webDeveloper webAdmin/
```

Chown dbAdmin
```bash
sudo chown dbAdmin:dbDeveloper dbAdmin/
```

Permission webAdmin
```bash
sudo chmod 751 webAdmin/
```

Permission dbAdmin
```bash
sudo chmod 751 dbAdmin/
```

Docker Install
```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

```bash
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```

```bash
sudo apt-cache policy docker-ce
```

```bash
sudo apt install docker-ce
```

```bash
sudo usermod -aG docker ${USER}
```

```bash
sudo usermod -aG docker webadmin
```

```bash
sudo usermod -aG docker dbadmin
```

Portainer
```bash
docker volume create portainer_data
```

```bash
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

Nginx Reverse Proxy Manager
```yml
version: '3'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'
      - '81:81'
      - '443:443'
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
```

MongoDB
```yml
version: "3"
services:
  mongodb:
    image: mongo:4.4.6
    container_name: SPA_DBS
    ports:
	  - 27018:27017
    environment:
      - MONGO_INITDB_ROOT_USERNAME=dbAdmin
      - MONGO_INITDB_ROOT_PASSWORD=123456789
    restart: unless-stopped
```

Mongo Config
```txt
mongo -u dbAdmin -p --authenticationDatabase admin
```

Mongo Create User
```json
db.createUser(
 {
	user: "spaAdmin",
	pwd: passwordPrompt(),
	roles: [ { role: "readWrite", db: "ceboostup" }]
 }
)
```


Mongo Connect
```bash
mongo -u spaAdmin -p --authenticationDatabase ceboostup
```

Mongo Connect (Node Application)
```bash
mongodb://spaAdmin:123456789@192.7.10.82:27018/ceboostup?authSource=ceboostup
```

FRONTEND
```bash
git clone https://github.com/BarwSirati/FRONTEND_CEBOOSTUPX.git
```

BACKEND
```bash
git clone https://github.com/BarwSirati/BACKEND_CEBOOSTUPX.git
```

Grader
```bash
git clone https://github.com/BarwSirati/GRADER_CEBOOSTUPX.git
```
