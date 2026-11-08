
# 내 컴퓨터에 개발자용 ‘작업실’ 꾸미기

## 프로젝트 개요

CLI, Git/Github, Docker 등의 개발자 도구를 설치 및 점검하여 물리적인 개발자 환경을 갖춤과 동시에 여러 명령을 시행해보면서 작동 방식과 원리를 배우는 개발자로서 사고방식을 갖추는 미션입니다. 

## 실행 환경

-Git : git version 2.39.3 (Apple Git-146)

ProductName:		macOS
ProductVersion:		14.3
BuildVersion:		23D56

-Docker version 29.9.2, build a82e528

## 수행 체크리스트

-제출 저장소  (O)

-터미널 기본 조작 (O)

-터미널 권한 변경 및 증거 기록  

-Docker 설치 및 운영 검증  (O)

-Dockerfile  (O)

-포토매핑 접속  (O)

-바인드 마운트  (O)

-볼륨 영속성   (O)

-Git 설정 및 Github/Vs code 연동 


## 터미널 조작 로그

#### 1. 현재 작업 경로 확인 (절대 경로)

pwd

/Users/2_sk

#### 2. 숨김 파일을 포함한 전체 목록 확인 (.git 폴더와 README.md 확인)

ls -la

#### 3. 실습용 테스트 디렉터리 생성 및 이동

mkdir practice

cd practice

pwd

/Users/practice

#### 4. 빈 파일 생성 및 텍스트 작성

touch original.txt

echo "Linux CLI Practice Test" > original.txt

#### 5. 파일 내용 확인

cat original.txt

#### 6. 파일 복사

cp original.txt copied.txt

ls -l

#### 7. 파일 이름 변경 (이동)

mv copied.txt renamed.txt
ls -l

#### 8. 파일 삭제

rm renamed.txt
ls -l

#### 9. 실습 디렉터리 빠져나오기 (상위 폴더 이동)

cd ..
pwd



## 권한 실습 증거 및 기록

#### 디렉토리 권한 변경

 ~ % mkdir change
 ~ % ls -ld change
drwxr-xr-x 2 2_sk staff 64 11 8 17:58 change
~ % chmod 655 change

~ % ls -ld change
drw-r-xr-x 2 2_sk staff 64 11 8 17:58 change

~ % chmod 755 change
~ % ls -ld change
drwxr-xr-x 2 2_sk staff 64 11 8 17:58 change

#### 파일 권한 변경

% cd change

% touch change-file
change % ls -l change-file
-rw-r--r--  1 2_sk  staff  0 11  8 18:03 change-file
change % chmod 755 change-file
change % ls -l change-file
-rwxr-xr-x  1 2_sk  staff  0 11  8 18:03 change-file


## docker 기본 운영 명령 수행

### docker —version

Docker version 29.9.2, build a82e528

### docker info

Client:
Version:    29.9.2
Context:    desktop-linux
Debug Mode: false
Plugins:
agent: Docker AI Agent Runner (Docker Inc.)
Version:  v1.152.0
Path:     /Users/2_sk/.docker/cli-plugins/docker-agent
ai: Docker AI Agent - Ask Gordon (Docker Inc.)
Version:  v1.33.0
Path:     /Users/2_sk/.docker/cli-plugins/docker-ai
buildx: Docker Buildx (Docker Inc.)
Version:  v0.38.1
Path:     /Users/2_sk/.docker/cli-plugins/docker-buildx
compose: Docker Compose (Docker Inc.)
Version:  v5.6.1
Path:     /Users/2_sk/.docker/cli-plugins/docker-compose
debug: Get a shell into any image or container (Docker Inc.)
Version:  0.49.0
Path:     /Users/2_sk/.docker/cli-plugins/docker-debug
desktop: Docker Desktop commands (Docker Inc.)
Version:  4.97.0
Path:     /Users/2_sk/.docker/cli-plugins/docker-desktop
dhi: CLI for managing Docker Hardened Images (Docker Inc.)
Version:  v0.0.9
Path:     /Users/2_sk/.docker/cli-plugins/docker-dhi
extension: Manages Docker extensions (Docker Inc.)
Version:  v0.2.32
Path:     /Users/2_sk/.docker/cli-plugins/docker-extension
init: Creates Docker-related starter files for your project (Docker Inc.)
Version:  v1.4.1
Path:     /Users/2_sk/.docker/cli-plugins/docker-init
mcp: Docker MCP Plugin (Docker Inc.)
Version:  v0.44.2
Path:     /Users/2_sk/.docker/cli-plugins/docker-mcp
model: Docker Model Runner (Docker Inc.)
Version:  v1.2.9
Path:     /Users/2_sk/.docker/cli-plugins/docker-model
offload: Docker Offload (Docker Inc.)
Version:  v0.7.21
Path:     /Users/2_sk/.docker/cli-plugins/docker-offload
pass: Docker Pass Secrets Manager Plugin (beta) (Docker Inc.)
Version:  v0.3.2
Path:     /Users/2_sk/.docker/cli-plugins/docker-pass
sandbox: "docker sandbox" is deprecated, use Docker Sandboxes instead (Docker Inc.)
Version:  v0.13.0
Path:     /Users/2_sk/.docker/cli-plugins/docker-sandbox
scout: Docker Scout (Docker Inc.)
Version:  v1.27.0
Path:     /Users/2_sk/.docker/cli-plugins/docker-scout

