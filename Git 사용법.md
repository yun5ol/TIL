# ๐ป git ์ฌ์ฉ๋ฒ

๐ท ํ๊ทธ: Ops, ํด๋ผ์ฐ๋OS, ํด๋ผ์ฐ๋์ธํ๋ผ  
๐ ํ์ต์ผ: 11/21/2022

## 1. Vagrantfile ์ดํดํ๊ธฐ


~/vm-projects

	centos test/Vagrantfile

	centos test2/Vagrantfile

	centos test3/Vagrantfile

> VM์์ฑํ๋ก์ ํธ / VM์ค์ ์ ๋ณดํ์ผ

โฌ

โvagrant upโ

โฌ

~/Virtualbox VMs/

	centostest_defaultโฆ/โฆ.vmdk(๋ฒ์ธ์ผ๋จธ์ ๋์คํฌ)

	centostest2_defaultโฆ/โฆ.vmdk(๋ฒ์ธ์ผ๋จธ์ ๋์คํฌ)

	centostest3_defaultโฆ/โฆ.vmdk(๋ฒ์ธ์ผ๋จธ์ ๋์คํฌ)

> VM์ํด๋ / VM์ํ์ผ

  
  
  
- **Vagrantfile = project**
    
    **VMs file = VM ์ด๋ผ๋ ๊ฐ๋ ์ดํดํ  ๊ฒ**
    
 
    ๐ก **vagrant ํ๋ก์ ํธ** : โ๊ฐ์๋จธ์ ์ ๋ง๋ค๊ณ  ์ด๊ธฐํ์ํค๋โ ์ค์  ์ ๋ณด๊ฐ ์๋ ํ๋ก์ ํธ
    
	    ํ๋ก์ ํธ๋ฅผ ์ง์ ๋ค๊ณ  vm์ด ์ง์์ง๋๊ฒ ์๋๋ค

	    eg. ํ๋ก์ ํธ ํ์ผ์ ์ง์๋ VB, VMs ์ ์กด์ฌํด

	    CLI ์์ โvagrant destroy <id>โ ํด๋ ํ๋ก์ ํธ ํด๋๋ฅผ ์ฐพ๊ธฐ ๋๋ฌธ์ ๋ช๋ น์ด๊ฐ ๋จนํ์ง ์์

	    GUI ์ญ์  ํ VMs ํ์ธ ํ๋ฉด VMs ์ญ์ ๋์ด์๋ ๊ฒ ํ์ธ ๊ฐ๋ฅ

	    ๐ฉor VMs ํด๋์์ ์ง์  ์ญ์ 

	    ๐ฉbut ํ๋ก์ ํธ ํ์ผ์ ์์์์ผ๋ก ์ง์์ค์ผ!
    
    
    
    ```
    # ๋ฌผ๋ก  ํด๋น ๋๋ ํ ๋ฆฌ ๋ด์์ ๋ช๋ น์ด ์์ฑ ํ  ๊ฒ
    
    C:\Users\bitcamp>cd vm-projects
    C:\Users\bitcamp\vm-projects>cd cetos2
    C:\Users\bitcamp\vm-projects\cetos2>vagrant destroy
        default: Are you sure you want to destroy the 'default' VM? [y/N] y
    ==> default: Discarding saved state of VM...
    ==> default: Destroying VM and associated drives...
    C:\Users\bitcamp\vm-projects\cetos2>cd..
    ```
    

## 2. VCS : Version Control System, ๋ฒ์ ๊ด๋ฆฌ์์คํ


### 2.1 VCS ๊ฐ์

