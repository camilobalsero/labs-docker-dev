# Se descargo imagen ubuntu
docker pull ubuntu

Using default tag: latest
latest: Pulling from library/ubuntu
9c704ecd0c69: Pull complete 
Digest: sha256:2e863c44b718727c860746568e1d54afd13b2fa71b160f5cd9058fc436217b30
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest

# Se descargo imagen de python 3.9
docker pull python:3.9

3.9: Pulling from library/python
ca4e5d672725: Pull complete 
30b93c12a9c9: Pull complete 
10d643a5fa82: Pull complete 
d6dc1019d793: Pull complete 
c387064957b7: Pull complete 
26766ebde481: Pull complete 
8a42d17fd0e2: Pull complete 
79eda865cc8a: Pull complete 
Digest: sha256:fea84f3a3b72c41efe7fc3b07ae209c6856b852b942c05fa88b747b74f70e711
Status: Downloaded newer image for python:3.9
docker.io/library/python:3.9

# ejecutar el contenedor de ubuntu en modo interactivo
docker run -it ubuntu bash

root@a04edd8dfdc5:

# ejecutar un servidor web apache en segundo plano utilizando el puerto 8000 del host al puerto 80 del contenedor
docker run -d -p 8000:80 httpd

Unable to find image 'httpd:latest' locally
latest: Pulling from library/httpd
efc2b5ad9eec: Already exists 
fce1785eb819: Pull complete 
4f4fb700ef54: Pull complete 
f214daa0692f: Pull complete 
05383fd8b2b3: Pull complete 
88ad12232aa1: Pull complete 
Digest: sha256:932ac36fabe1d2103ed3edbe66224ed2afe0041b317bcdb6f5d9be63594f0030
Status: Downloaded newer image for httpd:latest
bfee8c4591123e37d3d311b75ed0b47ee2d2bf01b1d50ee72d7d17fef0af2df1

# eliminar contenedores ubuntu
docker rm a04edd8dfdc5

a04edd8dfdc5

# visualizar que si se haya eliminado el contenedor ubuntu 
docker ps -a

CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                   NAMES
bfee8c459112   httpd     "httpd-foreground"       4 minutes ago    Up 4 minutes    0.0.0.0:8000->80/tcp, :::8000->80/tcp   zen_thompson
d90f0c0f592c   nginx     "/docker-entrypoint.…"   12 minutes ago   Up 12 minutes   0.0.0.0:8080->80/tcp, :::8080->80/tcp   intelligent_liskov

# eliminamos los contenedores detenidos
docker container prune -f

Total reclaimed space: 0B       

# Documentación laboratorio 2

# Crear el dockerfile y hacer el ejercicio 1 y 2 

docker build -t ubuntu-updated:latest .
[+] Building 10.9s (6/6) FINISHED                                                                                                                docker:default
 => [internal] load build definition from Dockerfile                                                                                                       0.3s
 => => transferring dockerfile: 96B                                                                                                                        0.0s
 => [internal] load metadata for docker.io/library/ubuntu:latest                                                                                           0.0s
 => [internal] load .dockerignore                                                                                                                          0.2s
 => => transferring context: 2B                                                                                                                            0.0s
 => [1/2] FROM docker.io/library/ubuntu:latest                                                                                                             0.1s
 => [2/2] RUN apt-get update && apt-get upgrade -y                                                                                                         8.9s
 => exporting to image                                                                                                                                     0.9s
 => => exporting layers                                                                                                                                    0.8s
 => => writing image sha256:b57ff4a90168188a95dad47bdd4afb26d76a4402693557ebdebdc01f7ef7240c                                                               0.0s
 => => naming to docker.io/library/ubuntu-updated:latest


# dockerfile para instalar nginx en ubuntu

docker build -t ubuntu-updated:latest .
[+] Building 14.2s (6/6) FINISHED                                                                                                                docker:default
 => [internal] load build definition from Dockerfile                                                                                                       0.1s
 => => transferring dockerfile: 138B                                                                                                                       0.0s
 => [internal] load metadata for docker.io/library/ubuntu:latest                                                                                           0.0s
 => [internal] load .dockerignore                                                                                                                          0.1s
 => => transferring context: 2B                                                                                                                            0.0s
 => CACHED [1/2] FROM docker.io/library/ubuntu:latest                                                                                                      0.0s
 => [2/2] RUN apt-get update && apt-get install -y nginx                                                                                                  13.0s
 => exporting to image                                                                                                                                     0.6s
 => => exporting layers                                                                                                                                    0.5s
 => => writing image sha256:50dbdc36a5dbb7f791e0c6e753e51774d78ca49e2b7d1809732582b1e9badee1                                                               0.0s
 => => naming to docker.io/library/ubuntu-updated:latest      


 # Construir la imagen de Nginx

 docker build -t my-nginx:latest .
[+] Building 0.5s (6/6) FINISHED                                                                                                                 docker:default
 => [internal] load build definition from Dockerfile                                                                                                       0.1s
 => => transferring dockerfile: 138B                                                                                                                       0.0s
 => [internal] load metadata for docker.io/library/ubuntu:latest                                                                                           0.0s
 => [internal] load .dockerignore                                                                                                                          0.1s
 => => transferring context: 2B                                                                                                                            0.0s
 => [1/2] FROM docker.io/library/ubuntu:latest                                                                                                             0.0s
 => CACHED [2/2] RUN apt-get update && apt-get install -y nginx                                                                                            0.0s
 => exporting to image                                                                                                                                     0.1s
 => => exporting layers                                                                                                                                    0.0s
 => => writing image sha256:50dbdc36a5dbb7f791e0c6e753e51774d78ca49e2b7d1809732582b1e9badee1                                                               0.0s
 => => naming to docker.io/library/my-nginx:latest           

