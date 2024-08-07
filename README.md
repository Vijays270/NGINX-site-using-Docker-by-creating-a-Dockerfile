# NGINX-site-using-Docker-by-creating-a-Dockerfile in ubuntu
## NGINX site using Docker by creating a Dockerfile by following steps:

root@ip-172-31-41-40:~# apt update

root@ip-172-31-41-40:~# apt-get install apt-transport-https ca-certificates curl software-properties-common

root@ip-172-31-41-40:~# curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

root@ip-172-31-41-40:~# sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

root@ip-172-31-41-40:~# apt-get update

root@ip-172-31-41-40:~# apt-get install docker-ce

root@ip-172-31-41-40:~# systemctl status docker

root@ip-172-31-41-40:~# mkdir ~/mynginx

root@ip-172-31-41-40:~/mynginx# mkdir content

root@ip-172-31-41-40:~/mynginx# cd content

root@ip-172-31-41-40:~/mynginx/content# vi index.html

test site

root@ip-172-31-41-40:~/mynginx/content# vi Dockerfile

# Use the official NGINX image from Docker Hub
FROM nginx:latest

# Copy the content of the 'content' directory to the NGINX html directory
COPY .  /usr/share/nginx/html

root@ip-172-31-41-40:~/mynginx/content# docker build -t mynginximage .

[+] Building 5.0s (7/7) FINISHED                                                                                                   docker:default
 => [internal] load build definition from Dockerfile                                                                                         0.0s
 => => transferring dockerfile: 210B                                                                                                         0.0s
 => [internal] load metadata for docker.io/library/nginx:latest                                                                              0.4s
 => [internal] load .dockerignore                                                                                                            0.0s
 => => transferring context: 2B                                                                                                              0.0s
 => [internal] load build context                                                                                                            0.0s
 => => transferring context: 260B                                                                                                            0.0s
 => [1/2] FROM docker.io/library/nginx:latest@sha256:6af79ae5de407283dcea8b00d5c37ace95441fd58a8b1d2aa1ed93f5511bb18c                        4.2s
 => => resolve docker.io/library/nginx:latest@sha256:6af79ae5de407283dcea8b00d5c37ace95441fd58a8b1d2aa1ed93f5511bb18c                        0.0s
 => => sha256:a72860cb95fd59e9c696c66441c64f18e66915fa26b249911e83c3854477ed9a 7.30kB / 7.30kB                                               0.0s
 => => sha256:045037a63be803c1d446a5239439580a49cd8a8682a5addf4f03b2c1638948a4 627B / 627B                                                   0.3s
 => => sha256:6af79ae5de407283dcea8b00d5c37ace95441fd58a8b1d2aa1ed93f5511bb18c 10.27kB / 10.27kB                                             0.0s
 => => sha256:efc2b5ad9eec05befa54239d53feeae3569ccbef689aa5e5dbfc25da6c4df559 29.13MB / 29.13MB                                             0.6s
 => => sha256:8fe9a55eb80f3167f7b3a9c39f90b9eacf833841e5a9f8d60c51f4d2400154a3 41.83MB / 41.83MB                                             0.9s
 => => sha256:baa881b012a49e3c2cd6ab9d80f9fcd2962a98af8ede947d0ef930a427b28afc 2.29kB / 2.29kB                                               0.0s
 => => sha256:7111b42b4bfa1b5273abcc4b138983f48f9cb96bb3f896a6cb36af3dade80383 955B / 955B                                                   0.6s
 => => extracting sha256:efc2b5ad9eec05befa54239d53feeae3569ccbef689aa5e5dbfc25da6c4df559                                                    1.6s
 => => sha256:9e891cdb453be97c53e1ddbe4b955ee71099f18f16e68e7010c33662aaa944bf 1.21kB / 1.21kB                                               0.9s
 => => sha256:3dfc528a4df9e1be9b2817271a35cef87f001e699e5b8ef944640b383ca27e1f 394B / 394B                                                   0.9s
 => => sha256:0f11e17345c583a30e9cc89b80b1423b7b52b0e36cda9a6dc5de587ecf6ed54c 1.40kB / 1.40kB                                               1.0s
 => => extracting sha256:8fe9a55eb80f3167f7b3a9c39f90b9eacf833841e5a9f8d60c51f4d2400154a3                                                    1.4s
 => => extracting sha256:045037a63be803c1d446a5239439580a49cd8a8682a5addf4f03b2c1638948a4                                                    0.0s
 => => extracting sha256:7111b42b4bfa1b5273abcc4b138983f48f9cb96bb3f896a6cb36af3dade80383                                                    0.0s
 => => extracting sha256:3dfc528a4df9e1be9b2817271a35cef87f001e699e5b8ef944640b383ca27e1f                                                    0.0s
 => => extracting sha256:9e891cdb453be97c53e1ddbe4b955ee71099f18f16e68e7010c33662aaa944bf                                                    0.0s
 => => extracting sha256:0f11e17345c583a30e9cc89b80b1423b7b52b0e36cda9a6dc5de587ecf6ed54c                                                    0.0s
 => [2/2] COPY .  /usr/share/nginx/html                                                                                                      0.3s
 => exporting to image                                                                                                                       0.0s
 => => exporting layers                                                                                                                      0.0s
 => => writing image sha256:79b0378d1cb3c2134e2aa0bbd3fa0ca7e9fe361de42e4622ba4f0ab489f80185                                                 0.0s
 => => naming to docker.io/library/mynginximage 

root@ip-172-31-41-40:~/mynginx/content# docker image ls 
REPOSITORY     TAG       IMAGE ID       CREATED          SIZE
mynginximage   latest    79b0378d1cb3   28 minutes ago   188MB


root@ip-172-31-41-40:~/mynginx/content#  docker run --name mynginx -d -p 80:80 mynginximage
6e9cd6b87ca59edaf558167a4eb11c34b67674a9578026bf9547d6dde18000c9

root@ip-172-31-41-40:~/mynginx/content# docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                               NAMES
6e9cd6b87ca5   mynginximage   "/docker-entrypoint.…"   11 seconds ago   Up 11 seconds   0.0.0.0:80->80/tcp, :::80->80/tcp   mynginx