- ํ์ผ ๋ณํ๋ฅผ ์๊ฐ์ ๋ฐ๋ผ ๊ธฐ๋กํ๋ค ํน์  ์์ ์ ๋ฒ์ ์ ๋ค์ ๊บผ๋ด์ฌ ์ ์๋ ์์คํ
- ํ์ผ๋ณ๋ก ์ด์  ์ํ๋ก ๋๋๋ฆฌ๊ฑฐ๋ ํ๋ก์ ํธ ํต์งธ๋ก ์ด์  ๋ฒ์ ผ์ผ๋ก ๋๋ฆด ์ ์๋ค.
- ์๊ฐ์ ๋ฐ๋ผ ์์  ๋ด์ฉ์ ๋น๊ตํ  ์ ์๋ค.
- ๋๊ฐ ์ธ์ , ์ด๋ป๊ฒ ๋ฌธ์ ๋ฅผ ์ผ์ผ์ผฐ๋์ง ์ถ์ ํ  ์ ์๋ค.

### 2.2 CVS vs SVN vs GIT

**๊ฐ์** 

- ๋ก์ปฌ ๋ฒ์  ๊ด๋ฆฌ ์์คํ
    - ๊ฐ๋จํ ๋ฐ์ดํฐ๋ฒ ์ด์ค๋ฅผ ์ด์ฉํ์ฌ ํ์ผ์์ ๋ณ๊ฒฝ๋๋ ๋ถ๋ถ์ ๊ด๋ฆฌ
    - eg. RCS (Revision Control System)
- ์ค์์ง์ค์ ๋ฒ์  ๊ด๋ฆฌ
    - ํ์ผ์ ๋ง์ง๋ง ์ค๋์ท์ ๋ฐ๋๋ค (checkout)
- ๋ถ์ฐ ๋ฒ์  ๊ด๋ฆฌ ์์คํ

1. **CVS : Concurrent Versions System**
    
    ์๋ฒ ๋ฆฌํฌ์์ ๋ก์ปฌ๋ก ๋์ค๋ ๊ฑธ checkout (๊ฐ ํ์ผ์ **๋ง์ง๋ง ์ค๋์ท**์ checkout)
    ๋ฐ๋๋ check in = commit 
    
    > snapshot ์ค๋์ท : ํน์  ์์ ์ ํ์ผ ๋ฒ์ ์ ๊ธฐ๋กํ ๊ฒ
    > 
    > 
    > eg. ๋ฌด๋์์ ์ฌ๋ฆด, ๋ด๋ฆด staging ๊ฒ์ ์ฐฐ์นต ์ฐ๋๋ค~!
    > 


	๐ก check in = commit   
	1. ์ต์  ๋ฒ์ ์ ํ์ผ์ ๊ฐ์ ธ์จ๋ค.
	2. ํ์ผ์ ํต์งธ๋ก ์๋ฒ์ ์ ์กํ๋ค.

์๋ฒ ๋ฆฌํฌ์๋ ํ๋ก์ ํธํ์ผ+ **๋ณ๊ฒฝ๋ด์ญ** ๊น์ง ํฌํจ๋์ด์๋ค.
  
์๋ฒ์์ ๋ณ๊ฒฝ ๋ด์ฉ์ ๊ด๋ฆฌํ๋ **์ค์์ง์ค๋ฐฉ์**

- ์๋ฒ์ ๋ฌธ์ ๊ฐ ๋ฐ์ํ๋ฉด ๋ณ๊ฒฝ ๋ด์ญ์ ๋ชจ๋ ์๋๋ค.
- ํ์ผ์ ํต์งธ๋ก ์ฃผ๊ณ ๋ฐ์ผ๋ฉด ๋คํธ์ํฌ์ ๋ถํ (overhead) ๋ฐ์
    
    ๋ณ๊ฒฝ ๋ด์ฉ ์ธ ๊ธฐ์กด ๋ด์ฉ๊น์ง ์ ์กํ๊ธฐ ๋๋ฌธ : ๋คํธ์ํฌ ๊ณผ๋ค ์ฌ์ฉ, ๋คํธ์ํฌ ์ค๋ฒํค๋
    
</aside>

