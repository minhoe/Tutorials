# Analytics environment setting guide on AWS

## 1. Launch AWS service

### 1.1 AMI 선택 
* Deep Learning AMI (Ubuntu) 를 선택(Tensorflow, Keras 등 ML tool들이 기본 설치되어 있는 Image)

### 1.2 인스턴스 유형 선택
* 작업의 특성에 따라 적절한 성능의 인스턴스를 선택함
* 참고 사항
- 'CPU optimized' : C5 Series
- 'GPU optimized' : P3 Series

### 1.3 인스턴스 구성
* 비용 절감 필요 시 '스팟 인스턴스 요청'을 선택함
- 주의 : '스팟 인스턴스'는 언제든지 회수(Shutdown)될 수 있으므로 사용 시 주의 필요

### 1.4 스토리지 추가
* 기본 제공되는 볼륨 외 추가 스토리지가 필요한 경우 추가한다. 
* '종료 시 추가'를 클릭하지 않으면 인스턴스가 종료된 이후에도 EBS에 데이터가 살아 남아 비용이 지속 청구됨
* 작업 내용은 완료 후 git으로 송부하는 방식으로 진행하는 경우 '종료 시 추가'를 클릭함(종료 시 모든 스토리지 초기화됨!)
* 그 외 별다른 설정 사항이 없으면 '검토 및 시작'을 눌러 완성한다.

### 1.5 키 페어 선택
* 발급 받은 '키 페어'를 선택한다. (다중 사용자의 경우 키 페어를 어떻게 하지?? 복사해서 주나??)

## 2. Connect to AWS 

### 2.1 EC2 대시보드 화면에서 인스턴스 상태 확인
* 인스턴스 리스트에서 조금 전 구성한 인스턴스의 상태가 'running'인 경우 접속이 가능한 상태임. 그 외 상태인 경우 추가 진단이 필요함

### 2.2 Public IP주소 확인
* 인스턴스를 클릭하면 아래 설명 탭이 나타나고, 'IPv4 퍼블릭 IP'를 확인할 수 있다.

### 2.3 Terminal 접속(MacOS 기준. WinOS는 별도 설명 필요)
* Terminal창을 열고 발급 받은 키 페어가 있는 곳으로 이동하여 아래 명령을 입력한다.
* 참고
- SSH가 작동하려면 키가 공개적으로 표시되지 않아야 합니다. 필요할 경우 이 명령을 사용합니다.
```bash
> chmod 400 hyundai_airlab_keypair.pem
```

* 퍼블릭 IP를 이용하여 인스턴스에 연결(중간에 yes/no를 물어보는 화면이 나오면 yes를 입력 후 엔터)
- 주의! Jupyter notebook을 실행할 목적이 아닌 일반 shell 작업을 진행할 경우에는 아래 명령어에서 8888:localhost:8888 를 제거 후 실행한다! 접속이 안 될 수 있음.
```bash
> ssh -i "hyundai_airlab_keypair.pem" –L 8888:localhost:8888 ubuntu@54.191.207.129
```


## 3. Git 설정
### 3.0 Git configuration
* Git을 AWS 내에서 처음 시작하기 전에 아래 정보를 설정한다
```bash
> git config --global user.name "minhoe"
> git config --global user.email "mhoe.hur@gmail.com"
```
* 설정된 사항은 아래 명령을 통해 확인한다.
```bash
> git config --list
```

### 3.1 기존 repo를 가져오는 경우
* 아래 명령을 입력 후 clone 된 폴더 내에서 작업을 실시한다.
```bash
> cd ~
> mkdir git_repos
> cd git_repos
> git clone https://github.com/minhoe/hello-world.git
> cd hello-world
# create a new branch to store any new changes
> git branch my-branch

# switch to that branch (line of development)
> git checkout my-branch

# Chech the git status
> git status

# Do some programming here!

# Reflect changes from the remort
> git add *

# take a snapshot of the staging area (anything that's been added)
> git commit -m "my snapshot"

# push changes to github
> git push --set-upstream origin my-branch

# 기존의 Github에 있었던 파일을 수정 후 올린 경우 Pull request가 필요하며 이는 github 내에서 진행한다. Local에서 신규로 생성한 파일이라면 Pull request는 필요 없이 종료된다.
```

### 3.2 신규 repo를 생성하는 경우

* Github 내에서 신규 repo를 생성한다.
* 로컬에서 다음을 진행한다.

```bash
# (주의! Do not initialize the repository with a README, .gitignore or License.)

# create a new directory, and initialize it with git-specific functions
> git init hello-world3

# change into the `hello-world3` directory
> cd hello-world3

# create the first file in the project
> touch README.md

# git isn't aware of the file, stage it
> git add README.md

# take a snapshot of the staging area
> git commit -m "add README to initial commit"

# provide the path for the repository you created on github
> git remote add origin https://github.com/minhoe/hello-world3.git

# push changes to github
> git push --set-upstream origin master
```

### 3.3 

## 4. Programming with Jupyter notebook

### 4.1 Launch Jupyter notebook
* Terminal에서 아래 명령어를 실행한다
```bash
> jupyter notebook
```

* 이후 나오는 아래 화면을 캡쳐 후 chrome에 붙여넣기를 한다.
 (주의! 기존에 로컬 또는 다른 원격의 jupyter notebook이 실행되고 있으면 기존의 notebook으로 접속이 되므로 기존 notebook은 전부 닫도록 한다.)
* 예시(token은 화면에 나타나는 것을 활용함) :
```bash
 http://localhost:8888/?token=36680994be1e766c5c207c47ace16303169a8d381f609e05&token=36680994be1e766c5c207c47ace16303169a8d381f609e05
```

## 5. Programming with Pycharm
* Pycharm Community 버전에서는 Remote server를 이용한 개발이 불가하며, Professional 버전(유료!)에서만 가능하다. 
* 정말 필요하다면 유료 버전을 구해보도록(DIY) 하자.


## 6. Save source codes to github

------
EC2에서 Docker를 어떻게 쓸까... (고민 중)
### 1. Install Docker 
Visit Docker homepage and download installation program

### 2. Download Anaconda3 docker image from the web(@Terminal)
sudo docker run -it -p 8888:8888 continuumio/anaconda3 /bin/bash

### 3. 
jupyter notebook

