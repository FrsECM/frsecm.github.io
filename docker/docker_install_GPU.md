# Installation Docker GPU WSL



```bash
# Get Key/Repos Nvidia
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list

# Enable experimental features/Repos (For the moment none is stable)
sudo sed -i -e '/experimental/ s/^#//g' /etc/apt/sources.list.d/nvidia-docker.list


# Install Nvidia Layers for Docker
sudo apt-get update
sudo apt-get install -y nvidia-docker2  


# Run the GPU Benchmark
sudo service docker stop
sudo service docker start
```
