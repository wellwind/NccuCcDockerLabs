## Ubuntu

1. sudo apt-get install apt-transport-https
2. sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9
3. sudo bash -c "echo deb https://get.docker.io/ubuntu docker main > /etc/apt/sources.list.d/docker.list"
4. sudo apt-get update
5. sudo apt-get install -y lxc-docker
6. curl -sSL https://get.docker.com/ | sudo sh
7. sudo service docker start
