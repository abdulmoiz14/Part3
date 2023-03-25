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
docker run --name my_nginx --volume my_volume:/usr/share/nginx/html -p 8080:80 -d nginx
```
**Verify that the "nginx" default page is accessible on your host machine at**
```
http://localhost:8080
```
**Output** <br />

![Screenshot (63)](https://user-images.githubusercontent.com/65711565/227740106-a9cf7764-b515-498e-a526-bc8c43fc11cf.png)

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
http://localhost:8080
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
**Output**<br />
![Screenshot (64)](https://user-images.githubusercontent.com/65711565/227740137-ad16443e-d878-4370-be9f-494c153a35f9.png)

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
**Verify that the "index.html" file is accessible on your host machine at**
```
http://localhost:8081
```
**Output**<br />

**Stop and remove the container.**
```
docker stop my_nginx
docker stop my_httpd2
docker rm my_nginx
docker rm my_httpd2
```
**Verify that the "index.html" and "about.html" files are still available in the "my_volume" volume.**
```
cd /
sudo ls /var/lib/docker/volumes/my_volume/_data
```
**Output**<br />
![Screenshot (55)](https://user-images.githubusercontent.com/65711565/227712893-b42ba8eb-9f59-42da-bb3a-54b6f59134c3.png)
**Remove the "my_volume" volume.**
```
docker volume rm my_volume
docker volume ls
```
**Output**<br />
![Screenshot (56)](https://user-images.githubusercontent.com/65711565/227712958-9b1dcee4-63de-4cd4-80fb-66aac3810cba.png)
**Create README.md file and describe your findings in markdown language.**
```
touch README.md
nano README.md
```
**Create git repo and clone it to local file.**
```
git clone https://github.com/abdulmoiz14/Part3.git
```
**copy to README file to Part3 folder and push it to the github.**
```
cp README.md /Part3
git add --all
git commit -m "adding codebase to the github"
git push -u origin main
```
