# Installer Docker sur Ubuntu

Pour installer docker sur ubuntu....<br>
On commence par installer des packages utiles :
```bash
 sudo apt-get update
 sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

Ensuite, on va ajouter les repos de docker au repos du système.
Pour ce faire, on commence par télécharger la clef publique :
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
Ensuite, on ajoute le repo :
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
Une fois que c'est fait, on update les repos et on installe docker :
 ```bash
 sudo apt-get update
 sudo apt-get install docker-ce docker-ce-cli containerd.io
```

Enfin, on va installer portainer pour visualiser nos packets :
 ```bash
docker volume create portainer_data
docker run -d -p 8000:8000 -p 9443:9443 --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    portainer/portainer-ce:latest
```


## Sources
Documentation Docker | https://docs.docker.com/engine/install/ubuntu/
Documentation Portainer | https://docs.portainer.io/v/ce-2.11/start/install/server/docker/linux