1. **SVN : Subversion**
    
    cvs ์ ๋์ผํ๊ฒ ์ค์์ง์ค๋ฐฉ์ ์ด์ง๋ง,
    
    **ํ์ผ์ ๋ณ๊ฒฝ ๋ถ๋ถ๋ง ์๋ฒ๋ก ์ ์กํ๋ค.** (๊ฐ ํ์ผ์ **๋ง์ง๋ง ์ค๋์ท**์ **checkout**)
    
    ๋ฐ๋ผ์, cvs๋ณด๋ค ์ค๋ฒํค๋๊ฐ ์ ๋ค.
    
    ํ์ง๋ง, ์๋ฒ์ ๋ฌธ์  ๋ฐ์์์๋ ๋์ผํ ๋จ์ ์ด ์๋ค.
    

1. **GIT**
    
    ์ ๋๊ฐ์ง๋ฅผ ๋ชจ๋ ๊ทน๋ณต
    
    ์๋ฒ ๋ฆฌํฌ๋ฅผ ๊ทธ๋๋ก ๋ก์ปฌ๋ก **clone**
    
    **๋ก์ปฌ ๋ฆฌํฌ์** ํ๋ก์ ํธํ์ผ+ **๋ณ๊ฒฝ๋ด์ญ** ๊น์ง ํฌํจ
    
    - **์ ์ฅ์๋ฅผ ํด๋ผ์ด์ธํธ ์ชฝ์ ๋ถ์ฐ ๋ณต์  : ์์ ์ฑ์ด ๋๋ค**
        
        ์๋ฒ์ ๋ฌธ์  ๋ฐ์ํ๋๋ผ๋ ํด๋ผ์ด์ธํธ์ ๋ถ์ฐ ๋ณต์ ๋ ๋ฆฌํฌ์งํ ๋ฆฌ๋ฅผ ์ฌ์ฉํ์ฌ ์์๋ณต๊ตฌ ๊ฐ๋ฅ
        
        push & pull
        
    - **commit & push & pull : ๋คํธ์ํฌ ์ค๋ฒํค๋๊ฐ ์ ๋ค**
    
    ```bash
    # ๋ณ๊ฒฝ ํ commit
    git commit : ์๋ฒ์ ์๋ก๋๊ฐ ์๋๋ผ ๋ก์ปฌ ๋ฆฌํฌ์งํ ๋ฆฌ์ ์ ์ฅ 
    # ๊ณต์ ๊ฐ ํ์ํ  ๋
    git push : ์๋ฒ๋ก
    git pull : ๋ก์ปฌ๋ก
    ```
    

## 3. git ์ฌ์ฉ๋ฒ

---

### 3.1 Git์ ํ์ผ ์ํ

modified : ํ์ผ์ด ๋ณ๊ฒฝ๋์์ง๋ง ์์ง ๋ก์ปฌ db์ ์ ์ฅ๋์ง ์์ > ์์ ํ์ผ๋ add ํ์ง ์์ ์ํ

committed : ๋ก์ปฌ db์ ์์ ํ ์ ์ฅ. ๋ฐ๋ ๊ฒ ์์ด ์ ์ฅ๋ ์ํ > add ์๋ฃ ํ ์ปค๋ฐ

staged : ๋ก์ปฌ db์ ์ ์ฅํ  ํ์ผ์์ ํ์ํ๋ค > add ํ ์ํ 

: ์คํ์ด์ง ๋์์ผ๋ ์ค๋์ท์ ์ฐ์ ์ ์๋ค. ๋ฌด๋์ ์ฌ๋ผ์์ผ๋ ์ฌ์ง ์ฐ์ด์ค๊ฒ!

        ๋ค์ ์ปค๋ฐํ  ๋ staged๋ก ํ์๋ํ์ผ์ ๋ณ๊ฒฝ ๋ด์ฉ์ด ์ ์ฅ๋  ๊ฒ์ด๋ค.

### 3.2 Git ํ๋ก์ ํธ์ ๋จ๊ณ : 3๋จ๊ณ

<aside>
๐ก ํ์ผ ํ์๊ธฐ > git > bitcamp-study  
	
**.git** ์ ๋ณ๊ฒฝ๋ ๋ด์ฉ๋ค์ด ์๋ค = ๋ก์ปฌ ์ ์ฅ์ = git ์ด ๊ด๋ฆฌํ๋ ํด๋ : ์ง์  ์ฌ์ฉ์๊ฐ ์๋๋ฉด ์๋ผ!

