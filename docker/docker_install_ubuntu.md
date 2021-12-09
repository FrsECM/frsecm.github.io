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
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
```
Ensuite, on ajoute le repo :
```bash
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

```
Une fois que c'est fait, on update les repos et on installe docker :
 ```bash
 sudo apt-get update -y
sudo apt-get install -y docker-ce
sudo usermod -aG docker $USER
```

Ensuite, on va automatiser le lancement du service :
 ```bash
# automatiser le démarrage du démon docker
echo "sudo service docker status || sudo service docker start" >> ~/.bashrc
 
# désactiver la demande de mot de passe pour gérer le service docker
echo "%docker ALL=(ALL) NOPASSWD: /usr/sbin/service docker *" | sudo tee -a /etc/sudoers
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
| Documentation           | Link                                                                                 |
|-------------------------|--------------------------------------------------------------------------------------|
|Documentation Docker     | https://docs.docker.com/engine/install/ubuntu/                                       |
|Documentation Utile      | https://blog.lecacheur.com/2021/11/23/docker-sous-windows-wsl-2-sans-docker-desktop/ |
|Documentation Portainer  | https://docs.portainer.io/v/ce-2.11/start/install/server/docker/linux                |
