# 💻 git 사용법

🏷 태그: Ops, 클라우드OS, 클라우드인프라  
📆 학습일: 11/21/2022

## 1. Vagrantfile 이해하기


~/vm-projects

	centos test/Vagrantfile

	centos test2/Vagrantfile

	centos test3/Vagrantfile

> VM생성프로젝트 / VM설정정보파일

⬇

“vagrant up”

⬇

~/Virtualbox VMs/

	centostest_default…/….vmdk(버츄얼머신디스크)

	centostest2_default…/….vmdk(버츄얼머신디스크)

	centostest3_default…/….vmdk(버츄얼머신디스크)

> VM의폴더 / VM의파일

  
  
  
- **Vagrantfile = project**
    
    **VMs file = VM 이라는 개념 이해할 것**
    
 
    💡 **vagrant 프로젝트** : ‘가상머신을 만들고 초기화시키는’ 설정 정보가 있는 프로젝트
    
	    프로젝트를 지웠다고 vm이 지워지는게 아니다

	    eg. 프로젝트 파일을 지워도 VB, VMs 에 존재해

	    CLI 에서 ‘vagrant destroy <id>’ 해도 프로젝트 폴더를 찾기 때문에 명령어가 먹히지 않아

	    GUI 삭제 후 VMs 확인 하면 VMs 삭제되어있는 것 확인 가능

	    🚩or VMs 폴더에서 직접 삭제

	    🚩but 프로젝트 파일은 수작업으로 지워줘야!
    
    
    
    ```
    # 물론 해당 디렉토리 내에서 명령어 작성 할 것
    
    C:\Users\bitcamp>cd vm-projects
    C:\Users\bitcamp\vm-projects>cd cetos2
    C:\Users\bitcamp\vm-projects\cetos2>vagrant destroy
        default: Are you sure you want to destroy the 'default' VM? [y/N] y
    ==> default: Discarding saved state of VM...
    ==> default: Destroying VM and associated drives...
    C:\Users\bitcamp\vm-projects\cetos2>cd..
    ```
    

## 2. VCS : Version Control System, 버전관리시스템


### 2.1 VCS 개요

- 파일 변화를 시간에 따라 기록했다 특정 시점의 버전을 다시 꺼내올 수 있는 시스템
- 파일별로 이전 상태로 되돌리거나 프로젝트 통째로 이전 버젼으로 돌릴 수 있다.
- 시간에 따라 수정 내용을 비교할 수 있다.
- 누가 언제, 어떻게 문제를 일으켰는지 추적할 수 있다.

### 2.2 CVS vs SVN vs GIT

**개요** 

- 로컬 버전 관리 시스템
    - 간단한 데이터베이스를 이용하여 파일에서 변경되는 부분을 관리
    - eg. RCS (Revision Control System)
- 중앙집중식 버전 관리
    - 파일의 마지막 스냅샷을 받는다 (checkout)
- 분산 버전 관리 시스템

1. **CVS : Concurrent Versions System**
    
    서버 리포에서 로컬로 나오는 걸 checkout (각 파일의 **마지막 스냅샷**을 checkout)
    반대는 check in = commit 
    
    > snapshot 스냅샷 : 특정 시점의 파일 버전을 기록한 것
    > 
    > 
    > eg. 무대위에 올릴, 내릴 staging 것을 찰칵 찍는다~!
    > 


	💡 check in = commit   
	1. 최신 버전의 파일을 가져온다.
	2. 파일을 통째로 서버에 전송한다.

서버 리포에는 프로젝트파일+ **변경내역** 까지 포함되어있다.
  
서버에서 변경 내용을 관리하는 **중앙집중방식**

- 서버에 문제가 발생하면 변경 내역을 모두 잃는다.
- 파일을 통째로 주고받으면 네트워크의 부하 (overhead) 발생
    
    변경 내용 외 기존 내용까지 전송하기 때문 : 네트워크 과다 사용, 네트워크 오버헤드
    
</aside>

1. **SVN : Subversion**
    
    cvs 와 동일하게 중앙집중방식 이지만,
    
    **파일의 변경 부분만 서버로 전송한다.** (각 파일의 **마지막 스냅샷**을 **checkout**)
    
    따라서, cvs보다 오버헤드가 적다.
    
    하지만, 서버에 문제 발생시에는 동일한 단점이 있다.
    

