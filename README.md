# 내 컴퓨터에 개발자용 ‘작업실’ 꾸미기

## 1. 프로젝트 개요
CLI, Git/GitHub, Docker 등 핵심 개발자 도구를 로컬 환경에 구축·점검하고, 주요 명령어를 직접 실행하며 작동 원리를 체득하는 개발 환경 세팅 미션입니다.

---

## 2. 실행 환경

| 항목 | 버전 / 사양 |
| :--- | :--- |
| **OS** | macOS 14.3 (Build 23D56, Apple Silicon / `aarch64`) |
| **Shell / Terminal** | `zsh` (macOS 기본 터미널) |
| **Git** | `git version 2.39.3 (Apple Git-146)` |
| **Docker** | `Docker version 29.9.2, build a82e528` (Docker Desktop) |
| **Editor** | Visual Studio Code |

---

## 3. 수행 항목 체크리스트

- [x] 제출 저장소(GitHub Repository) 생성 및 연동
- [x] 터미널 기본 조작 (탐색·생성·복사·이동·삭제)
- [x] 터미널 파일 및 디렉터리 권한 변경(`chmod`) 및 증거 기록
- [x] Docker 설치 및 기본 운영 명령 검증
- [x] Dockerfile 기반 커스텀 웹 서버 이미지 빌드 (A안: Nginx / B안: Ubuntu)
- [x] 포트 매핑(`-p`) 기반 웹 서버 접속 확인
- [x] 바인드 마운트(Bind Mount) 실시간 동기화 검증
- [x] Docker 볼륨(Volume) 데이터 영속성 검증
- [x] Git 사용자 설정 및 GitHub / VS Code 연동

---

## 4. 검증 방법 및 결과 요약

