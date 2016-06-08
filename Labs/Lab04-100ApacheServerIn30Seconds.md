## 30秒建立100個apache

### 調整TasksMax

1. sudo mkdir -p /etc/systemd/system/docker.service.d/
2. sudo vi /etc/systemd/system/docker.service.d/tasksmax.conf
  
  ```ini
  [Service]
  TasksMax=infinity
  ```

3. sudo systemctl daemon-reload
4. sudo systemctl restart docker

### 用shell script啟動大量Apache

1. vi make-100-servers.sh

  ```shell
  #!/bin/bash

  for index in $(seq 1 100)
  do
    declare -i port=${index}+100
    docker run -itd --name "server_${index}" -p ${port}:80 -v /var/www/website_${index}:/var/www apache-inst
  done
  ```
  
2. chmod 777 ./make-100-servers.sh
3. sudo ./make-100-servers.sh
4. sudo docker ps -a

### 快速移除所有的containers 

1. vi kill-containers.sh

  ``` shell 
  #!/bin/bash

  sudo docker stop $(sudo docker ps -aq)
  sudo docker rm $(sudo docker ps -aq)
  ```

2. sudo ./kill-containers.sh