1. **GIT**
    
    위 두가지를 모두 극복
    
    서버 리포를 그대로 로컬로 **clone**
    
    **로컬 리포에** 프로젝트파일+ **변경내역** 까지 포함
    
    - **저장소를 클라이언트 쪽에 분산 복제 : 안전성이 높다**
        
        서버에 문제 발생하더라도 클라이언트에 분산 복제된 리포지토리를 사용하여 원상복구 가능
        
        push & pull
        
    - **commit & push & pull : 네트워크 오버헤드가 적다**
    
    ```bash
    # 변경 후 commit
    git commit : 서버에 업로드가 아니라 로컬 리포지토리에 저장 
    # 공유가 필요할 때
    git push : 서버로
    git pull : 로컬로
    ```
    

## 3. git 사용법

---

### 3.1 Git의 파일 상태

modified : 파일이 변경되었지만 아직 로컬 db에 저장되지 않음 > 수정했으나 add 하지 않은 상태

committed : 로컬 db에 안전히 저장. 바뀐 것 없이 저장된 상태 > add 완료 후 커밋

staged : 로컬 db에 저장할 파일임을 표시했다 > add 한 상태 

: 스테이징 되었으니 스냅샷을 찍을 수 있다. 무대에 올라왔으니 사진 찍어줄게!

        다음 커밋할 때 staged로 표시된파일의 변경 내용이 저장될 것이다.

### 3.2 Git 프로젝트의 단계 : 3단계

<aside>
💡 파일 탐색기 > git > bitcamp-study  
	
**.git** 에 변경된 내용들이 있다 = 로컬 저장소 = git 이 관리하는 폴더 : 직접 사용자가 손대면 안돼!

**docs**

**.gitignore**

**README.md**

> 저장소에서 꺼낸파일 및 디렉토리 = 작업디렉토리 “워킹 디렉토리”
> 

	commit : .git 으로

	.git 과 워킹 디렉토리 사이에서 커밋한다!


### 💥3.3 Git 파일의 상태 변화 : 오늘의 핵심

![Untitled](11%2021%20%E1%84%8B%E1%85%AF%E1%86%AF%20595de4f0cfdb4d89a101e616321572d1/Untitled.png)

- untracked : 저장소에 없던 파일, 아직 추적 되지 않은, 한번도 백업 되지 않았다.
- unmodified : 저장소에 들어있는 상태 그대로인 상태
- modified : 파일이 수정된 상태, add 가 필요한 상황
- staged : 백업 대상이 된 상태, **git add 되어** staging area에 snapshot을 남길 수 있는 = 백업이 준비된 상태
- committed : **git commit** 되어 백업된 상태, staged 된 파일들만 백업된다.

<aside>
💡 main = master
리포 저장소는 변경 내역을 관리하는 기본 “트랙”을 가지고 있는데 이것이 “main”

</aside>

## 4. 실습 & Git 명령어

---

### 4.1 git init : 로컬에 깃 저장소 만들기

```bash
# 현재 디렉토리 위치 출력
pwd
# 리스트 불러와
ls

# ~/git/bitcamp-ncp : git 저장소로 만들기
mkdir bitcamp-ncp
cd bitcamp-ncp
git init 

# 생성 확인
ls -al
```

### 4.2 git config : 사용자 이름 및 이메일 설정 ‘환경 설정’

```bash
- git의 사용 환경을 설정한다.
- /etc/gitconfig 설정 파일
  - 시스템의 모든 사용자와 모든 저장소에 적용되는 설정.
  - `git config --system` 옵션으로 이 파일을 읽고 쓴다.
  - Windows OS의 경로 - C:/ProgramData/Git/config
- ~/.gitconfig, ~/.config/git/config 설정 파일
  - 특정 사용자만 적용되는 설정.
  - `git config --global` 옵션으로 이 파일을 읽고 쓴다.
  - Windows OS의 경로 - C:/Users/사용자홈/.gitconfig
- .git/config
  - 특정 저장소에만 적용되는 설정.
  - `git config` 옵션을 지정하지 않으면 이 파일을 읽고 쓸 수 있다.

	예1) 사용자 이름 설정하기
	$ git config --global user.name "eomjinyoung"
	$ git config --global user.email "jinyoung.eom@gmail.com"

	예2) 기본 텍스트 편집기 설정하기
	$ git config --global core.editor emacs

	예3) 설정 확인하기
	$ git config -l
	$ git config --list

	예4) 특정 값 확인하기
	$ git config user.name

```