# ejecutar la imagen 

docker run -d -p 80:80 my-nginx:latest
af857b260163ef8c4da16c6a18d840dbb51ef4da8940bffc2f97e2afa1d0c8d5


# Modificar el Dockerfile de Nginx para exponer el puerto 80 y reconstruirlo

 docker build -t my-nginx:latest .
[+] Building 0.6s (6/6) FINISHED                                                                                                                 docker:default
 => [internal] load build definition from Dockerfile                                                                                                       0.1s
 => => transferring dockerfile: 147B                                                                                                                       0.0s
 => [internal] load metadata for docker.io/library/ubuntu:latest                                                                                           0.0s
 => [internal] load .dockerignore                                                                                                                          0.1s
 => => transferring context: 2B                                                                                                                            0.0s
 => [1/2] FROM docker.io/library/ubuntu:latest                                                                                                             0.0s
 => CACHED [2/2] RUN apt-get update && apt-get install -y nginx                                                                                            0.0s
 => exporting to image                                                                                                                                     0.1s
 => => exporting layers                                                                                                                                    0.0s
 => => writing image sha256:2e31d5ae8172f49924ff475aeff6bb142e998dfe9ef60303005e1fb94b1dc020                                                               0.0s
 => => naming to docker.io/library/my-nginx:latest 

 
 # Copiar un archivo HTML local a una imagen de Nginx

 docker build -t my-nginx:latest .
[+] Building 2.7s (7/7) FINISHED                                                                                                      docker:default
 => [internal] load build definition from Dockerfile                                                                                            0.1s
 => => transferring dockerfile: 94B                                                                                                             0.0s
 => [internal] load metadata for docker.io/library/nginx:latest                                                                                 0.0s
 => [internal] load .dockerignore                                                                                                               0.1s
 => => transferring context: 2B                                                                                                                 0.0s
 => [internal] load build context                                                                                                               0.5s
 => => transferring context: 255B                                                                                                               0.0s
 => [1/2] FROM docker.io/library/nginx:latest                                                                                                   0.9s
 => [2/2] COPY index.html /usr/share/nginx/html/                                                                                                0.3s
 => exporting to image                                                                                                                          1.0s
 => => exporting layers                                                                                                                         0.8s
 => => writing image sha256:ef931c2c2bf34fb8dfc478fb32f25e04f75231e5b924226e1c04dd81a421e365                                                    0.0s
 => => naming to docker.io/library/my-nginx:latest        

 # Usar WORKDIR y copiar un archivo

 docker build -t ubuntu-updated:latest .
[+] Building 1.4s (8/8) FINISHED                                                                                                      docker:default
 => [internal] load build definition from Dockerfile                                                                                            0.1s
 => => transferring dockerfile: 87B                                                                                                             0.0s
 => [internal] load metadata for docker.io/library/ubuntu:latest                                                                                0.0s
 => [internal] load .dockerignore                                                                                                               0.0s
 => => transferring context: 2B                                                                                                                 0.0s
 => [1/3] FROM docker.io/library/ubuntu:latest                                                                                                  0.0s
 => [internal] load build context                                                                                                               0.0s
 => => transferring context: 31B                                                                                                                0.0s
 => CACHED [2/3] WORKDIR /app                                                                                                                   0.0s
 => [3/3] COPY myfile.txt .                                                                                                                     0.3s
 => exporting to image                                                                                                                          0.6s
 => => exporting layers                                                                                                                         0.5s
 => => writing image sha256:f9f06c09e61ae5d28615c3f3729434b81c0fc21a1f0e0690e073d80d8af031ad                                                    0.0s
 => => naming to docker.io/library/ubuntu-updated:latest  

 # Ejecutar un script Python al iniciar el contenedor

 docker build -t python:3.9 .
[+] Building 4.4s (8/8) FINISHED                                                                                                                 docker:default
 => [internal] load build definition from Dockerfile                                                                                                       0.1s
 => => transferring dockerfile: 110B                                                                                                                       0.0s
 => [internal] load metadata for docker.io/library/python:3.9                                                                                              0.0s
 => [internal] load .dockerignore                                                                                                                          0.0s
 => => transferring context: 2B                                                                                                                            0.0s
 => [1/3] FROM docker.io/library/python:3.9                                                                                                                0.8s
 => [internal] load build context                                                                                                                          0.2s
 => => transferring context: 30B                                                                                                                           0.0s
 => [2/3] WORKDIR /app                                                                                                                                     0.2s
 => [3/3] COPY script.py .                                                                                                                                 0.2s
 => exporting to image                                                                                                                                     2.7s
 => => exporting layers                                                                                                                                    2.5s
 => => writing image sha256:925bd2a7c5d8bb3629385b570647aa2fd423f03652a6db532f913c1bc5b4bb6d                                                               0.0s
 => => naming to docker.io/library/python:3.9               