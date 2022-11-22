# ♦ Git & 브랜치 사용법

🏷태그: Ops, 클라우드OS, 클라우드인프라  
📆 학습일: 11/23/2022


## 목차

1. Git 사용법 (2)
2. branch 브랜치
3. 작업순서 : 수업자료 이해
4. 과제


## 1. Git 사용법 (2)


### 1.1 .gitignore 파일의 역할 테스트

```
[vagrant@host1 bitcamp-ncp]$ git log --oneline   한줄로 나타낸다
3e89afe Merge branch 'main' of https://github.com/yun5ol/bitcamp-ncp
701d0c1 Initial commit
dd9dd66 6
493c125 5
dcb1719 4
debe282 3
a8426f5 2
04bbdb5 1
[vagrant@host1 bitcamp-ncp]$ file .gitignore
.gitignore: ASCII text
[vagrant@host1 bitcamp-ncp]$ less .gitignore  파일을 딱 1페이지로 출력
## Created by https://www.toptal.com/developers/gitignore/api/windows,macos,linux,gradle,java,visualstudiocode,eclipse
# Edit at https://www.toptal.com/developers/gitignore?templates=windows,macos,linux,gradle,java,visualstudiocode,eclipse

### Eclipse ###
.metadata
bin/       해당 항목들이 포함되면 ignore 된다!
tmp/
*.tmp
*.bak
*.swp
*~.nib
local.properties
.settings/
.loadpath
.recommenders

.
.
.
```

### 1.2 git 명령어 활용 실습

