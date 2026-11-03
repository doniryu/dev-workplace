# dev-workplace
코디세이 1-1 프로젝트

## 진행 상황
Windows PowerShell에서 파일 만들기, 읽기, 복사, 이름 바꾸기, 이동, 삭제를 연습했다.
Git 설정을 완료하고 실습 명령어 기록을 GitHub에 올렸다


## 사용 환경
- 운영체제: Windows 11
- 편집기: Visual Studio Code
- 터미널: Windows PowerShell
- Git 버전: 2.56.0.windows.4
- 추가 실습 환경: macOS Sequoia 15.8.2, Intel MacBook Pro
- Docker Desktop 설치 및 hello-world 실행 완료
- Docker 컨테이너에서 Ubuntu 24.04 권한 실습 완료

## 터미널 실습 기록
파일과 폴더를 만들고, 복사하고, 이름을 바꾸고, 이동하고, 삭제하는 연습을 했다.

[입력한 명령어 기록 보기](history.txt)

## Git 상태 확인 화면
![Git 상태 확인 결과](screenshots/git-status.png)

## 오류와 해결 과정

### Git 명령어 오타
- 문제: git ststus를 입력하니 명령어를 찾을 수 없다는 오류가 나왔다.
- 원인: status의 철자를 잘못 입력했다. 
- 해결: git status로 고쳐 입력했다.
- 결과: 현재 브랜치와 파일 변경 상태가 정상적으로 표시됐다. 

### Docker 설치 문제
- 문제: 학교 Windows 컴퓨터에서 Docker Desktop 설치 중 Virtual Machine Platform 관련 오류가 발생했다.
- 원인 가설: 가상화 기능과 관리자 권한 제한으로 설치가 어려운 것으로 보았다.
- 확인: 설치 안내에서 관리자 권한이 필요함을 확인했고, 담당자에게 서버 문제도 있다는 안내를 받았다.
- 대안: 개인 Intel MacBook에서 Docker Desktop을 설치하여 실습을 진행했다.
- 결과: hello-world 실행, 커스텀 웹페이지 실행, 포트 매핑, 바인드 마운트, 볼륨 데이터 유지 확인을 완료했다. 학교 컴퓨터의 설치 문제는 해결되지 않았다.

## 터미널 실습 따라 하기
Windows PowerShell에서 아래 명령어를 한 줄씩 입력한다.
실습할 위치에 practice 폴더가 없다면 다음 명령어로 만들고 들어간다.

    mkdir practice
    cd practice

파일을 만들고 내용을 저장한 뒤 확인한다.

    New-Item -Name hello.txt -ItemType File
    Set-Content hello.txt "Hello"
    Get-Content hello.txt

마지막 명령어를 실행하면 Hello가 표시된다.

파일을 복사하고 이름을 바꾼 뒤 폴더로 이동한다.

    Copy-Item hello.txt copy.txt
    Rename-Item copy.txt renamed.txt
    mkdir archive
    Move-Item renamed.txt archive
    Get-ChildItem archive

archive 폴더 안에 renamed.txt가 표시된다.

이동한 파일을 삭제한 다음 빈 폴더를 삭제한다.

    Remove-Item archive/renamed.txt
    Remove-Item archive
    Get-ChildItem

이 순서대로 실습했다면 practice 폴더에는 hello.txt만 남는다.

## 파일 내용 확인 화면
hello.txt에 저장한 Hello가 출력되는 것을 확인했다.

![파일 내용 확인 경과](screenshots/hello-output.png)

## 숨김 항목을 포함한 목록 확인
Get-ChildItem -Force를 실행하여 숨김 폴더인 .git까지 확인했다.

![파일과 폴더 목록](screenshots/folder-list.png)

## macOS 권한 연습
연습용 폴더와 파일에 chmod를 적용하고 변경 전후를 확인했다.

- r: 읽기, w: 쓰기, x: 실행(폴더에서는 접근)
- 폴더: 755 → 700 → 755
- 파일: 644 → 600 → 644
- 700·600은 소유자만 접근하도록 제한한 설정이다.
- macOS와 Docker의 Ubuntu 24.04에서 파일과 폴더의 권한 변경을 확인했다.

[권한 변경 결과](permission-practice/permissions-log.txt)

## Linux 권한 실습
Docker의 Ubuntu 24.04 안에서 파일과 폴더의 권한을 변경했다.

- 폴더: 755 → 700 → 755
- 파일: 644 → 600 → 644
- 변경 전, 제한한 상태, 복원한 상태를 기록했다.

[Linux 권한 변경 결과](linux-practice/permissions-log.txt)