**docs**

**.gitignore**

**README.md**

> ์ ์ฅ์์์ ๊บผ๋ธํ์ผ ๋ฐ ๋๋ ํ ๋ฆฌ = ์์๋๋ ํ ๋ฆฌ โ์ํน ๋๋ ํ ๋ฆฌโ
> 

	commit : .git ์ผ๋ก

	.git ๊ณผ ์ํน ๋๋ ํ ๋ฆฌ ์ฌ์ด์์ ์ปค๋ฐํ๋ค!


### ๐ฅ3.3 Git ํ์ผ์ ์ํ ๋ณํ : ์ค๋์ ํต์ฌ

![Untitled](11%2021%20%E1%84%8B%E1%85%AF%E1%86%AF%20595de4f0cfdb4d89a101e616321572d1/Untitled.png)

- untracked : ์ ์ฅ์์ ์๋ ํ์ผ, ์์ง ์ถ์  ๋์ง ์์, ํ๋ฒ๋ ๋ฐฑ์ ๋์ง ์์๋ค.
- unmodified : ์ ์ฅ์์ ๋ค์ด์๋ ์ํ ๊ทธ๋๋ก์ธ ์ํ
- modified : ํ์ผ์ด ์์ ๋ ์ํ, add ๊ฐ ํ์ํ ์ํฉ
- staged : ๋ฐฑ์ ๋์์ด ๋ ์ํ, **git add ๋์ด** staging area์ snapshot์ ๋จ๊ธธ ์ ์๋ = ๋ฐฑ์์ด ์ค๋น๋ ์ํ
- committed : **git commit** ๋์ด ๋ฐฑ์๋ ์ํ, staged ๋ ํ์ผ๋ค๋ง ๋ฐฑ์๋๋ค.

<aside>
๐ก main = master
๋ฆฌํฌ ์ ์ฅ์๋ ๋ณ๊ฒฝ ๋ด์ญ์ ๊ด๋ฆฌํ๋ ๊ธฐ๋ณธ โํธ๋โ์ ๊ฐ์ง๊ณ  ์๋๋ฐ ์ด๊ฒ์ด โmainโ

</aside>

## 4. ์ค์ต & Git ๋ช๋ น์ด

---

### 4.1 git init : ๋ก์ปฌ์ ๊น ์ ์ฅ์ ๋ง๋ค๊ธฐ

```bash
# ํ์ฌ ๋๋ ํ ๋ฆฌ ์์น ์ถ๋ ฅ
pwd
# ๋ฆฌ์คํธ ๋ถ๋ฌ์
ls

# ~/git/bitcamp-ncp : git ์ ์ฅ์๋ก ๋ง๋ค๊ธฐ
mkdir bitcamp-ncp
cd bitcamp-ncp
git init 

# ์์ฑ ํ์ธ
ls -al
```

### 4.2 git config : ์ฌ์ฉ์ ์ด๋ฆ ๋ฐ ์ด๋ฉ์ผ ์ค์  โํ๊ฒฝ ์ค์ โ

