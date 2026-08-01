# Codyssey_E1-1
Workstation Setup

## 프로젝트 개요
- 학습을 통해 터미널을 이용하여 작업 디렉토리와 권한을 정리하고 Docker를 설치 및 점검하고 컨테이너를 실행/관리할 수 있다.
- 이어서 간단한 웹 서버를 Dockerfile로 컨테이너화하고, 포트 매핑으로 접속을 확인하며, 바인드 마운트/볼륨으로 "변경 반영"과 "데이터 영속성"을 직접 검증할 수 있다.
- 각종 개념에 관해 이해하고 설명할 수 있다.

## 실행환경
- OS: Ubuntu 25.10
- Shell: zsh
- Docker: 28.5.2
- Git: 2.53.0

## 수행 항목 체크리스트
- [x] 터미널 기본 조작 및 폴더 구성
- [x] 권한 변경 실습
- [x] Docker 설치/점검
- [x] hello-world 실행
- [x] Dockerfile 빌드/실행
- [x] 포트 매핑 접속(2회)
- [x] 바인드 마운트 반영
- [x] 볼륨 영속성
- [x] Git 설정 + VSCode GitHub 연동

### 터미널 기본 조작 및 폴더 구성
Last login: Thu Jul 30 14:36:16 on console
lamb39723972@c6r6s6 ~ % pwd   
/Users/lamb39723972
lamb39723972@c6r6s6 ~ % mkdir ~/Desktop/terminal-study
lamb39723972@c6r6s6 ~ % cd ~/Desktop/terminal-study
lamb39723972@c6r6s6 terminal-study % pwd
/Users/lamb39723972/Desktop/terminal-study
lamb39723972@c6r6s6 terminal-study % touch og.txt
lamb39723972@c6r6s6 terminal-study % echo "Hello World" > og.txt    
lamb39723972@c6r6s6 terminal-study % cat og.txt
Hello World
lamb39723972@c6r6s6 terminal-study % mkdir practice_dir
lamb39723972@c6r6s6 terminal-study % ls -al
total 8
drwxr-xr-x  4 lamb39723972  lamb39723972  128  7 30 16:19 .
drwx------+ 6 lamb39723972  lamb39723972  192  7 30 16:11 ..
-rw-r--r--  1 lamb39723972  lamb39723972   12  7 30 16:18 og.txt
drwxr-xr-x  2 lamb39723972  lamb39723972   64  7 30 16:19 practice_dir
lamb39723972@c6r6s6 terminal-study % cp og.txt copy.txt
lamb39723972@c6r6s6 terminal-study % mv copy.txt renamed.txt
lamb39723972@c6r6s6 terminal-study % ls -al                 
total 16
drwxr-xr-x  5 lamb39723972  lamb39723972  160  7 30 16:20 .
drwx------+ 6 lamb39723972  lamb39723972  192  7 30 16:11 ..
-rw-r--r--  1 lamb39723972  lamb39723972   12  7 30 16:18 og.txt
drwxr-xr-x  2 lamb39723972  lamb39723972   64  7 30 16:19 practice_dir
-rw-r--r--  1 lamb39723972  lamb39723972   12  7 30 16:20 renamed.txt
lamb39723972@c6r6s6 terminal-study % rm og.txt
lamb39723972@c6r6s6 terminal-study % ls -al   
total 8
drwxr-xr-x  4 lamb39723972  lamb39723972  128  7 30 16:20 .
drwx------+ 6 lamb39723972  lamb39723972  192  7 30 16:11 ..
drwxr-xr-x  2 lamb39723972  lamb39723972   64  7 30 16:19 practice_dir
-rw-r--r--  1 lamb39723972  lamb39723972   12  7 30 16:20 renamed.txt

### 권한 변경 실습
lamb39723972@c6r6s6 terminal-study % ls -l renamed.txt 
-rw-r--r--  1 lamb39723972  lamb39723972  12  7 30 16:20 renamed.txt
lamb39723972@c6r6s6 terminal-study % chmod 444 renamed.txt 
lamb39723972@c6r6s6 terminal-study % ls -l renamed.txt    
-r--r--r--  1 lamb39723972  lamb39723972  12  7 30 16:20 renamed.txt
lamb39723972@c6r6s6 terminal-study % ls -ld practice_dir 
drwxr-xr-x  2 lamb39723972  lamb39723972  64  7 30 16:19 practice_dir
lamb39723972@c6r6s6 terminal-study % chmod 700 practice_dir 
lamb39723972@c6r6s6 terminal-study % ls -ld practice_dir   
drwx------  2 lamb39723972  lamb39723972  64  7 30 16:19 practice_dir

