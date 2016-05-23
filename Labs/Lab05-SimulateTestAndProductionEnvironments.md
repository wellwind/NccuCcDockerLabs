## 模擬正式/測試執行環境

1. mkdir ~/node-test && cd ~/node-test
2. touch database.txt Dockerfile
3. vi Dockerfile

  ```dockerfile
  FROM node:slim
  
  RUN mkdir -p /home/app/database
  
  COPY database.txt /home/app/database/database.txt
  
  VOLUME ["~/home/app/src"]
  
  ENTRYPOINT ["/bin/bash"]
  ```
  
4. vi database.txt

  ```
  test
  ```
  
5. mkdir ~/node-production && cp ~/node-test/* ~/node-production && cd ~/node-production
6. vi database.txt
  
  ```
  production
  ```
  
7. mkdir ~/app && vi ~/app/app.js
 
  ```javascript
  var fs = require("fs");
  
  fs.readFile("/home/app/database/database.txt", "utf8", (err, data) => {
    if (err) throw err;
    console.log(data);
  });
  ```
  
8. sudo docker build -t node-test ~/node-test
9. sudo docker build -t node-prod ~/node-production
10. sudo docker run -itd --name app-test -v ~/app:/home/app/src node-test
11. sudo docker run -itd --name app-prod -v ~/app:/home/app/src node-prod
12. sudo docker exec app-test node /home/app/src/app.js
13. sudo docker exec app-prod node /home/app/src/app.js