Server:
Containers: 10
Running: 0
Paused: 0
Stopped: 10
Images: 9
Server Version: 29.9.2
Storage Driver: overlayfs
driver-type: io.containerd.snapshotter.v1
Logging Driver: local
Cgroup Driver: cgroupfs
Cgroup Version: 2
Plugins:
Volume: local
Network: bridge host ipvlan macvlan null overlay
Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
CDI spec directories:
/etc/cdi
/var/run/cdi
Discovered Devices:
cdi: docker.com/gpu=webgpu
Swarm: inactive
Runtimes: io.containerd.runc.v2 runc
Default Runtime: runc
Init Binary: docker-init
containerd version: b7a25261e029d68978bbf290df0a62fc819b3c51
runc version: v1.5.2-0-g29dd3dc2
init version: de40ad0
Security Options:
seccomp
Profile: builtin
cgroupns
Kernel Version: 7.0.14-linuxkit
Operating System: Docker Desktop
OSType: linux
Architecture: aarch64
CPUs: 8
Total Memory: 7.748GiB
Name: docker-desktop
ID: 84a4a461-cb11-485e-997a-eb4fd2c6eda3
Docker Root Dir: /var/lib/docker
Debug Mode: false
HTTP Proxy: http.docker.internal:3128
HTTPS Proxy: http.docker.internal:3128
No Proxy: hubproxy.docker.internal
Labels:
com.docker.desktop.address=unix:///Users/2_sk/Library/Containers/com.docker.docker/Data/docker-cli.sock
Experimental: false
Insecure Registries:
hubproxy.docker.internal:5555
127.0.0.0/8
::1/128
Live Restore Enabled: false
Firewall Backend: iptables

### docker images

**i** Info →   U  In Use

**IMAGE**                           **ID**             **DISK USAGE**   **CONTENT SIZE**   **EXTRA**

**docker/welcome-to-docker:latest**

c4d56c24da4f       22.9MB         6.35MB    U

**hello-world:latest**              c567b231f656       22.6kB         10.3kB    U

**welcome-to-docker:latest**        f753e851c34f        479MB          132MB

### docker ps -a

CONTAINER ID   IMAGE                             COMMAND                   CREATED          STATUS                      PORTS     NAMES
4d01afd189a7   hello-world                       "/hello"                  10 minutes ago   Exited (0) 10 minutes ago             affectionate_payne
dae318668dd7   docker/welcome-to-docker:latest   "/docker-entrypoint.…"   4 days ago       Exited (0) 14 minutes ago             tutorial
41c3587db74f   docker/welcome-to-docker:latest   "/docker-entrypoint.…"   4 days ago       Exited (0) 4 days ago                 welcome-to-docker

### docker logs

docker: 'docker logs' requires 1 argument

Usage:  docker logs [OPTIONS] CONTAINER

Run 'docker logs --help' for more information

### docker stats

CONTAINER ID   NAME      CPU %     MEM USAGE / LIMIT   MEM %     NET I/O   BLOCK I/O   PIDS

### docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:

1. The Docker client contacted the Docker daemon.
2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
(arm64v8)
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

### docker run -it ubuntu bash

root@148df0534135:/# pwd

/

root@148df0534135:/# ls

**bin**   **dev**  **home**  **media**  **opt**   **root**  **sbin**  **sys**  **usr**

**boot**  **etc**  **lib**   **mnt**    **proc**  **run**   **srv**   tmp  **var**

root@148df0534135:/# echo "Hello everyone!"

Hello everyone!

root@148df0534135:/# whoami

root

root@148df0534135:/# cat /etc/os-release

PRETTY_NAME="Ubuntu 26.04.1 LTS"

NAME="Ubuntu"

VERSION_ID="26.04"

VERSION="26.04.1 LTS (Resolute Raccoon)"

VERSION_CODENAME=resolute

ID=ubuntu

ID_LIKE=debian

HOME_URL="https://www.ubuntu.com/"