```bash
- git์ ์ฌ์ฉ ํ๊ฒฝ์ ์ค์ ํ๋ค.
- /etc/gitconfig ์ค์  ํ์ผ
  - ์์คํ์ ๋ชจ๋  ์ฌ์ฉ์์ ๋ชจ๋  ์ ์ฅ์์ ์ ์ฉ๋๋ ์ค์ .
  - `git config --system` ์ต์์ผ๋ก ์ด ํ์ผ์ ์ฝ๊ณ  ์ด๋ค.
  - Windows OS์ ๊ฒฝ๋ก - C:/ProgramData/Git/config
- ~/.gitconfig, ~/.config/git/config ์ค์  ํ์ผ
  - ํน์  ์ฌ์ฉ์๋ง ์ ์ฉ๋๋ ์ค์ .
  - `git config --global` ์ต์์ผ๋ก ์ด ํ์ผ์ ์ฝ๊ณ  ์ด๋ค.
  - Windows OS์ ๊ฒฝ๋ก - C:/Users/์ฌ์ฉ์ํ/.gitconfig
- .git/config
  - ํน์  ์ ์ฅ์์๋ง ์ ์ฉ๋๋ ์ค์ .
  - `git config` ์ต์์ ์ง์ ํ์ง ์์ผ๋ฉด ์ด ํ์ผ์ ์ฝ๊ณ  ์ธ ์ ์๋ค.

	์1) ์ฌ์ฉ์ ์ด๋ฆ ์ค์ ํ๊ธฐ
	$ git config --global user.name "eomjinyoung"
	$ git config --global user.email "jinyoung.eom@gmail.com"

	์2) ๊ธฐ๋ณธ ํ์คํธ ํธ์ง๊ธฐ ์ค์ ํ๊ธฐ
	$ git config --global core.editor emacs

	์3) ์ค์  ํ์ธํ๊ธฐ
	$ git config -l
	$ git config --list

	์4) ํน์  ๊ฐ ํ์ธํ๊ธฐ
	$ git config user.name

```

### 4.3 .gitignore ํ์ผ

**git ์ ์ฅ์์ ๋ณด๊ดํ์ง ์์ ๋์์ ์ง์ ํ๋ค.**

๋๊ตฌ๋ฅผ ์คํํ  ๋ ๋ง๋ค ์๋ ์์ฑ๋๋ ํ์ผ ๋ฐ ํด๋ eg) .class, .exe, bin/, build/ ๋ฑ

<aside>
๐ก How to make .gitignore

- ๊ธฐ์กด ํ๋ก์ ํธ ์ ์ฅ์์ ์ค์ ๋ ํ์ผ์ ๊ฐ์ ธ์์ ํธ์งํ๋ ๋ฐฉ๋ฒ
- .gitignore  ํ์ผ์ ์๋ ์์ฑํด์ฃผ๋ ์ฌ์ดํธ๋ฅผ ์ด์ฉํ๋ ๋ฐฉ๋ฒ
    
    > gitignore.io
    > 
    > 
    > eg. windows macOS linux gradle java visualstudiocode eclipse
    > 
    > ๋ค๋ง ์ฐ๋ฆฌ๋ ๋ญ ๋ง๋ค์ง ๋ง์์ผ ํ ์งโฆ ๋ชจ๋ฅด์์
    > 
    > ๊ธฐ์กด ํ์ฌ ํ๋ก์ ํธ์ .gitignore ๋ฅผ ๋ณต๋ถํด๋ผ
    > 
</aside>

```bash
vi gitignore

# ์๋ ฅ๋ชจ๋
a 
# ๋ช๋ น๋ชจ๋
esc
# ์ ์ฅ
:w 
# ๋๊ฐ๊ธฐ
:q 

# ???????
cat .gitignore

# ๋๋ธ์๋ํฐ ์ค์น
sudo yum install nano -y

# .gitignore ์ค์ 
nano .gitignore
๋ถ์ฌ๋ฃ๊ธฐ!!

```

### 4.4 git ํ์ผ ์ํ๋ณํ ์ดํดํ๋ ์ค์ต : add/commit/status

```bash
[vagrant@host1 bitcamp-ncp]$ git status --short
?? .gitignore
?? a.txt
[vagrant@host1 bitcamp-ncp]$ git add .gitignore
[vagrant@host1 bitcamp-ncp]$ git status --short
A  .gitignore    A : staging area์ ๋ฑ๋ก ๋์๋ค
?? a.txt         ?? : untracked
```

