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