```
[vagrant@host1 bitcamp-ncp]$ mkdir tmp
[vagrant@host1 bitcamp-ncp]$ pwd
/home/vagrant/git/bitcamp-ncp
[vagrant@host1 bitcamp-ncp]$ ls -al
total 16
drwxrwxr-x. 4 vagrant vagrant   90 Nov 22 00:55 .
drwxrwxr-x. 6 vagrant vagrant  104 Nov 21 10:49 ..
-rw-rw-r--. 1 vagrant vagrant   12 Nov 21 05:41 a.txt
-rw-rw-r--. 1 vagrant vagrant   14 Nov 21 05:54 b.txt
drwxrwxr-x. 8 vagrant vagrant  201 Nov 21 08:26 .git
-rw-rw-r--. 1 vagrant vagrant 3594 Nov 21 05:16 .gitignore
-rw-rw-r--. 1 vagrant vagrant   13 Nov 21 08:15 README.md
drwxrwxr-x. 2 vagrant vagrant    6 Nov 22 00:55 tmp
[vagrant@host1 bitcamp-ncp]$ cd tmp
[vagrant@host1 tmp]$ touch hello.txt  파일의 날짜와 시간을 수정하는 명령어
[vagrant@host1 tmp]$ ls -al
total 0
[drwxrwxr-x. 2 vagrant vagrant 23 Nov 22 00:56 .
drwxrwxr-x. 4 vagrant vagrant 90 Nov 22 00:55 ..
-rw-rw-r--. 1 vagrant vagrant  0 Nov 22 00:56 hello.txt](https://www.notion.so/Linux-ls-20064d91409e4313aa79e36fd25d8fa1)
[vagrant@host1 tmp]$ cd ..
[vagrant@host1 bitcamp-ncp]$ tree
.
├── a.txt
├── b.txt
├── README.md
└── tmp
    └── hello.txt

1 directory, 4 files
[vagrant@host1 bitcamp-ncp]$ touch hello2.txt
[vagrant@host1 bitcamp-ncp]$ tree
.
├── a.txt
├── b.txt
├── hello2.txt
├── README.md
└── tmp
    └── hello.txt

1 directory, 5 files
[vagrant@host1 bitcamp-ncp]$ git status
# On branch main
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#       hello2.txt
nothing added to commit but untracked files present (use "git add" to track)
[vagrant@host1 bitcamp-ncp]$ git status --short    상태를 짧게
?? hello2.txt    hello.txt 가 안 뜨는 이유 : tmp/ gitignore 했기 때문
[vagrant@host1 bitcamp-ncp]$ mkdir tmp2
[vagrant@host1 bitcamp-ncp]$ cd tmp2
[vagrant@host1 tmp2]$ touch hello3.txt

[vagrant@host1 bitcamp-ncp]$ rm -rf tmp    -rf 강제적으로 지워라

[vagrant@host1 bitcamp-ncp]$ rm *bak     * 붙으면 bak 이 붙는 파일은 전부 지워라
[vagrant@host1 bitcamp-ncp]$ tree
.
├── a.txt
├── b.txt
├── hello2.txt
└── README.md

0 directories, 4 files

🚩 # git rm 예시
[vagrant@host1 bitcamp-ncp]$ git rm b.txt   rm:스테이징 목록에서 내린다
무대에 이미 올렸으니 내리던가 아예 커밋 시켜놓고 삭제해야
error: 'b.txt' has changes staged in the index
(use --cached to keep the file, or -f to force removal) 

[vagrant@host1 bitcamp-ncp]$ git diff a.txt 파일의 변경 내용을 비교
[vagrant@host1 bitcamp-ncp]$ nano a.txt
[vagrant@host1 bitcamp-ncp]$ git status --short
 M a.txt
?? hello2.txt
[vagrant@host1 bitcamp-ncp]$ git diff a.txt
diff --git a/a.txt b/a.txt
index d62462e..0bfd14a 100644
--- a/a.txt
+++ b/a.txt
@@ -1,4 +1,4 @@
 1111
 2222
-      - : 빠진 항목
+321   + : 추가된 항목   현재는 굳이 이렇게 확인하지 않아..

# git checkout

: 작업 디렉토리의 파일을 변경 후 변경 전으로 되돌린다
modifed > unmodifed : 스테이징 오르기 전! 복구 가능
staged > modifed 로는 불가 : 무대로 올렸으면 (add) 올리기 전의 상태로 복구 불가

[vagrant@host1 bitcamp-ncp]$ git status --short
 M a.txt
?? hello2.txt   b.txt 안 나오잖아 = unmodified : 서버에서 꺼냈으나 편집되지 않은 상태
[vagrant@host1 bitcamp-ncp]$ nano b.txt
[vagrant@host1 bitcamp-ncp]$ git status --short
 M a.txt
 M b.txt     수정해서 나오잖아 = modified : staged 될 준비가 됐어 + 4444
?? hello2.txt
[vagrant@host1 bitcamp-ncp]$ git checkout b.txt
[vagrant@host1 bitcamp-ncp]$ cat b.txt   cat : 바로 출력, 나노 접속 x
33331111
2222       +4444 가 사라진 것 확인 가능
[vagrant@host1 bitcamp-ncp]$ git status --short
 M a.txt
?? hello2.txt   b.txt 체크아웃 했더니 다시 unmodifed : 출력되지 않음
[vagrant@host1 bitcamp-ncp]$ nano b.txt
[vagrant@host1 bitcamp-ncp]$ git status --short
 M a.txt
 M b.txt     수정해서 다시 modified : 출력 가능
?? hello2.txt
[vagrant@host1 bitcamp-ncp]$ cat a.txt
1111
2222
321    +321
[vagrant@host1 bitcamp-ncp]$ cat b.txt
33331111
2222
4444   +4444
[vagrant@host1 bitcamp-ncp]$ git add b.txt
[vagrant@host1 bitcamp-ncp]$ git status --short
 M a.txt     변경 후 unstaged : modifed
M  b.txt     변경 후 staged
?? hello2.txt
[vagrant@host1 bitcamp-ncp]$ git checkout a.txt
[vagrant@host1 bitcamp-ncp]$ cat a.txt
1111
2222
        -321

[vagrant@host1 bitcamp-ncp]$ cat b.txt  워킹 디렉토리의 파일을 변경 > 변경 전으로
33331111                                b.txt 를 수정 > 스테이징 에리어로 넘어 갔으니 체크아웃 대상 x
2222
4444
[vagrant@host1 bitcamp-ncp]$ git checkout b.txt
[vagrant@host1 bitcamp-ncp]$ cat b.txt
33331111
2222
4444
[vagrant@host1 bitcamp-ncp]$ nano b.txt   +5555
[vagrant@host1 bitcamp-ncp]$ git status --short
MM b.txt    modified 후 staged : 왼쪽 M / 다시 한 번 수정하고 unmodified : 오른쪽 M
?? hello2.txt
[vagrant@host1 bitcamp-ncp]$ cat b.txt
33331111
2222
4444
5555
[vagrant@host1 bitcamp-ncp]$ git checkout b.txt
[vagrant@host1 bitcamp-ncp]$ cat checkout b.txt
cat: checkout: No such file or directory   수정하고 무대에 올렸으면 저장소의 원본 형태로 복구 불가
33331111                                수정했으나 무대에 올린게 없으면 저장소에 있는 상태로 복구 가능
2222
4444
[vagrant@host1 bitcamp-ncp]$ git status --short
M  b.txt
?? hello2.txt

# git reset HEAD (feat. git checkout)
git rm과 달리 staged 된 수정사항 삭제하려면 git checkout

- Head : 작업 브랜치의 push 된 version 을 가리킴
- 파일을 변경하고 git add 한 후 다시 commited 상태로 돌릴 때

[vagrant@host1 bitcamp-ncp]$ git log --oneline --graph --all  : GUI sourcetree 설치
*   3e89afe (HEAD -> main, origin/main) Merge branch 'main' of https://github.com/yun5ol/bitcamp-ncp
|\
| * 701d0c1 Initial commit
* dd9dd66 6
* 493c125 5
* dcb1719 4
* debe282 3
* a8426f5 2
* 04bbdb5 1
[vagrant@host1 bitcamp-ncp]$ git status --short
M  b.txt
?? hello2.txt
[vagrant@host1 bitcamp-ncp]$ git reset HEAD b.txt   :   staged 된 걸 HEAD 버전으로 다시 reset (1번)
Unstaged changes after reset:                        변경된 걸 날리는 상태는 아니다! modified 상태로!
M       b.txt                                           변경 전으로 되돌리려면 git checkout
[vagrant@host1 bitcamp-ncp]$ git status --short            (다시 git commit 하는 것과 같음)
 M b.txt
?? hello2.txt
[vagrant@host1 bitcamp-ncp]$ git status --short
 M b.txt
?? hello2.txt
[vagrant@host1 bitcamp-ncp]$ git checkout b.txt
Updated 1 path from the index
[vagrant@host1 bitcamp-ncp]$ cat b.txt
33331111

# git remote 
로컬 저장소에 연결된 원격 저장소를 확인하거나 추가한다.
git clon URL 로 원격 저장소를 복제하면, 원격 저장소가 **origin** 으로 자동 등록된다.

[vagrant@host1 bitcamp-ncp]$ git remote    원격 저장소 이름 알아내기
origin
[vagrant@host1 bitcamp-ncp]$ git remote -v    원격 저장소 이름 뿐 아니라 URL도 알아내기
origin  https://github.com/yun5ol/bitcamp-ncp (fetch)  다운받는 URL
origin  https://github.com/yun5ol/bitcamp-ncp (push)   업로드하는 URL
[vagrant@host1 bitcamp-ncp]$ git remote show origin
* remote origin
  Fetch URL: https://github.com/yun5ol/bitcamp-ncp
  Push  URL: https://github.com/yun5ol/bitcamp-ncp
  HEAD branch: main
  Remote branch:
    main tracked
  Local branch configured for 'git pull':   현재 원격과 로컬 모두 브랜치명이 main
    main merges with remote main
  Local ref configured for 'git push':
    main pushes to main (up to date)

# 현재 HEAD가 가리키는 브랜치의 역사 뿐 아니라 다른 브랜치의 역사까지 출력
[vagrant@host1 bitcamp-ncp]$ git log --oneline --graph --all
* 8dd276d (HEAD -> main) 11    로컬쪽
*   3e89afe (origin/main) Merge branch 'main'... 서버쪽
|\
| * 701d0c1 Initial commit
* dd9dd66 6
* 493c125 5
```

