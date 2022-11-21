# ⭕ Linux 기초

🏷 태그: Ops, 클라우드OS, 클라우드인프라  
📆 학습일: 11/18/2022

# 목차
1. 리눅스 설치
2. 실습
3. 퀴즈

## 1. 리눅스 설치


### 1.1 VirtualBox 및 Vagrant 설치

먼저 Hypervisor 인 버추얼 박스를 설치하기 전,

계층화된 가상 구조에 더 편리하고 자동화를 위한 추가 프로그램이 필요하다.

그것을 **Vagrant** 라고 한다.

- VirtualBox를 명령어(CLI)로 제어하는 프로그램(App.)
    
    vagrant를 사용하면 명령어 두줄로 간단히 vm 설치, 생성이 가능하다.
    

![image](https://user-images.githubusercontent.com/118426836/202899206-99b91874-59c9-4d01-9eeb-7b5bd15fa2bb.png)
> 계층화 layerd 된 가상 네트워크, 가상 계층 구조 모델링  

![image](https://user-images.githubusercontent.com/118426836/202899245-545f53f1-dd04-4890-a16f-923c70af2f78.png)
> 버츄얼박스와 함께 구동될 vagrant

1. **VirtualBox 설치**
    - [Downloads – Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads) 접속
    - 버전에 맞는 파일 다운로드 및 설치
    - install 진행이 안 될 때 [지원되는 최신 Visual C++ 재배포 가능 패키지 다운로드 | Microsoft Learn](https://answers.microsoft.com/en-us/windows/forum/all/microsoft-visual-c-redistributable-2019-x64/a2af45bb-85ce-4ab0-8318-e7be90b17725) 에서 Visual C++x64 다운로드 후 재설치
2. **Vagrant 설치**
    - [Downloads | Vagrant by HashiCorp](https://www.vagrantup.com/downloads) 접속
    - 버전에 맞는 파일 다운로드 및 설치

### 1.2 VM 생성 및 CentOS 설치

VirtualBox와 Vagrant가 설치되었으면, VM을 생성하고 그 위에 올릴 운영체제 CentOS/7 을 설치한다.
![image](https://user-images.githubusercontent.com/118426836/202899304-0addd199-ca46-49d3-b4cd-6d6f707742e1.png)

1. **Vagrant 로 VM 생성**
    1. **디렉토리 생성**
    2. **VagrantFile 생성**
        
        : VM의 세부 설정을 정의한다. (네트워크, 용량, 호트이름 등등) 
        
        ```
        vagrant init -m "cenetos/7" : VagrantFile 생성
        ```
        
2. **OS 이미지 다운로드 및 VM 생성, 설치**

        
        vagrant up : VagrantFile 통한 가상머신 생성
        

1. **VM SSH 접속 : 서버 접속**
    1. 가상 머신 접속 확인
        
        현재 vm프로젝트가 생성하고 실행 중인 서버에 접속됨
        

### 1.3 기본적인 vagrant 명령어 정리

    
    # 가상머신 기동
    vagrant up
    # 가상머신 상태 확인
    vagrant status
    # 가상머신 중단
    vagrant status
    # 가상머신 제거
    vagrant destroy
    # 가상머신 접속
    vagrant ssh
    # 접속 상태에서 다른 가상머신 운영상태 및 id 확인
    vagrant global-status
    # 접속 상태에서 다른 가상머신 중단
    vagrant halt <id>
    # 서버에서 exit
    exit
    

## 2. 실습


### 2.1 VM 서버이름 변경

**VagrantFile 을 편집한다**

    - ssh 서버 접속 후, 호스트명 확인

    
    vagrant ssh
    hostname

    #VagrantFile 편집
    config.vm.hostname=""

    eg.
    **config.vm.hostname = "myhost3.bitcamp"** 
   

### 2.2 VM 생성 및 설정

1. centos vm 설정 (virtual box)
2. centos vm 실행
3. 호스트명 변경 > “myhost3.bitcamp”

### 2.3 VM 추가 생성 및 git 개인 페이지 변경

1. **centos5 vm 생성**
    1. vm-projects에 centos5 디렉토리 생성
    2. VagrantFile 생성
    3. log 붙여넣기 & 호스트이름 설정
    4. VM 실행
2. **centos5 vm 접속**
3. **git 개인 페이지 변경**
    1. git 설치
    2. nano 에디터 설치
    3. git config 의 name & email 설정
    4. [README.md](http://README.md) 편집
    5. git commit & push
    
    ✨ nano 에디터
    
    ```
    # 서버 접속 상태에서
    sudo yum install git -y
    # complete 후 버전 확인
    git --version
    # print working directory : 현재 디렉토리를 알려주는 명령어
    pwd
    
    mkdir git
    cd git
    git clone <URL>
    
    sudo yum install nano editor -y
    cd yunol.github.io
    nano README.md
    
    # Your Name 을 변경해주세요
    git config --global user.name "Your Name"
    # user@email.com 을 변경해주세요
    git confit --global user.email "user@email.com"
    git add -A
    git commit -m ""
    git push
    ```
    

    ```
    # 리포지토리 clone  
    git clone <URL>
    # Your Name 을 변경해주세요
    git config --global user.name "Your Name"
    # user@email.com 을 변경해주세요
    git confit --global user.email "user@email.com"
    # 커밋 파일 추가
    git add -A
    # 커밋 및 인덱스 추가
    git commit -m “message”
    # push
    git push origin main

    vagrant init -m "cenetos/7" : VagrantFile 생성
    vagrant up : Vagrantfile 을 통한 가상 머신 생성

    dir : 로 확인

## 3. 퀴즈 

- 11.21.월 오전  
- 작업 내용:

    1. VirtualBox와 Vagrant 도구를 이용하여 로컬에 리눅스 가상 머신을 3개 생성하시오.
    2. 각 가상 머신의 이름을 host1.bitcamp, host2.bitcamp, host3.bitcamp 로 설정하시오.
    3. 각 가상 머신에 "https://github.com/eomjinyoung/bitcamp-study" 저장소를 복제하시오.

    복제한 저장소의 위치: ~/git/bitcamp-study

    ```
    # 디렉토리 생성
    # Vagrantfile 생성 > 서버이름 함께 수정 : log 붙여넣기
    vagrant init -m ""

    vagrant up

    # 서버 접속
    vagrant ssh

    # 서버 이름 확인
    hostname

    # git 설치 및 복제 ~/git/bitcamp-study 에 만드는게 중요
    mkdir git
    cd git
    sudo yum install git -y
    git clone https://github.com/eomjinyoung/bitcamp-study

    # 확인
    git ssh
    hostname
    cd bitcamp-study
    ls : docs README. 확인 가능
    pwd : /home/vagrant/git/bitcamp-study
    ```