SUPPORT_URL="https://help.ubuntu.com/"

BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"

PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"

UBUNTU_CODENAME=resolute

LOGO=ubuntu-logo


### docker start 148d

~ % docker ps
CONTAINER ID   IMAGE             COMMAND                   CREATED          STATUS          PORTS                                     NAMES
148df0534135   ubuntu            "bash"                    7 minutes ago    Up 13 seconds                                             eloquent_ardinghelli
4b50b113e674   practice-docker   "/docker-entrypoint.…"   40 minutes ago   Up 40 minutes   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   my-web

#### docker exec -it 148d /bin/bash


## dockerfile 작성하기

### dockerfile A안 웹서버 베이스 이미지

mkdir project-docker 

cd project-docker 

touch index.html 

cat << 'EOF' > index.html

<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<title>My Docker Web Server</title>
</head>
<body>
<h1>Docker 웹 서버 실행 성공!</h1>
<p>Dockerfile로 만든 나의 첫 번째 컨테이너입니다.</p>
</body>
</html>

EOF

#### touch Dockerfile

cat > Dockerfile << 'EOF'

FROM nginx:alpine
LABEL maintainer="myname@email.com"
COPY /usr/share/nginx/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

EOF

#### docker build -t practice-docker .

[+] Building 4.4s (8/8) FINISHED                           docker:desktop-linux
=> [internal] load build definition from Dockerfile                       0.0s
=> => transferring dockerfile: 171B                                       0.0s
=> [internal] load metadata for docker.io/library/nginx:alpine            2.2s
=> [auth] library/nginx:pull token for registry-1.docker.io               0.0s
=> [internal] load .dockerignore                                          0.0s
=> => transferring context: 2B                                            0.0s
=> [internal] load build context                                          0.0s
=> => transferring context: 319B                                          0.0s
=> [1/2] FROM docker.io/library/nginx:alpine@sha256:785835ea65db4bba6f02  1.5s
=> => resolve docker.io/library/nginx:alpine@sha256:785835ea65db4bba6f02  0.0s
=> => sha256:cbe54b031f3e1a4ce4471c96573084c6454f1c5f9 20.11MB / 20.11MB  0.7s
=> => sha256:c2fefbef531492feca04133b10436cc9783fce87888 1.40kB / 1.40kB  0.6s
=> => sha256:567a969e02211a0b0f51a1ac9b901e1bf88b7c79dbb 1.21kB / 1.21kB  0.7s
=> => sha256:dbb1ef19121a83d4810308cc89451dd32a5fafdf8d17da3 404B / 404B  0.7s
=> => sha256:f523b340a6c003e3b253f885115ab55af1d1f6a12a3fed8 964B / 964B  0.2s
=> => sha256:7b9d02243238d0f039c78eac1c532b5cc281e680fedbb27 629B / 629B  0.2s
=> => sha256:1408044c7403b2c319cdbb2cb2d18025d7997a703c1 1.96MB / 1.96MB  0.3s
=> => extracting sha256:1408044c7403b2c319cdbb2cb2d18025d7997a703c1c1115  0.1s
=> => extracting sha256:7b9d02243238d0f039c78eac1c532b5cc281e680fedbb27a  0.0s
=> => extracting sha256:f523b340a6c003e3b253f885115ab55af1d1f6a12a3fed82  0.0s
=> => extracting sha256:dbb1ef19121a83d4810308cc89451dd32a5fafdf8d17da3f  0.0s
=> => extracting sha256:567a969e02211a0b0f51a1ac9b901e1bf88b7c79dbb99497  0.0s
=> => extracting sha256:c2fefbef531492feca04133b10436cc9783fce87888d03b1  0.0s
=> => extracting sha256:cbe54b031f3e1a4ce4471c96573084c6454f1c5f91e03bbd  0.4s
=> [2/2] COPY app/ /usr/share/nginx/html/                                 0.1s
=> exporting to image                                                     0.5s
=> => exporting layers                                                    0.0s
=> => exporting manifest sha256:0e4770a360e97789c5e00304cb79658cd9a460fb  0.0s
=> => exporting config sha256:fbc80af8d1c74ea3a4ae72db77eb455d5e8f20cc62  0.0s
=> => exporting attestation manifest sha256:511ec3ba1bbd6f015fd5fa5eddad  0.0s
=> => exporting manifest list sha256:a00b76b73184d5aad1df3272d971315a378  0.0s
=> => naming to docker.io/library/practice-docker:latest                  0.0s
=> => unpacking to docker.io/library/practice-docker:latest               0.5s

### docker run -d -p 8080:80 --name my-web practice-docker