```b
# 2서버 열기

[vagrant@host2 ~]$ ls
git
[vagrant@host2 ~]$ cd git
[vagrant@host2 git]$ pwd
/home/vagrant/git

# git 최신 업데이트 하고, clone
[vagrant@host2 git]$ git clone https://github.com/yun5ol/bitcamp-ncp
[vagrant@host2 git]$ cd bitcamp-ncp

git log 확인하면 git log --oneline --graph --all
서버 1과 2과 동일한 것 확인 가능

# 서버 1에서 나노a 수정 후 커밋하자

[vagrant@host1 bitcamp-ncp]$ nano a.txt
[vagrant@host1 bitcamp-ncp]$ git add.
git: 'add.' is not a git command. See 'git --help'.

The most similar command is
        add
[vagrant@host1 bitcamp-ncp]$ git add .
[vagrant@host1 bitcamp-ncp]$ git commit -m "12"
[main a8354e2] 12
 1 file changed, 1 insertion(+), 1 deletion(-)
[vagrant@host1 bitcamp-ncp]$ git log --oneline --graph --all
* a8354e2 (HEAD -> main) 12
* 8dd276d (origin/main) 11
*   3e89afe Merge branch 'main' of https://github.com/yun5ol/bitcamp-ncp
|\
| * 701d0c1 Initial commit
* dd9dd66 6
* 493c125 5
* dcb1719 4
* debe282 3
* a8426f5 2
* 04bbdb5 1
[vagrant@host1 bitcamp-ncp]$

# git fetch & git merge
# 서버2로 git pull 하면 서버 1, 2 로그 상태가 동일 확인

git pull : 받아와서 머지까지 된 것
merge : 받아온 걸 합치는거
git fetch : 받아오는 것 까지만!

# 서버 1 나노 수정하고 1 다시 커밋
서버 2 에 git fetch 로 받고 로그 비교하면!

[vagrant@host1 bitcamp-ncp]$ git log --oneline --graph --all
* 1ee192a (HEAD -> main, origin/main) 13
* a8354e2 12
* 8dd276d 11
*   3e89afe Merge branch 'main' of https://github.com/yun5ol/bitcamp-ncp
|\
| * 701d0c1 Initial commit
* dd9dd66 6
* 493c125 5
* dcb1719 4
* debe282 3
* a8426f5 2
* 04bbdb5 1

[vagrant@host2 bitcamp-ncp]$ git log --oneline --graph --all
* 1ee192a (origin/main, origin/HEAD) 13
* a8354e2 12
| * 5507a12 (HEAD -> main) 12
|/
* 8dd276d 11
*   3e89afe Merge branch 'main' of https://github.com/yun5ol/bitcamp-ncp
|\
| * 701d0c1 Initial commit
* dd9dd66 6
* 493c125 5
* dcb1719 4
* debe282 3
* a8426f5 2
* 04bbdb5 1

# 페치한거 합쳐보자
# 충돌나면 ??????
https://wikidocs.net/17171

Auto-merging a.txt
CONFLICT (content): Merge conflict in a.txt
Automatic merge failed; fix conflicts and then commit the result.
```

