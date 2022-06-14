
- [Install Docker Engine](https://kubernetes.io/docs/setup/production-environment/container-runtimes/#docker)
- [Install cri-dockerd](https://github.com/Mirantis/cri-dockerd)
  - Install Go
  - Build cri-dockerd




 ````
###Install GO###
wget https://storage.googleapis.com/golang/getgo/installer_linux
chmod +x ./installer_linux
./installer_linux
source ~/.bash_profile

###Clone Repo###
git clone https://github.com/Mirantis/cri-dockerd.git
 
###Build cri-dockerd###
cd cri-dockerd
mkdir bin
go get && go build -o bin/cri-dockerd
mkdir -p /usr/local/bin
sudo install -o root -g root -m 0755 bin/cri-dockerd /usr/local/bin/cri-dockerd
sudo cp -a packaging/systemd/* /etc/systemd/system
sudo sed -i -e 's,/usr/bin/cri-dockerd,/usr/local/bin/cri-dockerd,' /etc/systemd/system/cri-docker.service
sudo systemctl daemon-reload
sudo systemctl enable cri-docker.service
sudo systemctl enable --now cri-docker.socket
 ````