## Docker 실습 결과
Dockerfile로 my-web 이미지를 만들고 웹페이지를 실행했다.

- 8080번과 8081번 포트에서 각각 웹페이지 접속을 확인했다.
- logs로 실행 기록, stats로 CPU와 메모리 사용량을 확인했다.
- 컨테이너를 중지한 뒤 다시 시작했다.
- 8082번에서는 바인드 마운트로 index.html 수정 내용이 반영되는 것을 확인했다.
- diary-data 볼륨에 저장한 문장이 컨테이너 삭제 후에도 남는 것을 확인했다.

### 실행 기록
- [Docker 버전](docker-practice/version.txt)
- [Docker 환경 정보](docker-practice/info.txt)
- [컨테이너 목록](docker-practice/containers.txt)
- [웹 서버 로그](docker-practice/web-logs.txt)
- [자원 사용량](docker-practice/stats.txt)
- [바인드 마운트 설정](docker-practice/bind-mount.txt)
- [볼륨 데이터 확인](docker-practice/volume-result.txt)

## 웹페이지 실행 방법
Docker Desktop을 실행한 상태에서 터미널에 입력한다.

```
git clone https://github.com/doniryu/dev-workplace.git
cd dev-workplace
docker build -t my-web .
docker run -d --name diary-demo -p 8090:80 my-web
```

브라우저에서 http://localhost:8090 으로 접속한다.

실습을 마치면 아래 명령으로 중지하고 삭제한다.

```
docker stop diary-demo
docker rm diary-demo
```

## Docker 실행 확인
[hello-world 실행 결과](docker-practice/hello-world.txt)

아래는 localhost:8090에서 웹페이지가 실행된 화면이다.

![Docker 웹페이지 실행 화면](screenshots/docker-web.png)

## Git 설정 확인
[Git 사용자 정보와 기본 브랜치 확인 결과](git-practice/config.txt)

## Linux 권한 실습 재현 방법
Mac 터미널에서 다음 명령으로 Ubuntu를 실행한다.

```
docker run --rm -it ubuntu:24.04 bash
```

Ubuntu 안에서 다음 명령을 한 줄씩 실행한다.

```
mkdir -p /practice
cd /practice
touch sample.txt
chmod 755 /practice
chmod 644 sample.txt
ls -ld /practice sample.txt
chmod 700 /practice
chmod 600 sample.txt
ls -ld /practice sample.txt
chmod 755 /practice
chmod 644 sample.txt
ls -ld /practice sample.txt
exit
```

권한 표시가 폴더는 755 → 700 → 755,
파일은 644 → 600 → 644 순서로 바뀌는지 확인한다.

## 바인드 마운트 재현 방법
저장소 폴더에서 Docker Desktop이 실행된 상태로 진행한다.

```
docker build -t my-web .
docker run -d --name bind-demo -p 8092:80 -v "$PWD/index.html:/usr/share/nginx/html/index.html:ro" my-web
```

1. 브라우저에서 http://localhost:8092 에 접속한다.
2. 컴퓨터의 index.html에서 문장을 바꾸고 저장한다.
3. 브라우저를 새로고침하여 변경된 문장이 보이는지 확인한다.

컴퓨터의 파일을 컨테이너와 연결했으므로 이미지를 다시 만들지 않아도 변경이 반영된다.
아래 명령으로 실습용 컨테이너를 정리한다.

```
docker stop bind-demo
docker rm bind-demo
```

주의: 위 명령은 macOS의 zsh/bash 기준이다.
포트 8092를 다른 프로그램이 사용 중이면 다른 번호로 바꾼다.

## 볼륨 데이터 유지 확인 방법
Docker Desktop이 실행된 상태에서 진행한다.

```
docker volume create volume-demo-data
docker run --name volume-write-demo -v volume-demo-data:/data alpine sh -c 'echo "My diary is saved" > /data/diary.txt'
docker rm volume-write-demo
docker run --rm -v volume-demo-data:/data alpine cat /data/diary.txt
```

마지막 명령에서 다음 문장이 출력되는지 확인한다.

```
My diary is saved
```

데이터가 컨테이너 밖의 이름 있는 볼륨에 저장되므로,
처음 만든 컨테이너를 삭제해도 새 컨테이너에서 읽을 수 있다.

확인이 끝나면 아래 명령으로 실습용 볼륨을 삭제한다.
이 명령은 볼륨에 저장된 데이터도 삭제한다.

```
docker volume rm volume-demo-data
```

## 프로젝트 목표
터미널, Linux 권한, Docker, Git/GitHub를 활용하여
다른 사람도 따라 실행할 수 있는 개발 작업 환경을 구성한다.