### Docker 설치/점검
lamb39723972@c6r6s6 ~ % docker --version           
Docker version 28.5.2, build ecc6942
lamb39723972@c6r6s6 ~ % docker info
Client:
 Version:    28.5.2
 Context:    orbstack
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.29.1
    Path:     /Users/lamb39723972/.docker/cli-plugins/docker-buildx
  compose: Docker Compose (Docker Inc.)
    Version:  v2.40.3
    Path:     /Users/lamb39723972/.docker/cli-plugins/docker-compose

Server:
 Containers: 1
  Running: 1
  Paused: 0
  Stopped: 0
 Images: 1
 Server Version: 28.5.2
 Storage Driver: overlay2
  Backing Filesystem: btrfs
  Supports d_type: true
  Using metacopy: false
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
 CDI spec directories:
  /etc/cdi
  /var/run/cdi
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 1c4457e00facac03ce1d75f7b6777a7a851e5c41
 runc version: d842d7719497cc3b774fd71620278ac9e17710e0
 init version: de40ad0
 Security Options:
  seccomp
   Profile: builtin
  cgroupns
 Kernel Version: 6.17.8-orbstack-00308-g8f9c941121b1
 Operating System: OrbStack
 OSType: linux
 Architecture: x86_64
 CPUs: 6
 Total Memory: 15.67GiB
 Name: orbstack
 ID: 20a027d1-ff08-4c4c-b980-813d29be7404
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Experimental: false
 Insecure Registries:
  ::1/128
  127.0.0.0/8
 Live Restore Enabled: false
 Product License: Community Engine
 Default Address Pools:
   Base: 192.168.97.0/24, Size: 24
   Base: 192.168.107.0/24, Size: 24
   Base: 192.168.117.0/24, Size: 24
   Base: 192.168.147.0/24, Size: 24
   Base: 192.168.148.0/24, Size: 24
   Base: 192.168.155.0/24, Size: 24
   Base: 192.168.156.0/24, Size: 24
   Base: 192.168.158.0/24, Size: 24
   Base: 192.168.163.0/24, Size: 24
   Base: 192.168.164.0/24, Size: 24
   Base: 192.168.165.0/24, Size: 24
   Base: 192.168.166.0/24, Size: 24
   Base: 192.168.167.0/24, Size: 24
   Base: 192.168.171.0/24, Size: 24
   Base: 192.168.172.0/24, Size: 24
   Base: 192.168.181.0/24, Size: 24
   Base: 192.168.183.0/24, Size: 24
   Base: 192.168.186.0/24, Size: 24
   Base: 192.168.207.0/24, Size: 24
   Base: 192.168.214.0/24, Size: 24
   Base: 192.168.215.0/24, Size: 24
   Base: 192.168.216.0/24, Size: 24
   Base: 192.168.223.0/24, Size: 24
   Base: 192.168.227.0/24, Size: 24
   Base: 192.168.228.0/24, Size: 24
   Base: 192.168.229.0/24, Size: 24
   Base: 192.168.237.0/24, Size: 24
   Base: 192.168.239.0/24, Size: 24
   Base: 192.168.242.0/24, Size: 24
   Base: 192.168.247.0/24, Size: 24
   Base: fd07:b51a:cc66:d000::/56, Size: 64

### hello-world 실행
lamb39723972@c6r6s6 ~ % docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

lamb39723972@c6r6s6 ~ % docker run -it ubuntu /bin/bash
root@1830d631b04a:/# ls
bin   dev  home  lib64  mnt  proc  run   srv  tmp  var
boot  etc  lib   media  opt  root  sbin  sys  usr
root@1830d631b04a:/# echo "Hello from Ubuntu"
Hello from Ubuntu
root@1830d631b04a:/# exit
exit
lamb39723972@c6r6s6 ~ %

