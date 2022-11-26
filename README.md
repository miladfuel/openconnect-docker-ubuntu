# OpenConnect-VPN-Server

1) Install Docker:
apt update

apt install apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update

apt-cache policy docker-ce

sudo apt install docker-ce

sudo systemctl status docker


-----------------------
Install openconnect container:

2-Build docker image:
docker build -t ocserv https://github.com/miladfuel/openconnect-docker-ubuntu.git

3-Run docker container:
docker run --name ocserv --privileged -p 8080:443 -p 8080:443/udp -d ocserv

--------------
4-Add user:
docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd testUserName

5-Change user password:
docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd testPassword

6-Delete user:
docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd -d testUserName

7-Lock user:
docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd -l testUserName

8-Unlock user:
docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd -u testUserName

9-Show all users and their hashed password:
docker exec -ti ocserv cat /etc/ocserv/ocpasswd
