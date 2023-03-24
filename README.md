# Assignment 3
## Part 3: Docker Volume

**Create a new Docker volume named "my_volume".**
```
docker volume create my_volume
```
**varify that the volume is created.**
```
docker volume ls
```
**Output** <br />
![Screenshot (44)](https://user-images.githubusercontent.com/65711565/227238306-1e0c87b8-0636-446d-9d95-ad7f838a9a54.png)
**Create a new Docker container using the "nginx" image**
```
docker pull nginx
docker run --name my_nginx --volume my_volume:/usr/share/nginx/html -p 80:80 -d nginx
```
**Verify that the "nginx" default page is accessible on your host machine at**
```
http://localhost:80
```
**or**
```
0.0.0.0:80
```
**Output** <br />
![Screenshot (45)](https://user-images.githubusercontent.com/65711565/227248848-0b06a7f5-c32d-4e06-afc0-0187fb79e14a.png)

**Create a new index.html**
```
touch index.html
```
**add some text to it.**
```
nano index.html
```
**Paste this in index.html**
```
<!DOCTYPE html>
<html>
<head>
    <title></title>
</head>
<body>
<h1>new html page</h1>
</body>
</html>
```
**First go in the superuser mode**
```
sudo su
```
**use this command to copy new index.html file to my_volume**
```
docker cp /home/osboxes/temp/index.html my_nginx:/usr/share/nginx/html
```
**Verify that the "index.html" file is accessible on your host machine at**
```
http://localhost:80
```
**or**
```
0.0.0.0:80
```
**Output**
![Screenshot (46)](https://user-images.githubusercontent.com/65711565/227255627-963afbd9-7862-4452-9796-8cd4be451236.png)
**Create a new docker container using httpd image and mounting it.**
```
 docker run -d -p 8081:80 --name my_httpd -v my_volume:/usr/local/apache2/htdocs httpd
```
**Verify that the "index.html" file is accessible on your host machine at**
```
http://localhost:8081
```
**or**
```
0.0.0.0:8081
```
**Output**<br />


**Create a new index.html**
```
touch about.html
```
**add some text to it.**
```
nano about.html
```
**Paste this in index.html**
```
<!DOCTYPE html>
<html>
<head>
    <title></title>
</head>
<body>
<h1>(httpd)2nd new html page</h1>
</body>
</html>
```
**First go in the superuser mode**
```
sudo su
```
**use this command to copy new index.html file to my_volume**
```
docker cp /home/osboxes/temp/about.html my_httpd2:/usr/local/apache2/htdocs
```