```bash
[vagrant@host1 bitcamp-ncp]$ nano b.txt       nano ์๋ํฐ๋ก b.txt ์์ฑ : untracked
[vagrant@host1 bitcamp-ncp]$ git status --short
?? a.txt   ์์๋ฆฌ๋ staging area
?? b.txt   ๋ท์๋ฆฌ๋ working directory
[vagrant@host1 bitcamp-ncp]$ git add a.txt      untracked ๋ ํ์ผ stging area ์ ์ฌ๋ฆฌ๊ธฐ
[vagrant@host1 bitcamp-ncp]$ git status --short
A  a.txt                     A : staging area์ ๋ฑ๋ก ๋์๋ค
?? b.txt                     ?? : ์ฌ์ ํ untracked
[vagrant@host1 bitcamp-ncp]$ git commit -m "2"
[master a8426f5] 2
 1 file changed, 2 insertions(+)
 create mode 100644 a.txt
[vagrant@host1 bitcamp-ncp]$ git status --short          b.txt๋ ์ฌ์ ํ untracked ์ํ์ด๋ ์ค๋์ท์ด ๋จ์ง ์์
?? b.txt
[vagrant@host1 bitcamp-ncp]$

์ฌ๊ธฐ์ 
nano a.text 
์ ์ํด์ ์์  ํ๋ฉด : a.txt ๋ฒ์ ผ 2๋ก ๋ณ๊ฒฝ๋์์
git status --short ํ๋ฉด
_M : modified ๋ณ๊ฒฝ๋์๋ค, ์์ง ์๋ฒ์ ์ ์ฅ๋์ง ์์๋ค
๊ทธ๋ผ ๋ฐฑ์ํด์ผ์ง! 

[vagrant@host1 bitcamp-ncp]$ nano a.txt         staged๋ a.txt ๋ฅผ ๋ค์ ์์ ํด๋ณด์
[vagrant@host1 bitcamp-ncp]$ git status --short
 M a.txt                                       ์ํน๋๋ ํ ๋ฆฌ์์ modified๋ ์ํ
?? b.txt
[vagrant@host1 bitcamp-ncp]$ git add b.txt
[vagrant@host1 bitcamp-ncp]$ git status --short
 M a.txt
A  b.txt    ํ ์ํ์์ ์ปค๋ฐํ๋ฉด ์ํน์์ M์ํ์ธ a๋ ์ค๋์ท์ด ๋จ์ง์๋๋ค > staged ๋์ง ์์
[vagrant@host1 bitcamp-ncp]$ git commit -m "3"
[master debe282] 3
 1 file changed, 1 insertion(+)
 create mode 100644 b.txt
[vagrant@host1 bitcamp-ncp]$ git status --short
 M a.txt          M์ํ์ธ a๋ ๊ทธ๋๋ก ๋จ์์๊ณ , b๋ ์ฌ๋ผ์ง
[vagrant@host1 bitcamp-ncp]$ nano b.txt
[vagrant@host1 bitcamp-ncp]$ git status --short
 M a.txt
 M b.txt
[vagrant@host1 bitcamp-ncp]$ git add a.txt
[vagrant@host1 bitcamp-ncp]$ git status --short
M  a.txt   add ํ์ผ๋ staged ์ํ
 M b.txt
[vagrant@host1 bitcamp-ncp]$ git commit -m "4"
[master dcb1719] 4
 1 file changed, 2 insertions(+)
[vagrant@host1 bitcamp-ncp]$ git status --short
 M b.txt    a.txt๋ ์ปค๋ฐ ์๋ฃ, ํธ์ง์ค์ด์ง ์์ผ๋ a ์ฌ๋ผ์ง
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
  ์คํ์ด์ฆ๋ ๋๊ฒ ์์ผ๋ ์ค๋์ท์ ์ฐ์ ์ ์๋ค. add ๋จผ์ ! = ๋ฌด๋์ ๋จผ์  ์ฌ๋ฆด ๊ฒ staged
no changes added to commit (use "git add" and/or "git commit -a")
[vagrant@host1 bitcamp-ncp]$ git add b.txt
[vagrant@host1 bitcamp-ncp]$ git status --short
M  b.txt
[vagrant@host1 bitcamp-ncp]$ git commit -m "6"
[master dd9dd66] 6
 1 file changed, 1 insertion(+), 1 deletion(-)
[vagrant@host1 bitcamp-ncp]$ git status --short   
[vagrant@host1 bitcamp-ncp]$        ๋ฌผ๋ก  ์๋ฌด๊ฒ๋ ์์ด, 6๋ฒ ์ปค๋ฐ์ ํตํด b.txt๊ฐ 3์ด ๋์๋ค.
```