## 추가 실습 실행 환경
- OS: macOS Sequoia 15.8.2
- 컴퓨터: Intel MacBook Pro
- 편집기: Visual Studio Code
- 셸: zsh / Ubuntu 컨테이너 내부 bash
- Git: 2.39.5 (Apple Git-154)
- Docker: 29.9.2
- Linux 실습 이미지: Ubuntu 24.04

[버전 및 이미지 목록 실제 출력](docker-practice/final-check.txt)

## 수행 체크리스트
- [x] 터미널 파일·폴더 조작
- [x] macOS 및 Linux 파일·디렉터리 권한 변경
- [x] Docker 설치 및 동작 확인
- [x] hello-world 및 Ubuntu 컨테이너 실행
- [x] 컨테이너 실행·중지·재시작
- [x] 컨테이너 목록·로그·자원 사용량 확인
- [x] Dockerfile로 커스텀 이미지 빌드
- [x] 포트 매핑 및 웹페이지 접속
- [x] 바인드 마운트로 파일 변경 반영
- [x] 컨테이너 삭제 후 볼륨 데이터 유지 확인
- [x] Git 설정 및 GitHub 업로드

## Dockerfile 구성과 목적
- FROM nginx:alpine: 웹 서버가 포함된 베이스 이미지를 사용한다.
- COPY: 기본 웹페이지를 직접 작성한 index.html로 교체한다.
- EXPOSE 80: 컨테이너에서 사용하는 웹 서버 포트를 명시한다.
- EXPOSE만으로 접속 포트가 열리지는 않으며, 실행할 때 -p로 연결한다.

## 실습에서 확인한 개념
- 이미지는 실행에 필요한 파일과 설정이고, 컨테이너는 이미지를 실행한 환경이다.
- 8080:80은 컴퓨터의 8080 포트를 컨테이너의 80 포트와 연결한다.
- 바인드 마운트는 컴퓨터의 파일을 컨테이너에 연결한다.
- 이름 있는 볼륨은 컨테이너와 별도로 데이터를 유지한다.
- Git은 변경 이력을 관리하고, GitHub는 저장소를 공유하는 서비스다.

## GitHub 원격 저장소 연결
제출 저장소: https://github.com/doniryu/dev-workplace
사용 브랜치: main

git remote -v로 내려받기(fetch)와 업로드(push)에 사용하는
원격 저장소 주소를 확인한다.

[원격 저장소 설정 실제 기록](git-practice/remote.txt)

## 포트 매핑과 네트워크 격리
컨테이너는 일반적으로 호스트와 분리된 네트워크 공간
(네트워크 네임스페이스)을 사용한다.
따라서 컨테이너의 80번 포트와 컴퓨터의 80번 포트는 서로 다르다.

-p 8080:80은 컴퓨터의 8080번 포트로 들어온 요청을
컨테이너의 80번 포트로 전달한다.
EXPOSE 80은 사용하는 포트를 명시하는 정보이며,
그 자체로 호스트에 포트를 공개하지 않는다.

## 절대 경로와 상대 경로
- 절대 경로: 현재 위치와 관계없이 파일 위치를 지정한다.
  예: /usr/share/nginx/html/index.html
- 상대 경로: 현재 작업 폴더를 기준으로 지정한다.
  예: index.html, docker-practice/version.txt
- 저장소 안의 문서 링크는 다른 컴퓨터에서도 사용할 수 있도록 상대 경로를 쓴다.
- 바인드 마운트에서는 호스트 파일의 위치를 명확히 하려고 절대 경로를 사용한다.
  macOS의 "$PWD/index.html"은 현재 폴더의 절대 경로를 이용한다.

## 권한 숫자를 읽는 규칙
권한은 소유자, 그룹, 기타 사용자 순서로 세 자리 숫자를 쓴다.
각 자리에서 r=4, w=2, x=1을 더한다.

- 7 = 4+2+1 = rwx
- 6 = 4+2 = rw-
- 5 = 4+1 = r-x
- 4 = r--

따라서 755는 rwxr-xr-x이고, 644는 rw-r--r--이다.
디렉터리의 r은 목록 읽기, w는 항목 생성·삭제,
x는 경로 통과와 내부 항목 접근에 관련된다.

## 포트 충돌 진단과 해결 절차
아래는 충돌이 발생했을 때 사용할 진단 절차이다.

### Windows PowerShell
8080번 포트를 사용하는 항목과 PID를 확인한다.

```
netstat -ano | findstr :8080
```