### 4.3 .gitignore 파일

**git 저장소에 보관하지 않을 대상을 지정한다.**

도구를 실행할 때 마다 자동 생성되는 파일 및 폴더 eg) .class, .exe, bin/, build/ 등

<aside>
💡 How to make .gitignore

- 기존 프로젝트 저장소에 설정된 파일을 가져와서 편집하는 방법
- .gitignore  파일을 자동 생성해주는 사이트를 이용하는 방법
    
    > gitignore.io
    > 
    > 
    > eg. windows macOS linux gradle java visualstudiocode eclipse
    > 
    > 다만 우리는 뭘 만들지 말아야 할지… 모르잖아
    > 
    > 기존 회사 프로젝트의 .gitignore 를 복붙해라
    > 
</aside>

```bash
vi gitignore

# 입력모드
a 
# 명령모드
esc
# 저장
:w 
# 나가기
:q 

# ???????
cat .gitignore

# 나노에디터 설치
sudo yum install nano -y

# .gitignore 설정
nano .gitignore
붙여넣기!!

```

### 4.4 git 파일 상태변화 이해하는 실습 : add/commit/status

```bash
[vagrant@host1 bitcamp-ncp]$ git status --short
?? .gitignore
?? a.txt
[vagrant@host1 bitcamp-ncp]$ git add .gitignore
[vagrant@host1 bitcamp-ncp]$ git status --short
A  .gitignore    A : staging area에 등록 되었다
?? a.txt         ?? : untracked
```

```bash
[vagrant@host1 bitcamp-ncp]$ nano b.txt       nano 에디터로 b.txt 생성 : untracked
[vagrant@host1 bitcamp-ncp]$ git status --short
?? a.txt   앞자리는 staging area
?? b.txt   뒷자리는 working directory
[vagrant@host1 bitcamp-ncp]$ git add a.txt      untracked 된 파일 stging area 에 올리기
[vagrant@host1 bitcamp-ncp]$ git status --short
A  a.txt                     A : staging area에 등록 되었다
?? b.txt                     ?? : 여전히 untracked
[vagrant@host1 bitcamp-ncp]$ git commit -m "2"
[master a8426f5] 2
 1 file changed, 2 insertions(+)
 create mode 100644 a.txt
[vagrant@host1 bitcamp-ncp]$ git status --short          b.txt는 여전히 untracked 상태이니 스냅샷이 남지 않음
?? b.txt
[vagrant@host1 bitcamp-ncp]$

여기서 
nano a.text 
접속해서 수정 하면 : a.txt 버젼 2로 변경됐잖아
git status --short 하면
_M : modified 변경되었다, 아직 서버에 저장되지 않았다
그럼 백업해야지! 

[vagrant@host1 bitcamp-ncp]$ nano a.txt         staged된 a.txt 를 다시 수정해보자
[vagrant@host1 bitcamp-ncp]$ git status --short
 M a.txt                                       워킹디렉토리에서 modified된 상태
?? b.txt
[vagrant@host1 bitcamp-ncp]$ git add b.txt
[vagrant@host1 bitcamp-ncp]$ git status --short
 M a.txt
A  b.txt    현 상태에서 커밋하면 워킹에서 M상태인 a는 스냅샷이 남지않는다 > staged 되지 않음
[vagrant@host1 bitcamp-ncp]$ git commit -m "3"
[master debe282] 3
 1 file changed, 1 insertion(+)
 create mode 100644 b.txt
[vagrant@host1 bitcamp-ncp]$ git status --short
 M a.txt          M상태인 a는 그대로 남아있고, b는 사라짐
[vagrant@host1 bitcamp-ncp]$ nano b.txt
[vagrant@host1 bitcamp-ncp]$ git status --short
 M a.txt
 M b.txt
[vagrant@host1 bitcamp-ncp]$ git add a.txt
[vagrant@host1 bitcamp-ncp]$ git status --short
M  a.txt   add 했으니 staged 상태
 M b.txt
[vagrant@host1 bitcamp-ncp]$ git commit -m "4"
[master dcb1719] 4
 1 file changed, 2 insertions(+)
[vagrant@host1 bitcamp-ncp]$ git status --short
 M b.txt    a.txt는 커밋 완료, 편집중이지 않으니 a 사라짐
[vagrant@host1 bitcamp-ncp]$ git add b.txt
[vagrant@host1 bitcamp-ncp]$ git status --short
M  b.txt
[vagrant@host1 bitcamp-ncp]$ nano b.txt
[vagrant@host1 bitcamp-ncp]$ git status --short
MM b.txt        
[vagrant@host1 bitcamp-ncp]$ git commit -m "5"
[master 493c125] 5
 1 file changed, 1 insertion(+)
[vagrant@host1 bitcamp-ncp]$ git status --short
 M b.txt
[vagrant@host1 bitcamp-ncp]$ git commit -m "6"
# On branch master
# Changes not staged for commit:          
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       modified:   b.txt
  스테이즈드 된게 없으니 스냅샷을 찍을 수 없다. add 먼저! = 무대에 먼저 올릴 것 staged
no changes added to commit (use "git add" and/or "git commit -a")
[vagrant@host1 bitcamp-ncp]$ git add b.txt
[vagrant@host1 bitcamp-ncp]$ git status --short
M  b.txt
[vagrant@host1 bitcamp-ncp]$ git commit -m "6"
[master dd9dd66] 6
 1 file changed, 1 insertion(+), 1 deletion(-)
[vagrant@host1 bitcamp-ncp]$ git status --short   
[vagrant@host1 bitcamp-ncp]$        물론 아무것도 없어, 6번 커밋을 통해 b.txt가 3이 되었다.
```