### attach / exec 비교
- docker attach 는 컨테이너의 메인 프로세스에 연결
lamb39723972@c6r6s1 docker % docker run -it --name ubuntu-attach ubuntu bash 
root@0c2dc84a5240:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@0c2dc84a5240:/# echo "hello"
hello
root@0c2dc84a5240:/# exit
exit
lamb39723972@c6r6s1 docker % docker ps -a                                   
CONTAINER ID   IMAGE         COMMAND                  CREATED          STATUS                     PORTS                                     NAMES
0c2dc84a5240   ubuntu        "bash"                   20 seconds ago   Exited (0) 3 seconds ago                                             ubuntu-attach
ca08af19f8d5   nginx         "/docker-entrypoint.…"   2 hours ago      Up 2 hours                 0.0.0.0:8081->80/tcp, [::]:8081->80/tcp   bind-test
94c2dff3ca22   testweb       "/docker-entrypoint.…"   3 hours ago      Up 3 hours                 0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   web-test
4ef884062751   hello-world   "/hello"                 3 hours ago      Exited (0) 3 hours ago                                               sad_kare
bae5a4cca168   nginx         "/docker-entrypoint.…"   3 hours ago      Up 3 hours                 80/tcp                                    my-web

-> exit 입력 시 컨테이너도 함께 종료됨

- docker exec 은 컨테이너의 메인 프로세스에 연결
- 실행 중인 컨테이너에 새로운 프로세스를 추가로 실행
lamb39723972@c6r6s1 docker % docker run -d -it --name ubuntu-exec ubuntu bash
dc25b6b634f3f81e42abe773ec94a8db94852cb1bd842f8fcefecee4a8630816
lamb39723972@c6r6s1 docker % docker exec -it ubuntu-exec bash
root@dc25b6b634f3:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@dc25b6b634f3:/# echo "hello"
hello
root@dc25b6b634f3:/# exit
exit
lamb39723972@c6r6s1 docker % docker ps                                       
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                     NAMES
dc25b6b634f3   ubuntu    "bash"                   29 seconds ago   Up 27 seconds                                             ubuntu-exec
ca08af19f8d5   nginx     "/docker-entrypoint.…"   2 hours ago      Up 2 hours      0.0.0.0:8081->80/tcp, [::]:8081->80/tcp   bind-test
94c2dff3ca22   testweb   "/docker-entrypoint.…"   3 hours ago      Up 3 hours      0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   web-test
bae5a4cca168   nginx     "/docker-e

-> exit 해도 컨테이너가 종료되지 않음

### Docker 기본 명령
- 이미지 다운로드 목록/확인
lamb39723972@c6r6s1 docker % docker images      
REPOSITORY    TAG       IMAGE ID       CREATED          SIZE
testweb       latest    d3727cd6e393   41 minutes ago   161MB
nginx         latest    4e5db4761e0f   2 weeks ago      161MB
hello-world   latest    e2ac70e7319a   4 months ago     10.1kB

- 컨테이너: 실행/중지/목록 확인
lamb39723972@c6r6s1 docker % docker ps -a
CONTAINER ID   IMAGE         COMMAND                   CREATED          STATUS                      PORTS                                     NAMES
94c2dff3ca22   testweb       "/docker-entrypoint.…"   42 minutes ago   Up 42 minutes               0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   web-test
4ef884062751   hello-world   "/hello"                  49 minutes ago   Exited (0) 49 minutes ago                                             sad_kare
bae5a4cca168   nginx         "/docker-entrypoint.…"   50 minutes ago   Up 50 minutes               80/tcp                                    my-web

- 운영: 로그 확인, 리소스 확인
lamb39723972@c6r6s1 docker % docker logs my-web   
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2026/08/01 05:30:59 [notice] 1#1: using the "epoll" event method
2026/08/01 05:30:59 [notice] 1#1: nginx/1.31.3
2026/08/01 05:30:59 [notice] 1#1: built by gcc 14.2.0 (Debian 14.2.0-19) 
2026/08/01 05:30:59 [notice] 1#1: OS: Linux 6.17.8-orbstack-00308-g8f9c941121b1
2026/08/01 05:30:59 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 20480:1048576
2026/08/01 05:30:59 [notice] 1#1: start worker processes
2026/08/01 05:30:59 [notice] 1#1: start worker process 29
2026/08/01 05:30:59 [notice] 1#1: start worker process 30
2026/08/01 05:30:59 [notice] 1#1: start worker process 31
2026/08/01 05:30:59 [notice] 1#1: start worker process 32
2026/08/01 05:30:59 [notice] 1#1: start worker process 33
2026/08/01 05:30:59 [notice] 1#1: start worker process 34

lamb39723972@c6r6s1 docker % docker stats my-web
CONTAINER ID   NAME      CPU %     MEM USAGE / LIMIT     MEM %     NET I/O         BLOCK I/O         PIDS 
bae5a4cca168   my-web    0.00%     5.215MiB / 15.67GiB   0.03%     1.87kB / 126B   16.3MB / 8.19kB   7 