출력의 마지막 숫자가 PID이다. 해당 PID를 다음 명령의
1234 자리에 넣어 프로그램을 확인한다.

```
Get-Process -Id 1234
```

### macOS
8080번 포트에서 접속을 기다리는 프로세스를 확인한다.

```
lsof -nP -iTCP:8080 -sTCP:LISTEN
```

### 해결 방법
먼저 docker ps로 실행 중인 컨테이너의 포트도 확인한다.
내 실습용 컨테이너가 점유하고 있고 더 필요 없다면
docker stop 컨테이너이름으로 중지한다.
다른 프로그램이 사용 중이면 해당 프로그램의 용도를 확인하고,
실습에서는 호스트 포트를 다른 번호로 바꿀 수 있다.

예를 들어 Docker 실행이 가능한 환경에서는 다음처럼
8093번 포트로 실행한다.

```
docker run -d --name port-demo-8093 -p 8093:80 my-web
```

브라우저에서 http://localhost:8093 으로 접속한다.

## 저장소 파일과 폴더 역할
- Dockerfile: Nginx 기반 이미지에 직접 작성한 웹페이지를 넣는 빌드 설정
- index.html: 웹 서버가 제공하는 페이지
- history.txt: Windows 터미널 실습 명령 기록
- permission-practice/: macOS 권한 실습 파일과 결과
- linux-practice/: Ubuntu 권한 변경 결과
- docker-practice/: Docker 버전·환경·컨테이너·로그·볼륨 확인 결과
- git-practice/: Git 사용자 설정과 원격 저장소 확인 결과
- screenshots/: 실행 화면 증거

[이미지 목록과 버전 실제 출력](docker-practice/final-check.txt)
[컨테이너 목록 실제 출력](docker-practice/containers.txt)

## 이미지 빌드와 변경 반영 흐름
Dockerfile은 nginx:alpine을 기반으로 index.html을 이미지 안에 복사한다.
따라서 컴퓨터의 HTML만 수정해도 기존 이미지와 컨테이너가 자동으로 바뀌지는 않는다.

COPY 방식의 변경 반영 절차는 다음과 같다.
1. index.html 수정 및 저장
2. docker build -t my-web . 실행
3. 새 이미지로 새 컨테이너 생성
4. 브라우저에서 변경 내용 확인

바인드 마운트 방식은 호스트 파일을 직접 연결하므로
HTML을 저장하고 브라우저를 새로고침하면 변경을 확인할 수 있다.
바인드 마운트는 개발 중 파일 편집에 편리하고,
COPY 방식은 웹페이지를 이미지에 포함하여 전달하기 편리하다.

## 저장된 실제 결과 해설
아래 내용은 저장소의 실제 출력 파일을 확인하여 정리했다.

- docker-practice/final-check.txt:
  docker images 결과에 my-web:latest 이미지가 존재한다.
  이미지 존재 증거이며 빌드 과정 로그를 대신하지는 않는다.
- docker-practice/info.txt:
  Server 정보가 출력되어 Docker 데몬과 통신했음을 확인할 수 있다.
- docker-practice/containers.txt:
  my-web은 8080:80, my-web-8081은 8081:80,
  my-web-live는 8082:80으로 실행된 기록이 있다.
  ubuntu-practice는 bash 실행 후 Exited (0) 상태로 기록돼 있다.
- docker-practice/web-logs.txt:
  GET / 요청에 HTTP 200으로 응답한 실제 기록이 있다.
- docker-practice/bind-mount.txt:
  호스트의 index.html이 컨테이너의
  /usr/share/nginx/html/index.html에 읽기 전용으로 연결돼 있다.
- docker-practice/volume-result.txt:
  새 컨테이너에서 읽은 My diary is saved 문장이 저장돼 있다.

## 컨테이너 종료와 접속 방식의 차이
다음은 명령의 동작 원리를 정리한 내용이며,
별도 비교 실습의 실제 출력 기록은 아직 첨부하지 않았다.

- docker run -it ubuntu:24.04 bash:
  bash가 컨테이너의 주 프로세스이므로 exit로 bash를 끝내면 컨테이너도 종료된다.
- docker exec -it 컨테이너이름 bash:
  실행 중인 컨테이너에 추가 bash를 실행한다.
  이 bash에서 exit해도 기존 주 프로세스가 계속 실행 중이면 컨테이너는 유지된다.
- docker attach:
  컨테이너의 주 프로세스에 연결한다.
  Ctrl+P를 누른 뒤 Ctrl+Q를 누르면 프로세스를 종료하지 않고 연결에서 빠져나올 수 있다.
  
  