### 4.5 git log : 저장소의 변경 내역 조회

```bash
# 저장소의 변경 내역 조회 / GUI는 Soucetree 많이 씀

[vagrant@host1 bitcamp-ncp]$ git log     최근 것 부터 조회됨
commit dd9dd668d205936da3a93856613b83cd576bc2a9     커밋 체크섬 : 해시 알고리즘을 통해 지정된 해시값
Author: yun5ol <yunsol2095@gmail.com>    커밋한 사람의 이름과 이메일
Date:   Mon Nov 21 06:00:11 2022 +0000   커밋한 날짜 > 영국 시간 기준 +9시 필요

    6    커밋 때 인덱스한 내용

commit 493c1254ff6cad3ffe74878f8c344b5056b4297a
Author: yun5ol <yunsol2095@gmail.com>
Date:   Mon Nov 21 05:56:06 2022 +0000

    5

commit dcb17193c4b23c20ca9bed96af2e62a7c57d3d17
Author: yun5ol <yunsol2095@gmail.com>
Date:   Mon Nov 21 05:49:26 2022 +0000

    4

commit debe2826a5ff66f89f4e780d23c018316d13c533
Author: yun5ol <yunsol2095@gmail.com>
Date:   Mon Nov 21 05:44:45 2022 +0000

    3

commit a8426f5e908c91d55ee534c321f384883db6e83a
Author: yun5ol <yunsol2095@gmail.com>
Date:   Mon Nov 21 05:39:32 2022 +0000

    2

commit 04bbdb53058bded3736f18a5f3338a99d729ae53
Author: yun5ol <yunsol2095@gmail.com>
Date:   Mon Nov 21 05:36:31 2022 +0000

    1
[vagrant@host1 bitcamp-ncp]$ git log -p -2
commit dd9dd668d205936da3a93856613b83cd576bc2a9
Author: yun5ol <yunsol2095@gmail.com>
Date:   Mon Nov 21 06:00:11 2022 +0000

    6

diff --git a/b.txt b/b.txt
index 4f142ee..3e4f154 100644
--- a/b.txt
+++ b/b.txt
@@ -1,2 +1,2 @@
-1111
+33331111
 2222

commit 493c1254ff6cad3ffe74878f8c344b5056b4297a
Author: yun5ol <yunsol2095@gmail.com>
Date:   Mon Nov 21 05:56:06 2022 +0000

    5

diff --git a/b.txt b/b.txt
index 5f2f16b..4f142ee 100644
--- a/b.txt
+++ b/b.txt
@@ -1 +1,2 @@
 1111
+2222
[vagrant@host1 bitcamp-ncp]$ git log --oneline
dd9dd66 6
493c125 5
dcb1719 4
debe282 3
a8426f5 2
04bbdb5 1
[vagrant@host1 bitcamp-ncp]$ git log --oneline --graph --all
* dd9dd66 6
* 493c125 5
* dcb1719 4
* debe282 3
* a8426f5 2
* 04bbdb5 1

**명령어 재정리**
# ?????
git log -p -2
# 커밋 정보 한번에 조회
git log --oneline
# ?????
git log --oneline --graph --all
```

