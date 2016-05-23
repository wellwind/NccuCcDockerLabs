## 執行多個Apache container

1. mkdir ~/apache-inst && cd ~/apache-inst
2. vi Dockerfile

  ```dockerfile
  FROM httpd:2.4
  
  RUN ln -s "/usr/local/apache2/htdocs/" "/var/www"
  
  VOLUME ["/var/www"]
  ```
  
3. mkdir ~/www && vi ~/www/index.html
 
 ```html
  <h1>Hello Docker</h1>
  <p>This is a webpage in apache of Docker</p>
  ```

4. mkdir ~/www2 && vi ~/www2/index.html

  ```html
  <h1>Hello Docker 2!</h1>
  ```
  
5. sudo docker build -t apache-inst ~/apache-inst/
6. sudo docker run -itd -P -p 8080:80 -v ~/www:/var/www apache-inst
7. sudo docker run -itd -P -p 8088:80 -v ~/www2:/var/www apache-inst
8. curl http://127.0.0.1:8080
9. curl http://127.0.0.1:8088