- fast foward
    
    : git merge 관련
    
    합치려는 브랜치가 현 브랜치 보다 upstream (이후 버전)일 경우, 
    
    별도의 merge 과정이 필요없고, 
    
    해당 브랜치의 최신 버전의 커밋을 이동한다.
    

### 1.3 git merge 충돌

```b
# 서버랑 로컬 버전 다를 때 rejected
서버 1에서 수정한 게 있는데
서버 2도 수정을 한 상황

서버 2가 마음대로 push 하면 서버1께 날라가?
그러면 안되니깐 먼저 가져오자!!

[vagrant@host2 bitcamp-ncp]$ git push
Username for 'https://github.com': yun5ol
Password for 'https://yun5ol@github.com':
To https://github.com/yun5ol/bitcamp-ncp
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/yun5ol/bitcamp-ncp'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

# 페치한거 합쳐보자
# 그런데 같은 파일이 있어서 충돌나면 ??????
https://wikidocs.net/17171

Auto-merging a.txt
CONFLICT (content): Merge conflict in a.txt
Automatic merge failed; fix conflicts and then commit the result.

# 두 서버에서 같은 파일을 편집 . 맘대로 커밋해서 덮을 순 없자날
 eg. a.txt에 host1=xxx / host2=yyy
 eg. 작업하고 집에서 편집할 때 합치고 편집을 해야하는데... 안했어!!! 그냥 로컬에서 수정했어!

[vagrant@host1 bitcamp-ncp]$ nano a.txt
[vagrant@host1 bitcamp-ncp]$ git push   
Username for 'https://github.com': yun5ol
Password for 'https://yun5ol@github.com':
Everything up-to-date
푸시라는 것은 작업디렉토리로 바로 땅기는 것이 아니라, 서버의 변경된 사항을 로컬로 가져온다는것
현재 편집 중인게 있을 때는 git pull 이 먹히지 않는다.

[vagrant@host2 bitcamp-ncp]$ git merge
Auto-merging a.txt
CONFLICT (content): Merge conflict in a.txt
Automatic merge failed; fix conflicts and then commit the result.
[vagrant@host2 bitcamp-ncp]$ cat a.txt
1111
2222
3333
4444
5555
6666
7777
8888
<<<<<<< HEAD
host2=yyy    이거 내가 바꾼거 (host2 상태)
=======
host1=>xxx   이거 다른 서버에서 바꾼거
>>>>>>> refs/remotes/origin/main   내가 맘대로 덮어쓸 수 없으니깐 너가 편집해
[vagrant@host1 bitcamp-ncp]$ git branch -d b1     개발 후 메인에 합쳤으면, 이전 브랜치는 반드시 지워라
Deleted branch b1 (was 5a011a6).          지워야하는 이유 & 작업 순서 그림 참고!!
[vagrant@host1 bitcamp-ncp]$ git branch   브랜치를 따올 땐 습관적으로 서버에서 최신 버전으로 브랜치 pull 하도록
* main      b1 이 사라진 것 확인 가능
[vagrant@host1 bitcamp-ncp]$ git log --oneline
5a011a6 (HEAD -> main) 26    b1 이 사라진 것 확인 가능
de1e3f5 25
639547f (origin/main) 24

# 브랜치 따서 작업 후 메인에 merge 할 때는 merge 를 받을 대상으로 checkout
```