📌 commit hash 값 이해하기  = 데이터 id = 디지털 지문

> **데이터에 아이디를 부여하기 위한 개념**
> 
> 
> 각 파일의 변경 내용을 hash 알고리즘 (계산) 에 따라 연산을 수행하여 나온 결과값 = hash code
> 
>  hash 알고리즘 : 데이터를 입력 받아 해시값을 return 하는 수학 공식
> 
> hash code 는 데이터 크기에 상관 없이 256bit, 512bit, 1224bit 등의 정수 값이다.
> 

디지털 지문 사용 예 2가지

- 데이터 공유 사이트
- 파일 검증

### 4.6 git remote & pull & push & branch

**로컬 저장소에 연결된 원격 저장소를 확인하거나 추가한다.**

git clone 은 한 리포지만 가능하나, remote 로 멀티 연결 가능

(서버에서 만들고 깃클론이 가장 심플해!)

로컬 저장소에 있는 걸 서버에 업로드 해야하며 > 자동생성은 없다

```bash
[vagrant@host1 bitcamp-ncp]$ git remote   원격 저장소 이름알아내기 / 서버에 연결된 적이 없으니 안 나와
[vagrant@host1 bitcamp-ncp]$ git remote add origin https://github.com/yun5ol/bitcamp-ncp bitcamp-ncp 리포지토리 만들고 로컬과 연결하겠다. 서버이름은 origin 으로 하겠다
[vagrant@host1 bitcamp-ncp]$ git remote
origin
[vagrant@host1 bitcamp-ncp]$ git remote show origin
* remote origin
  Fetch URL: https://github.com/yun5ol/bitcamp-ncp
  Push  URL: https://github.com/yun5ol/bitcamp-ncp
  HEAD branch: main
  Remote branch:
    main new (next fetch will store in remotes/origin)
첫 pull 할 때 origin/main 연결 필요
클론이 아니니깐 정확히 지정이 필요
머지할게 있으면 이렇게 창이 뜬다
[vagrant@host1 bitcamp-ncp]$ git pull
warning: no common commits
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/yun5ol/bitcamp-ncp
 * [new branch]      main       -> origin/main
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> master

[vagrant@host1 bitcamp-ncp]$ git pull origin main   최초 1회 연결 필요 / 로컬 이름이 main이 아니라 master인 상황

**merge 화면에서 esc > :wq**

# branch 이름 변경
[vagrant@host1 bitcamp-ncp]$ git branch
* master
[vagrant@host1 bitcamp-ncp]$ git branch -m main
[vagrant@host1 bitcamp-ncp]$ git branch
* main
[vagrant@host1 bitcamp-ncp]$ git push --set-upstream origin main
Username for 'https://github.com': yun5ol
Password for 'https://yun5ol@github.com':
Counting objects: 21, done.
Compressing objects: 100% (14/14), done.
Writing objects: 100% (20/20), 3.14 KiB | 0 bytes/s, done.
Total 20 (delta 4), reused 0 (delta 0)
remote: Resolving deltas: 100% (4/4), done.
To https://github.com/yun5ol/bitcamp-ncp
   701d0c1..3e89afe  main -> main
Branch main set up to track remote branch main from origin.
```

## 5. 과제 : 22일 아침까지

로컬 git 저장소를 만들고 [github.com](http://github.com) 개인 저장소와 연결하라

작업내용: (host1 리눅스 VM에서 작업을 수행한다.)

1. 다음의 경로에 로컬 깃 저장소를 생성한다.
    
    ~/git/bitcamp-ncp2/
    
2. 다음의 테스트 파일을 생성하고 로컬 저장소에 커밋한다.
    
    ~/git/bitcamp-ncp2/a.txt
    
    a.txt 파일의 내용을 아무거나 입력한다.
    
3. github.com의 개인 계정에 bitcamp-ncp2 이름으로 저장소를 생성한다.
4. 로컬 깃 저장소와 원격 깃 저장소를 연결한다.
5. 로컬 깃 저장소의 내용을 원격 저장소에 push 한다.

과제 제출시 URL 넣기

```bash
# host 1 에서

cd vm-projects
cd centos test
vagrant ssh

$ nano a.txt
$ git init
$ git add a.txt
$ git commint -m "1"
$ git remote add origin URL
$ git remote
$ git remote show origin
$ git pull (origin main)
$ git branch
$ git branch -m main
$ git branch
$ git push --set-upstream origin main
username:
password:
```
