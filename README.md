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
- Git:

## 수행 항목 체크리스트
- [o] 터미널 기본 조작 및 폴더 구성
- [o] 권한 변경 실습
- [o] Docker 설치/점검
- [o] hello-world 실행
- [o] Dockerfile 빌드/실행
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
- 원인 : 