| 검증 영역 | 핵심 검증 명령어 | 확인 내용 | 결과 위치 |
| :--- | :--- | :--- | :--- |
| **터미널 조작** | `pwd`, `ls -la`, `mkdir`, `touch`, `cp`, `mv`, `rm` | 파일/디렉터리 생성·수정·복사·이름 변경·삭제 흐름 | [5. 터미널 조작 및 권한 실습](#5-터미널-조작-및-권한-실습) |
| **권한 관리** | `ls -ld`, `ls -l`, `chmod 655/755` | 디렉터리 및 파일의 읽기/쓰기/실행 권한 변경 확인 | [5-2. 권한 변경 실습](#5-2-권한-변경-실습) |
| **Docker 운영** | `docker --version`, `docker info`, `images`, `ps -a`, `run`, `exec` | 데몬 정상 동작, 이미지/컨테이너 생명주기 및 셸 접속 | [6. Docker 운영 및 검증 로그](#6-docker-운영-및-검증-로그) |
| **Dockerfile & 포트** | `docker build`, `docker run -d -p 8080:80`, `curl` | 커스텀 웹 서버 이미지 빌드 및 호스트 포트 포워딩 접속 | [7. Dockerfile 기반 웹 서버 컨테이너](#7-dockerfile-기반-웹-서버-컨테이너) |
| **데이터 영속성** | `docker run -v`, `docker volume create/ls` | 바인드 마운트 실시간 반영 및 컨테이너 삭제 후 볼륨 유지 | [8. 데이터 영속성 검증](#8-데이터-영속성-검증) |
| **Git & GitHub** | `git config --list`, `git remote -v` | 사용자 정보·기본 브랜치(`main`)·원격 저장소 연결 확인 | [9. Git 설정 및 GitHub / VS Code 연동](#9-git-설정-및-github--vs-code-연동) |

---

## 5. 터미널 조작 및 권한 실습

### 5-1. 기본 CLI 조작 로그

```bash
# 1. 현재 작업 경로 확인 (절대 경로)
pwd
# /Users/2_sk

# 2. 숨김 파일 포함 전체 목록 확인 (.git, README.md 등)
ls -la

# 3. 실습용 디렉터리 생성 및 이동
mkdir practice
cd practice
pwd
# /Users/2_sk/practice

# 4. 파일 생성 및 텍스트 작성, 내용 확인
touch original.txt
echo "Linux CLI Practice Test" > original.txt
cat original.txt
# Linux CLI Practice Test

# 5. 파일 복사, 이름 변경(이동), 삭제
cp original.txt copied.txt
ls -l

mv copied.txt renamed.txt
ls -l

rm renamed.txt
ls -l

# 6. 상위 디렉터리로 이동
cd ..
pwd
```

### 5-2. 권한 변경 실습

**디렉터리 권한 변경 (`755` → `655` → `755`)**
```bash
~ % mkdir change
~ % ls -ld change
drwxr-xr-x 2 2_sk staff 64 11 8 17:58 change

~ % chmod 655 change
~ % ls -ld change
drw-r-xr-x 2 2_sk staff 64 11 8 17:58 change

~ % chmod 755 change
~ % ls -ld change
drwxr-xr-x 2 2_sk staff 64 11 8 17:58 change
```

**파일 권한 변경 (`644` → `755`)**
```bash
~ % cd change
change % touch change-file
change % ls -l change-file
-rw-r--r-- 1 2_sk staff 0 11 8 18:03 change-file

change % chmod 755 change-file
change % ls -l change-file
-rwxr-xr-x 1 2_sk staff 0 11 8 18:03 change-file
```

---

## 6. Docker 운영 및 검증 로그

### 6-1. 설치 및 시스템 상태 점검

```bash
# Docker 버전 확인
docker --version
# Docker version 29.9.2, build a82e528

# Docker 시스템 핵심 정보 요약 (docker info)
Client:
 Version:    29.9.2
 Context:    desktop-linux

Server:
 Containers: 10 (Running: 0, Paused: 0, Stopped: 10)
 Images:     9
 Server Version: 29.9.2
 Storage Driver: overlayfs (io.containerd.snapshotter.v1)
 Cgroup Driver:  cgroupfs (Version 2)
 Operating System: Docker Desktop (linux / aarch64)
 CPUs: 8 / Total Memory: 7.748GiB
```

### 6-2. 이미지·컨테이너 조회 및 기본 실행

```bash
# 로컬 이미지 목록 확인
docker images
# IMAGE                            ID             DISK USAGE   CONTENT SIZE   EXTRA
# docker/welcome-to-docker:latest  c4d56c24da4f   22.9MB       6.35MB         U
# hello-world:latest               c567b231f656   22.6kB       10.3kB         U
# welcome-to-docker:latest         f753e851c34f   479MB        132MB

# 전체 컨테이너 상태 확인
docker ps -a
# CONTAINER ID   IMAGE                             COMMAND                  CREATED          STATUS                      PORTS     NAMES
# 4d01afd189a7   hello-world                       "/hello"                 10 minutes ago   Exited (0) 10 minutes ago             affectionate_payne
# dae318668dd7   docker/welcome-to-docker:latest   "/docker-entrypoint.…"   4 days ago       Exited (0) 14 minutes ago             tutorial
# 41c3587db74f   docker/welcome-to-docker:latest   "/docker-entrypoint.…"   4 days ago       Exited (0) 4 days ago                 welcome-to-docker

# 리소스 사용량 모니터링 확인 (실행 중 컨테이너 없음)
docker stats
# CONTAINER ID   NAME   CPU %   MEM USAGE / LIMIT   MEM %   NET I/O   BLOCK I/O   PIDS

# hello-world 컨테이너 실행 검증
docker run hello-world
# Hello from Docker!
# This message shows that your installation appears to be working correctly.
```

### 6-3. Ubuntu 컨테이너 대화형 접속 및 생명주기 관리

```bash
# Ubuntu 컨테이너 실행 및 배시 셸 진입
docker run -it ubuntu bash
root@148df0534135:/# pwd
/
root@148df0534135:/# ls
bin  boot  dev  etc  home  lib  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@148df0534135:/# echo "Hello everyone!"
Hello everyone!
root@148df0534135:/# whoami
root
root@148df0534135:/# cat /etc/os-release
PRETTY_NAME="Ubuntu 26.04.1 LTS"
NAME="Ubuntu"
VERSION_ID="26.04"

# 종료된 컨테이너 재시작 및 실행 확인 후 재접속
docker start 148d
docker ps
# CONTAINER ID   IMAGE             COMMAND                  CREATED          STATUS          PORTS                                     NAMES
# 148df0534135   ubuntu            "bash"                   7 minutes ago    Up 13 seconds                                             eloquent_ardinghelli
# 4b50b113e674   practice-docker   "/docker-entrypoint.…"   40 minutes ago   Up 40 minutes   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   my-web

docker exec -it 148d /bin/bash
```

---

## 7. Dockerfile 기반 웹 서버 컨테이너

### 7-1. A안: 경량 웹 서버 베이스 (`nginx:alpine`)

**웹 페이지 소스 (`app/index.html`)**
```bash
mkdir -p project-docker/app && cd project-docker
cat << 'EOF' > app/index.html
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
```

**Dockerfile**
```bash
cat << 'EOF' > Dockerfile
FROM nginx:alpine
LABEL maintainer="myname@email.com"
COPY app/ /usr/share/nginx/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
EOF
```

**이미지 빌드 및 컨테이너 실행 (`8080:80` 포트 매핑)**
```bash
docker build -t practice-docker .
# [+] Building 4.4s (8/8) FINISHED docker:desktop-linux
#  => [1/2] FROM docker.io/library/nginx:alpine
#  => [2/2] COPY app/ /usr/share/nginx/html/
#  => naming to docker.io/library/practice-docker:latest

docker run -d -p 8080:80 --name my-web practice-docker
# 4b50b113e6749a35fa3f931bc1e513c2552dd91d46847e49c45f7672445483ea
```

**포트 매핑 접속 증거 (`http://localhost:8080`)**
> ![A안 웹 서버 브라우저 접속 화면](./images/web-nginx-8080.png)
> *(추후 주소창이 포함된 브라우저 접속 스크린샷 첨부 예정)*

---

### 7-2. B안: 리눅스 OS 베이스 (`ubuntu:22.04` + NGINX 직접 설치)

**웹 페이지 소스 (`app/index.html`)**
```bash
cat << 'EOF' > app/index.html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>B방식 커스텀 이미지</title>
</head>
<body>
  <h1>Ubuntu 베이스 커스텀 이미지 빌드 성공</h1>
  <p>운영체제 위에 NGINX를 직접 설치하고 웹 문서를 교체했습니다.</p>
</body>
</html>
EOF
```

**Dockerfile**
```bash
cat << 'EOF' > Dockerfile
FROM ubuntu:22.04
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y nginx
COPY app/index.html /var/www/html/index.html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
EOF
```

**이미지 빌드·실행 및 응답 검증 (`8081:80` 포트 매핑)**
```bash
docker build -t my-ubuntu-web:1.0 .
docker run -d --name ubuntu-web -p 8081:80 my-ubuntu-web:1.0
curl http://localhost:8081
```

**포트 매핑 접속 증거 (`http://localhost:8081`)**
> ![B안 웹 서버 브라우저 접속 화면](./images/web-ubuntu-8081.png)
> *(추후 주소창이 포함된 브라우저 접속 스크린샷 첨부 예정)*

---

## 8. 데이터 영속성 검증

### 8-1. 바인드 마운트 (Bind Mount) 실시간 공유 검증

호스트의 `~/bind-test` 디렉터리를 컨테이너의 `/app/bind-test`에 마운트하여 호스트 파일 수정이 컨테이너 내부에 즉시 반영되는지 확인했습니다.

```bash
# 바인드 마운트 컨테이너 실행
docker run -d --name bind-container -v ~/bind-test:/app/bind-test ubuntu:22.04 sleep infinity

# [변경 전] 컨테이너 내부에서 초기 파일 확인
docker exec bind-container cat /app/bind-test/test.txt
# 초기 데이터입니다

# [호스트 변경] 로컬(macOS)에서 파일에 내용 추가
cat << 'EOF' >> ~/bind-test/test.txt
수정된 데이터입니다.
EOF
echo "맥북에서 데이터를 수정했습니다." >> ~/bind-test/test.txt

# [변경 후] 컨테이너 내부에서 실시간 반영 확인
docker exec bind-container cat /app/bind-test/test.txt
# 초기 데이터입니다
# 수정된 데이터입니다.
# 맥북에서 데이터를 수정했습니다.
```

### 8-2. Docker 볼륨 (Volume) 영속성 검증

명명된 볼륨(`my_assingment_volume`)을 생성해 컨테이너에 연결하고, 컨테이너 삭제 후에도 볼륨과 데이터가 유지되는지 검증했습니다.

```bash
# 1. 볼륨 생성 및 목록 확인
docker volume create my_assingment_volume
docker volume ls
# DRIVER    VOLUME NAME
# local     bind-test
# local     my_assingment_volume

# 2. 볼륨을 마운트한 컨테이너 실행 및 데이터 기록
docker run -d --name vol_container_1 -v my_assingment_volume:/app/data ubuntu:22.04 sleep infinity
docker exec vol_container_1 bash -c 'echo "보존 되어야 할 데이터" > /app/data/data.txt'

# 3. [삭제 전] 컨테이너 내부 데이터 확인
docker exec vol_container_1 cat /app/data/data.txt
# 보존 되어야 할 데이터

# 4. [삭제 후] 컨테이너 제거 확인 및 볼륨 잔존 검증
docker ps
# CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

docker volume ls
# DRIVER    VOLUME NAME
# local     bind-test
# local     my_assignment_vol
# local     my_assignment_volume
# local     my_assingment_volume
```

---

## 9. Git 설정 및 GitHub / VS Code 연동

민감한 인증 정보(비밀번호, PAT 등)가 노출되지 않도록 macOS 키체인(`osxkeychain`)을 자격 증명 도우미로 설정하고, 사용자 정보 및 원격 저장소를 연결했습니다.

```bash
# Git 전역 설정 확인
git config --list
# credential.helper=osxkeychain
# init.defaultbranch=main
# user.name=ISSAC JO
# user.email=jobongdang6478@gmail.com

# 원격 저장소(GitHub) 연결 확인
git remote -v
# origin  [https://github.com/jobongdang6478-commits/-.git](https://github.com/jobongdang6478-commits/-.git) (fetch)
# origin  [https://github.com/jobongdang6478-commits/-.git](https://github.com/jobongdang6478-commits/-.git) (push)
```

**VS Code – GitHub 연동 증거**
> ![VS Code GitHub 연동 화면](./images/vscode-github-sync.png)
> *(추후 VS Code 좌측 소스 제어 / GitHub 계정 로그인 확인 스크린샷 첨부 예정)*

---

## 10. 트러블슈팅 (Troubleshooting)

### Case 1. 바인드 마운트 후 컨테이너에서 호스트 파일을 찾을 수 없는 문제
* **문제**: `docker run -d --name bind-container -v bind-test:/app/bind-test ...` 실행 후 컨테이너 내부에서 `test.txt`를 조회하자 `No such file or directory` 오류 발생.
* **원인 가설**: `-v` 옵션의 소스 경로를 절대 경로(`/...`, `~/...`)나 상대 경로(`./...`)로 명시하지 않으면, Docker가 이를 호스트 디렉터리가 아닌 **Named Volume**으로 인식하여 빈 볼륨을 새로 생성할 것이라 추정.
* **확인**: `docker volume ls` 실행 결과 `local bind-test`라는 이름의 볼륨이 생성되어 있음을 확인.
* **해결/대안**: 기존 컨테이너를 `docker rm -f bind-container`로 제거한 뒤, 호스트 경로를 `~/bind-test:/app/bind-test`로 명확히 지정하여 재실행함으로써 실시간 파일 공유 정상 동작을 확인.

### Case 2. `docker run` 실행 시 `executable file not found in $PATH` 오류
* **문제**: 컨테이너 실행 시 `exec: "22:04": executable file not found in $PATH` 오류가 발생하며 컨테이너 초기화 실패.
* **원인 가설**: 이미지 이름과 태그를 구분하는 콜론(`:`) 대신 공백을 입력하여(`ubuntu 22:04`), Docker가 `22:04`를 이미지 태그가 아닌 컨테이너 내부에서 실행할 명령어(CMD)로 해석했을 것이라 추정.
* **확인**: 실행 명령어 이력을 검토한 결과 `ubuntu:22.04`가 아닌 `ubuntu 22:04`로 오타가 입력된 것을 확인.
* **해결/대안**: 이미지와 태그를 `ubuntu:22.04`로 정확히 수정하여 재실행함으로써 컨테이너가 정상 기동됨을 확인.

### Case 3. `docker logs` 실행 시 인자 부족 오류
* **문제**: 컨테이너 로그 확인을 위해 `docker logs`를 단독 실행하자 `docker: 'docker logs' requires 1 argument` 오류 출력.
* **원인 가설**: `docker logs`는 어떤 컨테이너의 로그를 조회할지 대상 식별자(Container ID 또는 Name)를 필수로 요구할 것이라 추정.
* **확인**: 출력된 Usage 메시지(`Usage: docker logs [OPTIONS] CONTAINER`)를 통해 컨테이너 지정이 필수임을 확인.
* **해결/대안**: `docker ps -a`로 대상 컨테이너 이름이나 ID를 먼저 확인한 뒤 `docker logs my-web` 형태로 컨테이너를 지정하여 로그를 조회하도록 개선.