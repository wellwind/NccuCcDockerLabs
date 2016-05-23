## 建立自己的images

1. sudo docker pull ubuntu
2. sudo docker run -it ubuntu /bin/bash
3. touch ~/tempfile
3. exit
4. sudo docker ps -a (找出剛產生的contianer id)
5. sudo docker commit -m "Message" -a "Wellwind" [container-id] ubuntu
6. sudo docker run -it ubuntu /bin/bash
7. ls -la ~/