## 2. branch 브랜치

- Git의 브랜치는 커밋 사이를 이동할 때 사용하는 포인터 같은 것이다.
- 커밋의 체크섬을 이용하여 여러 커밋들 중에서 한 커밋을 가리킨다.
- 따라서 브랜치를 여러 개 만들어도 전혀 상관없다.
- Git은 브랜치를 만들어 작업하고 나중에 merge 하는 것을 권장한다.
- 하루에 수십 번씩 해도 괜찮다고 제안하고 있다.

> **chekcout** : HEAD가 가리키는 브랜치의 최신 버전을 작업 디렉토리에 꺼낸다.
> 

```
# 브랜치를 관리
git branch
# 브랜치 중에 merge 한 항목 조회
git branch merge
# 브랜치 중에 merge 하지 않은 항목 조회
git branch --no-merged
# 브랜치 삭제
git branch -d []
# 작업 디렉토리에 커밋 파일을 교체하기
git checkout []     : HEAD 포인터를 옮긴다

```

## 3. 작업순서 : 수업자료 이해  

![화면 캡처 2022-11-22 201630](https://user-images.githubusercontent.com/118426836/203301046-40ce0f01-e52f-4f0a-ab9a-136a7da7748b.png)


1. **서버 리포지토리 생성**
2. **서버 리포지토리** **클론**
3. **로컬 브랜치 따서 작업하고 커밋**
4. **메인 브랜치에 머지**
5. **서버 최신버전 풀**
6. **로컬의 브랜치와 메인을 머지**
7. **서버에 푸시 (로컬 브랜치의 과정 까지 모두 푸시됨)**
8. **로컬 브랜치 삭제**

 

## 4. 과제

1. **리포지토리 생성 : That’s me ! 권한 부여 필요 (bitcamp-test)**
    1. **쓰기권한 부여** 
        
        **리포지 settings > collaborators > add people** 
        
    2. **이메일 발송**
2. **서버 리포지토리 생성**
3. **서버 리포지토리** **클론**
4. **로컬 브랜치 따서 작업하고 커밋**
5. **메인 브랜치에 머지**
6. **서버 최신버전 풀**
7. **로컬 브랜치와 로컬 메인을 머지**
8. **서버 메인 것 풀**
9. **서버 메인에 푸시 (로컬 브랜치의 과정 까지 모두 푸시됨)**
10. **로컬 브랜치 삭제**

```

test 2

cd vm-projects
cd centos test1
vagrant ssh
cd git

git branch
git branch x1
git checkout x1
git branch
git clone url
nano a.txt
git add .
git commit -m "1"
nano a.txt
git add .
git commit -m "2"
nano a.txt
git add .
git commit -m "3"

git checkout main
git branch
git merge x1
git pull
git push

git branch 

# git init 할 것
fatal: Not a git repository (or any of the parent directories): .git

# git rm -rf .bash_history
[vagrant@host1 ~]$ git checkout main
error: Your local changes to the following files would be overwritten by checkout:
.bash_history
Please commit your changes or stash them before you switch branches.
Aborting

```

### 번외 )

> 1.
> 
> 
> 리눅스 git 최신 업데이트 필요 시
> 
> - [https://dololgun.github.io/linux/centos7-git-install/](https://dololgun.github.io/linux/centos7-git-install/)
> 
> ```bash
> 	[vagrant@host1 bitcamp-ncp]$ git --version
> git version 1.8.3.1
> [vagrant@host1 bitcamp-ncp]$ yum install http://opensource.wandisco.com/centos/7/git/x86_64/wandisco-git-release-7-1.noarch.rpm
> Loaded plugins: fastestmirror
> You need to be root to perform this command.   +sudo
> [vagrant@host1 bitcamp-ncp]$ sudo yum install http://opensource.wandisco.com/centos/7/git/x86_64/wandisco-git-release-7-1.noarch.rpm
> Loaded plugins: fastestmirror
> wandisco-git-release-7-1.noarch.rpm                                          | 4.5 kB  00:00:00
> Examining /var/tmp/yum-root-NOC2zS/wandisco-git-release-7-1.noarch.rpm: wandisco-git-release-7-1.noarch
> Marking /var/tmp/yum-root-NOC2zS/wandisco-git-release-7-1.noarch.rpm to be installed
> Resolving Dependencies
> --> Running transaction check
> ---> Package wandisco-git-release.noarch 0:7-1 will be installed
> --> Finished Dependency Resolution
> 
> Dependencies Resolved
> 
> ====================================================================================================
>  Package                     Arch          Version    Repository                               Size
> ====================================================================================================
> Installing:
>  wandisco-git-release        noarch        7-1        /wandisco-git-release-7-1.noarch        1.9 k
> 
> Transaction Summary
> ====================================================================================================
> Install  1 Package
> 
> Total size: 1.9 k
> Installed size: 1.9 k
> Is this ok [y/d/N]: y
> Downloading packages:
> Running transaction check
> Running transaction test
> Transaction test succeeded
> Running transaction
>   Installing : wandisco-git-release-7-1.noarch                                                  1/1
>   Verifying  : wandisco-git-release-7-1.noarch                                                  1/1
> 
> Installed:
>   wandisco-git-release.noarch 0:7-1
> 
> Complete!
> [vagrant@host1 bitcamp-ncp]$ yum remove git
> Loaded plugins: fastestmirror
> You need to be root to perform this command.
> [vagrant@host1 bitcamp-ncp]$ sudo yum remove git
> Loaded plugins: fastestmirror
> Resolving Dependencies
> --> Running transaction check
> ---> Package git.x86_64 0:1.8.3.1-23.el7_8 will be erased
> --> Processing Dependency: git = 1.8.3.1-23.el7_8 for package: perl-Git-1.8.3.1-23.el7_8.noarch
> --> Running transaction check
> ---> Package perl-Git.noarch 0:1.8.3.1-23.el7_8 will be erased
> --> Finished Dependency Resolution
> 
> Dependencies Resolved
> 
> ====================================================================================================
>  Package               Arch                Version                         Repository          Size
> ====================================================================================================
> Removing:
>  git                   x86_64              1.8.3.1-23.el7_8                @base               22 M
> Removing for dependencies:
>  perl-Git              noarch              1.8.3.1-23.el7_8                @base               57 k
> 
> Transaction Summary
> ====================================================================================================
> Remove  1 Package (+1 Dependent package)
> 
> Installed size: 22 M
> Is this ok [y/N]: y
> Downloading packages:
> Running transaction check
> Running transaction test
> Transaction test succeeded
> Running transaction
>   Erasing    : perl-Git-1.8.3.1-23.el7_8.noarch                                                 1/2
>   Erasing    : git-1.8.3.1-23.el7_8.x86_64                                                      2/2
>   Verifying  : git-1.8.3.1-23.el7_8.x86_64                                                      1/2
>   Verifying  : perl-Git-1.8.3.1-23.el7_8.noarch                                                 2/2
> 
> Removed:
>   git.x86_64 0:1.8.3.1-23.el7_8
> 
> Dependency Removed:
>   perl-Git.noarch 0:1.8.3.1-23.el7_8
> 
> Complete!
> [vagrant@host1 bitcamp-ncp]$ git
> -bash: /usr/bin/git: No such file or directory
> [vagrant@host1 bitcamp-ncp]$ sudo yum install git -y
> Loaded plugins: fastestmirror
> Loading mirror speeds from cached hostfile
>  * base: mirror.kakao.com
>  * extras: mirror.kakao.com
>  * updates: mirror.kakao.com
> WANdisco-git                                                                 | 2.9 kB  00:00:00
> base                                                                         | 3.6 kB  00:00:00
> extras                                                                       | 2.9 kB  00:00:00
> updates                                                                      | 2.9 kB  00:00:00
> WANdisco-git/7/x86_64/primary_db                                             | 153 kB  00:00:01
> Resolving Dependencies
> --> Running transaction check
> ---> Package git.x86_64 0:2.31.1-1.WANdisco.1657096008 will be installed
> --> Processing Dependency: perl-Git = 2.31.1-1.WANdisco.1657096008 for package: git-2.31.1-1.WANdisco.1657096008.x86_64
> --> Processing Dependency: perl(Git) for package: git-2.31.1-1.WANdisco.1657096008.x86_64
> --> Processing Dependency: perl(Digest::SHA) for package: git-2.31.1-1.WANdisco.1657096008.x86_64
> --> Processing Dependency: perl(Git::I18N) for package: git-2.31.1-1.WANdisco.1657096008.x86_64
> --> Running transaction check
> ---> Package perl-Digest-SHA.x86_64 1:5.85-4.el7 will be installed
> --> Processing Dependency: perl(Digest::base) for package: 1:perl-Digest-SHA-5.85-4.el7.x86_64
> ---> Package perl-Git.noarch 0:2.31.1-1.WANdisco.1657096008 will be installed
> --> Running transaction check
> ---> Package perl-Digest.noarch 0:1.17-245.el7 will be installed
> --> Finished Dependency Resolution
> 
> Dependencies Resolved
> 
> ====================================================================================================
>  Package                Arch          Version                             Repository           Size
> ====================================================================================================
> Installing:
>  git                    x86_64        2.31.1-1.WANdisco.1657096008        WANdisco-git        8.7 M
> Installing for dependencies:
>  perl-Digest            noarch        1.17-245.el7                        base                 23 k
>  perl-Digest-SHA        x86_64        1:5.85-4.el7                        base                 58 k
>  perl-Git               noarch        2.31.1-1.WANdisco.1657096008        WANdisco-git         23 k
> 
> Transaction Summary
> ====================================================================================================
> Install  1 Package (+3 Dependent packages)
> 
> Total download size: 8.8 M
> Installed size: 41 M
> Downloading packages:
> (1/4): perl-Digest-1.17-245.el7.noarch.rpm                                   |  23 kB  00:00:00
> (2/4): perl-Digest-SHA-5.85-4.el7.x86_64.rpm                                 |  58 kB  00:00:00
> warning: /var/cache/yum/x86_64/7/WANdisco-git/packages/perl-Git-2.31.1-1.WANdisco.1657096008.noarch.rpm: Header V4 DSA/SHA1 Signature, key ID 3bbf077a: NOKEY
> Public key for perl-Git-2.31.1-1.WANdisco.1657096008.noarch.rpm is not installed
> (3/4): perl-Git-2.31.1-1.WANdisco.1657096008.noarch.rpm                      |  23 kB  00:00:00
> (4/4): git-2.31.1-1.WANdisco.1657096008.x86_64.rpm                           | 8.7 MB  00:00:09
> ----------------------------------------------------------------------------------------------------
> Total                                                               991 kB/s | 8.8 MB  00:00:09
> Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-WANdisco
> Importing GPG key 0x3BBF077A:
>  Userid     : "WANdisco (http://WANdisco.com - We Make Software Happen...) <software-key@wandisco.com>"
>  Fingerprint: 69c1 be83 da54 cbed 6889 72f8 e9f0 e922 3bbf 077a
>  From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-WANdisco
> Running transaction check
> Running transaction test
> Transaction test succeeded
> Running transaction
>   Installing : perl-Digest-1.17-245.el7.noarch                                                  1/4
>   Installing : 1:perl-Digest-SHA-5.85-4.el7.x86_64                                              2/4
>   Installing : perl-Git-2.31.1-1.WANdisco.1657096008.noarch                                     3/4
>   Installing : git-2.31.1-1.WANdisco.1657096008.x86_64                                          4/4
>   Verifying  : git-2.31.1-1.WANdisco.1657096008.x86_64                                          1/4
>   Verifying  : 1:perl-Digest-SHA-5.85-4.el7.x86_64                                              2/4
>   Verifying  : perl-Git-2.31.1-1.WANdisco.1657096008.noarch                                     3/4
>   Verifying  : perl-Digest-1.17-245.el7.noarch                                                  4/4
> 
> Installed:
>   git.x86_64 0:2.31.1-1.WANdisco.1657096008
> 
> Dependency Installed:
>   perl-Digest.noarch 0:1.17-245.el7                      perl-Digest-SHA.x86_64 1:5.85-4.el7
>   perl-Git.noarch 0:2.31.1-1.WANdisco.1657096008
> 
> Complete!
> ```
> 
> 1. 
> 
> ```bash
> # 참고로 가능한 푸시는 최종 한번 하는게 좋아
> 커밋은 로컬에서 계속 하고 푸시는 집가기 전에 한번 하기
> 그리고 버그있는 건 커밋하면 안되지!! 
> 푸시 마지막 한번하면 커밋 과정, 횟수 전체 푸시됨!!
> 
> Auto-merging a.txt
> CONFLICT (content): Merge conflict in a.txt
> Automatic merge failed; fix conflicts and then commit the result.
> ```
>
