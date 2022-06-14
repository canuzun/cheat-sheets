[Docker Engine Installation](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)

````
#1
sudo apt-get update

#2
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
    
#3
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

#4
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
#5
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin

#6
sudo docker run hello-world
````