4b50b113e6749a35fa3f931bc1e513c2552dd91d46847e49c45f7672445483ea

http://localhost:8080

!스크린샷 2026-11-04 오후 7.19.12.png

---

### Dockerfile B안 리눅스 서버 베이스

cat << 'EOF' > opp/index.html 

<!DOCTYPE html>
<html>
<head><meta charset="UTF-8"><title>B방식 커스텀 이미지</title></head>
<body>
<h1>Ubuntu 베이스 커스텀 이미지 빌드 성공</h1>
<p>운영체제 위에 NGINX를 직접 설치하고 웹 문서를 교체했습니다.</p>
</body>
</html>

EOF

#### cat << 'EOF' > Dockerfile

FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y nginx

COPY app/index.html /var/www/html/index.html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

EOF 

#### docker build -t my-ubuntu-web:1.0 .

#### docker run -d --name ubuntu-web -p 8081:80 my-ubuntu-web:1.0

curl http://localhost:8081

!image.png


## docker 데이터 영속성 검증

### docker 바인드 마운트

- docker run -d --name bind-container -v bind-test

test:/app/bind-test ubuntu:22.04 sleep infinity
82d7d1da31b68f7d5f18419da91448aff922e0602bb2fdcdbd2fc2a1e911414d
2_sk@joisag-ui-MacBookAir-2 bind-test % docker exec bind-container cat /app/bind-test/test.txt
cat: /app/bind-test/test.txt: No such file or directory

- docker run -d --name bind-container -v ~/bind-test:/app/bind-test ubuntu 22:04 sleep infinity

1b8f0040ac99d1ca6457a41e709f7fd717848a2b1f2b66b4305dfaa677760930

docker: Error response from daemon: failed to create task for container: failed to create shim task: OCI runtime create failed: runc create failed: unable to start container process: error during container init: exec: "22:04": executable file not found in $PATH

Run 'docker run --help' for more information

**What's next:**

Debug this container error with Gordon → docker ai "help me fix this container error"

#### 실시간 데이터 공유 검증

~/bind-test % docker rm -f bind-container
bind-container
~/bind-test % docker run -d --name bind-container -v ~/bind-test:/app/bind-test ubuntu:22.04 sleep infinity
49f816ee041788f091dd9cd9bdbca36314a1fe403c7251faf0d957d84234861b
~/bind-test % docker exec bind-container cat /app/bind-test/test.txt
초기 데이터입니다

~/bind-test % docker exec bind-container cat /app/bind-test/test/txt
cat: /app/bind-test/test/txt: No such file or directory

~/bind-test % cat << 'EOF' >> test.txt
heredoc> 수정된 데이터입니다.
heredoc> EOF

~/bind-test % cat test.txt
초기 데이터입니다
수정된 데이터입니다.

~/bind-test % echo "맥북에서 데이터를 수정했습니다." >> test.txt
~/bind-test % cat test.txt
초기 데이터입니다
수정된 데이터입니다.
맥북에서 데이터를 수정했습니다.

~/bind-test % docker exec bind-container cat /app/bind-test/test.txt
초기 데이터입니다
수정된 데이터입니다.
맥북에서 데이터를 수정했습니다.

### docker 볼륨

 ~ % docker volume create my_assingment_volume
my_assingment_volume

 ~ % docker volume ls
DRIVER VOLUME NAME
local bind-test
local my_assingment_volume

~ % docker volume create my_assingment_volume
my_assingment_volume
~ % docker volume ls
DRIVER    VOLUME NAME
local     bind-test
local     my_assingment_volume
~ %

~ % docker run -d --name vol_container_1 -v my_assingment_volume:/app/data ubuntu:22.04 sleep infinity
7efd6f938db8cf66cfb9dbb217c428adc785bf18ea7891fb3e3f829730908cf2
~ % docker exec vol_container_1 bash -c 'echo "보존 되어야 할 데이터 " > /app/data/data.txt'
~ % docker exec vol_container_1 cat /app/data/data.txt
보존 되어야 할 데이터
~ %

#### 컨테이너를 제거 한 후에도 볼륨 파일은 남아 있다는 것을 확인.

% docker ps
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES

 % docker volume ls
DRIVER VOLUME NAME
local bind-test
local my_assignment_vol
local my_assignment_volume
local my_assingment_volume

### Git 설정 및 Github 연동

~ % git config --list
credential.helper=osxkeychain
init.defaultbranch=main
user.name=ISSAC JO
user.email=jobongdang6478@gmail.com
init.defaultbranch=main

practice % git remote -v
origin	https://github.com/jobongdang6478-commits/-.git (fetch)
origin	https://github.com/jobongdang6478-commits/-.git (push)