### 4.5 git log : ์ ์ฅ์์ ๋ณ๊ฒฝ ๋ด์ญ ์กฐํ

```bash
# ์ ์ฅ์์ ๋ณ๊ฒฝ ๋ด์ญ ์กฐํ / GUI๋ Soucetree ๋ง์ด ์

[vagrant@host1 bitcamp-ncp]$ git log     ์ต๊ทผ ๊ฒ ๋ถํฐ ์กฐํ๋จ
commit dd9dd668d205936da3a93856613b83cd576bc2a9     ์ปค๋ฐ ์ฒดํฌ์ฌ : ํด์ ์๊ณ ๋ฆฌ์ฆ์ ํตํด ์ง์ ๋ ํด์๊ฐ
Author: yun5ol <yunsol2095@gmail.com>    ์ปค๋ฐํ ์ฌ๋์ ์ด๋ฆ๊ณผ ์ด๋ฉ์ผ
Date:   Mon Nov 21 06:00:11 2022 +0000   ์ปค๋ฐํ ๋ ์ง > ์๊ตญ ์๊ฐ ๊ธฐ์ค +9์ ํ์

    6    ์ปค๋ฐ ๋ ์ธ๋ฑ์คํ ๋ด์ฉ

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

**๋ช๋ น์ด ์ฌ์ ๋ฆฌ**
# ?????
git log -p -2
# ์ปค๋ฐ ์ ๋ณด ํ๋ฒ์ ์กฐํ
git log --oneline
# ?????
git log --oneline --graph --all
```

๐ commit hash ๊ฐ ์ดํดํ๊ธฐ  = ๋ฐ์ดํฐ id = ๋์งํธ ์ง๋ฌธ

> **๋ฐ์ดํฐ์ ์์ด๋๋ฅผ ๋ถ์ฌํ๊ธฐ ์ํ ๊ฐ๋**
> 
> 
> ๊ฐ ํ์ผ์ ๋ณ๊ฒฝ ๋ด์ฉ์ hash ์๊ณ ๋ฆฌ์ฆ (๊ณ์ฐ) ์ ๋ฐ๋ผ ์ฐ์ฐ์ ์ํํ์ฌ ๋์จ ๊ฒฐ๊ณผ๊ฐ = hash code
> 
>  hash ์๊ณ ๋ฆฌ์ฆ : ๋ฐ์ดํฐ๋ฅผ ์๋ ฅ ๋ฐ์ ํด์๊ฐ์ return ํ๋ ์ํ ๊ณต์
> 
> hash code ๋ ๋ฐ์ดํฐ ํฌ๊ธฐ์ ์๊ด ์์ด 256bit, 512bit, 1224bit ๋ฑ์ ์ ์ ๊ฐ์ด๋ค.
> 

๋์งํธ ์ง๋ฌธ ์ฌ์ฉ ์ 2๊ฐ์ง

- ๋ฐ์ดํฐ ๊ณต์  ์ฌ์ดํธ
- ํ์ผ ๊ฒ์ฆ

### 4.6 git remote & pull & push & branch

**๋ก์ปฌ ์ ์ฅ์์ ์ฐ๊ฒฐ๋ ์๊ฒฉ ์ ์ฅ์๋ฅผ ํ์ธํ๊ฑฐ๋ ์ถ๊ฐํ๋ค.**

git clone ์ ํ ๋ฆฌํฌ์ง๋ง ๊ฐ๋ฅํ๋, remote ๋ก ๋ฉํฐ ์ฐ๊ฒฐ ๊ฐ๋ฅ

(์๋ฒ์์ ๋ง๋ค๊ณ  ๊นํด๋ก ์ด ๊ฐ์ฅ ์ฌํํด!)

