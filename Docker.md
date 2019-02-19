# Docker Tutorials for Mac

### Docker 상태 확인
Docker가 정상적으로 설치 되었는지 확인하기 위해서는 다음 명령어를 입력한다.
이 때 Server와 Client 정보가 Error 정보 없이 나타나면 정상이다.
```bash
> docker version
```

### Docker Login
Docker image를 Push or pull하기 위해서는 Docker hub에 로그인을 해야 한다. (계정 없는 경우 Docker hub에서 가입!)
```bash
> docker login
```

### Run container(Ubuntu:16.04)
ubuntu 16.04를 실행한다. 만일 기존에 Pull해 놓은 이미지가 없다면 새로 다운로드 부터 시작하게 된다.

```bash
> docker run ubuntu:16.04
```

실행 후 바로 프롬프트 상태로 전환되는 것을 알 수 있다. 이는 컨테이너는 정상적으로 실행됐지만 뭘 하라고 명령어를 전달하지 않았기 때문에 컨테이너는 생성되자마자 종료된다. 컨테이너는 프로세스이기 때문에 실행중인 프로세스가 없으면 컨테이너는 종료된다고 함!
따라서 컨테이너 내에서 실행을 위해서는 다음의 명령을 실행한다.

```bash
> docker run --rm -it ubuntu:16.04 /bin/bash
```

비고
- '--rm' : 프로세스 종료 후 자동으로 컨테이너 자동 삭제
- '-it' : bash shell 실행 및 키보드 입력 목적

만일 컨테이너가 호스트 디렉토리에 접근이 필요한 경우(예: 컨테이너와 호스트 PC/서버 간 데이터를 주고 받아야 하는 경우) 아래 -v 옵션을 추가하여 입력한다.
서로 연결할 경로를 명시하여 컨테이너 내에서도 호스트에 접근이 가능하다.

```bash
> docker run -v /Users/minhoe/DockerDrive:/DockerDrive -it miniconda3:v2r2 /bin/bash
```

비고
- '-v' : 호스트 PC/서버의 볼륨을 컨테이너에 추가함. {호스트 경로}:{컨테이너 내 경로}


컨테이너를 종료하고자 할 때는 우선 컨테이너에서 빠져 나온다.
```bash
(docker) > exit
```

그리고 변동 사항을 컨테이너 이미지에 저장하고자 할 때는 다음을 입력한다.

```bash
# 가장 최근에 빠져나온 컨테이너 이름 확인
> docker ps -a
# 컨테이너 이미지 저장
> docker commit -m "Add opencv" epic_cocks miniconda3:v2r3
# 저장된 이미지 확인
> docker images
```



### Run container(Redis - Remote Dictionary Server)
Redis는 In-memory에 상주하는 Key-value 구조를 갖는 database이다(Port 6379로 통신).
Redis 컨테이너는 다음과 같은 명령으로 실행한다.

```bash
> docker run -d -p 1234:6379 redis
```

비고
- '-d' : detached mode(백그라운드 모드)로 실행(Redis 내부로 들어가는 것을 방지)
- '-p' : 컨테이너 포트를 호스트 포트로 연결

```bash
docker run -d -p 1234:6379 redis

# redis test
$ telnet localhost 1234
set mykey hello
+OK
get mykey
$5
hello
```


### Run Mysql
```bash
docker run -d -p 3306:3306 \
  -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
  --name mysql \
  -v /my/own/datadir:/var/lib/mysql \ # <- volume mount
  mysql:5.7
```

비고
- '-v' : 컨테이너 삭제 이후에도 하드 볼륨에 저장하여 데이터 유실을 방지함!!

Image를 pull한 이후에 mysql 실행은 다음을 입력한다.

```bash
> docker exec -it heuristic_ellis /bin/bash

$ mysql -uroot

mysql> show databases;
mysql> quit
```

여기서 heuristic_ellis는 컨테이너의 이름이다(컨테이너 생성 시 docker가 자동으로 생성해 준 이름)


### Docker 컨테이너 목록 확인하기

```bash
> docker ps # 현재 실행 중인 컨테이너들
> docker ps -a # 전체 컨테이너 리스트(종료된 컨테이너까지 모두!)
```

### 컨테이너 종료
```bash
> docker stop ${TENSORFLOW_CONTAINER_ID}
> docker ps
```

### 컨테이너 제거하기
```bash
> docker ps -a
> docker rm ${CONTAINER_ID}
> docker ps -a # Check the result
```


### 이미지 목록 확인하기
```bash
> docker images
```

### 이미지 다운로드 하기
```bash
> docker pull ubuntu:14.04
```
기존 이미지가 있다면 해당 버전 내에서 최신의 버전으로 업그레이드함

### 이미지 삭제하기
```bash
> docker images # get image ID
> docker rmi ${TENSORFLOW_IMAGE_ID}
```

### 컨테이너 로그 보기
```bash
> docker ps
> docker logs ${WORDPRESS_CONTAINER_ID}
```


### 컨테이너 실행하기
```bash
> 
```