### Dockerfile 빌드/실행 + 포트 매핑
- 웹 서버 베이스 이미지 중 nginx를 활용하였다
- 폴더를 만들어 index.html과 Dockerfile을 생성하였다
- Dockerfile
FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
- Dockerfile을 통해 본 html 파일을 수정하였다.
- 매번 컨테이너에 들어가서 수정할 필요 없이, COPY 명령어를 통해 이미지를 만드는 시점에 파일을 미리 포함시켜 배포 효율성을 높임.
- 컨테이너 내부의 80번 포트를 내 컴퓨터(호스트)의 8080번 포트로 연결하여 브라우저에서 쉽게 접근할 수 있도록 설정함.

- 빌드
docker build -t nginx_test .
docker run -d -p 8080:80 --name my-web nginx_test

- 포트매핑

<img width="337" height="243" alt="스크린샷 2026-07-30 오후 9 07 11" src="https://github.com/user-attachments/assets/201fe6ac-72f4-4957-b2d9-1cc46e2075f4" />

- 트러블슈팅
- index.html 파일이 브라우저에서 렌더링되지 않고 소스 코드 그대로 출력됨.
- 원인 : index.html을 vscode가 아닌 텍스트 편집기로 편집하여 <p>형태로 입력되었음
- 해결 : vscode를 이용하여 정상적인 태그 활용

<img width="1694" height="1086" alt="스크린샷 2026-08-01 오후 2 40 12" src="https://github.com/user-attachments/assets/841d8795-5029-4a69-b0d7-47e55ffbf83e" />

### 바인드 마운트 반영
- 바인드 마운트하여 폴더와 동기화
lamb39723972@c6r6s1 docker % docker run -d -p 8081:80 -v $(pwd):/usr/share/nginx/html --name bind-test nginx
ca08af19f8d5b00366f3d6b7fdd70f45f3febd2360a9f3b473a3a1cd8ab9d1ec

- 8081 로 접속
<img width="476" height="304" alt="스크린샷 2026-08-01 오후 3 52 05" src="https://github.com/user-attachments/assets/539dde4f-d27b-4277-9a35-7cca6083aa8a" />

- index.html 변경 후 재접속
<img width="372" height="206" alt="스크린샷 2026-08-01 오후 3 54 02" src="https://github.com/user-attachments/assets/f60e6859-35eb-4e80-84f2-d91005e5912b" />

### 볼륨 영속성
- 컨테이너가 삭제되더 사라지지 않는 특별한 저장공간을 만드는 것
- 볼륨 생성
lamb39723972@c6r6s1 docker % docker volume create my-data
my-data
- 볼륨을 컨테이너의 /data 폴더에 연결하여 실행
lamb39723972@c6r6s1 docker % docker run -it --name vol-test-1 -v my-data:/data ubuntu bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
ed819469700f: Pull complete 
a3679419df18: Pull complete 
Digest: sha256:3131b4cc82a783df6c9df078f86e01819a13594b865c2cad47bd1bca2b7063bb
Status: Downloaded newer image for ubuntu:latest
- 컨테이너 내부에서 /data폴더로 이동후 파일 저장
root@6c060684545d:/# cd /data
root@6c060684545d:/data# echo "this data" > hello.txt
root@6c060684545d:/data# exit
exit
- 컨테이너 삭제
lamb39723972@c6r6s1 docker % docker rm vol-test-1
vol-test-1
- 새 컨테이너를 만들어 같은 볼륨을 연결
lamb39723972@c6r6s1 docker % docker run -it --name vol-test-2 -v my-data:/data ubuntu bash
- 데이터를 확인해보니 사라지지 않음을 확인
root@a945fbfe7b72:/# cat /data/hello.txt
this data

### Git 설정 + VSCode GitHub 연동
lamb39723972@c6r6s1 docker % git config --list
credential.helper=osxkeychain
user.name=Rascal7
user.email=***
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
core.ignorecase=true
core.precomposeunicode=true
remote.origin.url=https://github.com/Rascal7/Codyssey_E1-1.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
pull.rebase=false
branch.main.remote=origin
branch.main.merge=refs/heads/main

<img width="566" height="291" alt="스크린샷 2026-08-01 오후 5 10 18" src="https://github.com/user-attachments/assets/6cb111bb-8f44-4925-8580-598b09889e0e" />

-vscode 연동
<img width="1409" height="1145" alt="스크린샷 2026-08-01 오후 5 15 31" src="https://github.com/user-attachments/assets/da9ae91a-121e-4c8f-806a-125d25698224" />