๋ก์ปฌ ์ ์ฅ์์ ์๋ ๊ฑธ ์๋ฒ์ ์๋ก๋ ํด์ผํ๋ฉฐ > ์๋์์ฑ์ ์๋ค

```bash
[vagrant@host1 bitcamp-ncp]$ git remote   ์๊ฒฉ ์ ์ฅ์ ์ด๋ฆ์์๋ด๊ธฐ / ์๋ฒ์ ์ฐ๊ฒฐ๋ ์ ์ด ์์ผ๋ ์ ๋์
[vagrant@host1 bitcamp-ncp]$ git remote add origin https://github.com/yun5ol/bitcamp-ncp bitcamp-ncp ๋ฆฌํฌ์งํ ๋ฆฌ ๋ง๋ค๊ณ  ๋ก์ปฌ๊ณผ ์ฐ๊ฒฐํ๊ฒ ๋ค. ์๋ฒ์ด๋ฆ์ origin ์ผ๋ก ํ๊ฒ ๋ค
[vagrant@host1 bitcamp-ncp]$ git remote
origin
[vagrant@host1 bitcamp-ncp]$ git remote show origin
* remote origin
  Fetch URL: https://github.com/yun5ol/bitcamp-ncp
  Push  URL: https://github.com/yun5ol/bitcamp-ncp
  HEAD branch: main
  Remote branch:
    main new (next fetch will store in remotes/origin)
์ฒซ pull ํ  ๋ origin/main ์ฐ๊ฒฐ ํ์
ํด๋ก ์ด ์๋๋๊น ์ ํํ ์ง์ ์ด ํ์
๋จธ์งํ ๊ฒ ์์ผ๋ฉด ์ด๋ ๊ฒ ์ฐฝ์ด ๋ฌ๋ค
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

[vagrant@host1 bitcamp-ncp]$ git pull origin main   ์ต์ด 1ํ ์ฐ๊ฒฐ ํ์ / ๋ก์ปฌ ์ด๋ฆ์ด main์ด ์๋๋ผ master์ธ ์ํฉ

**merge ํ๋ฉด์์ esc > :wq**

# branch ์ด๋ฆ ๋ณ๊ฒฝ
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

## 5. ๊ณผ์  : 22์ผ ์์นจ๊น์ง

๋ก์ปฌ git ์ ์ฅ์๋ฅผ ๋ง๋ค๊ณ  [github.com](http://github.com) ๊ฐ์ธ ์ ์ฅ์์ ์ฐ๊ฒฐํ๋ผ

์์๋ด์ฉ: (host1 ๋ฆฌ๋์ค VM์์ ์์์ ์ํํ๋ค.)

1. ๋ค์์ ๊ฒฝ๋ก์ ๋ก์ปฌ ๊น ์ ์ฅ์๋ฅผ ์์ฑํ๋ค.
    
    ~/git/bitcamp-ncp2/
    
2. ๋ค์์ ํ์คํธ ํ์ผ์ ์์ฑํ๊ณ  ๋ก์ปฌ ์ ์ฅ์์ ์ปค๋ฐํ๋ค.
    
    ~/git/bitcamp-ncp2/a.txt
    
    a.txt ํ์ผ์ ๋ด์ฉ์ ์๋ฌด๊ฑฐ๋ ์๋ ฅํ๋ค.
    
3. github.com์ ๊ฐ์ธ ๊ณ์ ์ bitcamp-ncp2 ์ด๋ฆ์ผ๋ก ์ ์ฅ์๋ฅผ ์์ฑํ๋ค.
4. ๋ก์ปฌ ๊น ์ ์ฅ์์ ์๊ฒฉ ๊น ์ ์ฅ์๋ฅผ ์ฐ๊ฒฐํ๋ค.
5. ๋ก์ปฌ ๊น ์ ์ฅ์์ ๋ด์ฉ์ ์๊ฒฉ ์ ์ฅ์์ push ํ๋ค.

๊ณผ์  ์ ์ถ์ URL ๋ฃ๊ธฐ

```bash
# host 1 ์์

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
