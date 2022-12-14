# โญ Linux ๊ธฐ์ด

๐ท ํ๊ทธ: Ops, ํด๋ผ์ฐ๋OS, ํด๋ผ์ฐ๋์ธํ๋ผ  
๐ ํ์ต์ผ: 11/18/2022

# ๋ชฉ์ฐจ
1. ๋ฆฌ๋์ค ์ค์น
2. ์ค์ต
3. ํด์ฆ

## 1. ๋ฆฌ๋์ค ์ค์น


### 1.1 VirtualBox ๋ฐ Vagrant ์ค์น

๋จผ์  Hypervisor ์ธ ๋ฒ์ถ์ผ ๋ฐ์ค๋ฅผ ์ค์นํ๊ธฐ ์ ,

๊ณ์ธตํ๋ ๊ฐ์ ๊ตฌ์กฐ์ ๋ ํธ๋ฆฌํ๊ณ  ์๋ํ๋ฅผ ์ํ ์ถ๊ฐ ํ๋ก๊ทธ๋จ์ด ํ์ํ๋ค.

๊ทธ๊ฒ์ **Vagrant** ๋ผ๊ณ  ํ๋ค.

- VirtualBox๋ฅผ ๋ช๋ น์ด(CLI)๋ก ์ ์ดํ๋ ํ๋ก๊ทธ๋จ(App.)
    
    vagrant๋ฅผ ์ฌ์ฉํ๋ฉด ๋ช๋ น์ด ๋์ค๋ก ๊ฐ๋จํ vm ์ค์น, ์์ฑ์ด ๊ฐ๋ฅํ๋ค.
    

![image](https://user-images.githubusercontent.com/118426836/202899206-99b91874-59c9-4d01-9eeb-7b5bd15fa2bb.png)
> ๊ณ์ธตํ layerd ๋ ๊ฐ์ ๋คํธ์ํฌ, ๊ฐ์ ๊ณ์ธต ๊ตฌ์กฐ ๋ชจ๋ธ๋ง  

![image](https://user-images.githubusercontent.com/118426836/202899245-545f53f1-dd04-4890-a16f-923c70af2f78.png)
> ๋ฒ์ธ์ผ๋ฐ์ค์ ํจ๊ป ๊ตฌ๋๋  vagrant

1. **VirtualBox ์ค์น**
    - [Downloads โ Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads) ์ ์
    - ๋ฒ์ ์ ๋ง๋ ํ์ผ ๋ค์ด๋ก๋ ๋ฐ ์ค์น
    - install ์งํ์ด ์ ๋  ๋ [์ง์๋๋ ์ต์  Visual C++ ์ฌ๋ฐฐํฌ ๊ฐ๋ฅ ํจํค์ง ๋ค์ด๋ก๋ | Microsoft Learn](https://answers.microsoft.com/en-us/windows/forum/all/microsoft-visual-c-redistributable-2019-x64/a2af45bb-85ce-4ab0-8318-e7be90b17725) ์์ Visual C++x64 ๋ค์ด๋ก๋ ํ ์ฌ์ค์น
2. **Vagrant ์ค์น**
    - [Downloads | Vagrant by HashiCorp](https://www.vagrantup.com/downloads) ์ ์
    - ๋ฒ์ ์ ๋ง๋ ํ์ผ ๋ค์ด๋ก๋ ๋ฐ ์ค์น

### 1.2 VM ์์ฑ ๋ฐ CentOS ์ค์น

VirtualBox์ Vagrant๊ฐ ์ค์น๋์์ผ๋ฉด, VM์ ์์ฑํ๊ณ  ๊ทธ ์์ ์ฌ๋ฆด ์ด์์ฒด์  CentOS/7 ์ ์ค์นํ๋ค.
![image](https://user-images.githubusercontent.com/118426836/202899304-0addd199-ca46-49d3-b4cd-6d6f707742e1.png)

1. **Vagrant ๋ก VM ์์ฑ**
    1. **๋๋ ํ ๋ฆฌ ์์ฑ**
    2. **VagrantFile ์์ฑ**
        
        : VM์ ์ธ๋ถ ์ค์ ์ ์ ์ํ๋ค. (๋คํธ์ํฌ, ์ฉ๋, ํธํธ์ด๋ฆ ๋ฑ๋ฑ) 
        
        ```
        vagrant init -m "cenetos/7" : VagrantFile ์์ฑ
        ```
        
2. **OS ์ด๋ฏธ์ง ๋ค์ด๋ก๋ ๋ฐ VM ์์ฑ, ์ค์น**

        
        vagrant up : VagrantFile ํตํ ๊ฐ์๋จธ์  ์์ฑ
        

1. **VM SSH ์ ์ : ์๋ฒ ์ ์**
    1. ๊ฐ์ ๋จธ์  ์ ์ ํ์ธ
        
        ํ์ฌ vmํ๋ก์ ํธ๊ฐ ์์ฑํ๊ณ  ์คํ ์ค์ธ ์๋ฒ์ ์ ์๋จ
        

### 1.3 ๊ธฐ๋ณธ์ ์ธ vagrant ๋ช๋ น์ด ์ ๋ฆฌ

    
    # ๊ฐ์๋จธ์  ๊ธฐ๋
    vagrant up
    # ๊ฐ์๋จธ์  ์ํ ํ์ธ
    vagrant status
    # ๊ฐ์๋จธ์  ์ค๋จ
    vagrant status
    # ๊ฐ์๋จธ์  ์ ๊ฑฐ
    vagrant destroy
    # ๊ฐ์๋จธ์  ์ ์
    vagrant ssh
    # ์ ์ ์ํ์์ ๋ค๋ฅธ ๊ฐ์๋จธ์  ์ด์์ํ ๋ฐ id ํ์ธ
    vagrant global-status
    # ์ ์ ์ํ์์ ๋ค๋ฅธ ๊ฐ์๋จธ์  ์ค๋จ
    vagrant halt <id>
    # ์๋ฒ์์ exit
    exit
    

## 2. ์ค์ต


### 2.1 VM ์๋ฒ์ด๋ฆ ๋ณ๊ฒฝ

**VagrantFile ์ ํธ์งํ๋ค**

    - ssh ์๋ฒ ์ ์ ํ, ํธ์คํธ๋ช ํ์ธ

    
    vagrant ssh
    hostname

    #VagrantFile ํธ์ง
    config.vm.hostname=""

    eg.
    **config.vm.hostname = "myhost3.bitcamp"** 
   

### 2.2 VM ์์ฑ ๋ฐ ์ค์ 

1. centos vm ์ค์  (virtual box)
2. centos vm ์คํ
3. ํธ์คํธ๋ช ๋ณ๊ฒฝ > โmyhost3.bitcampโ

### 2.3 VM ์ถ๊ฐ ์์ฑ ๋ฐ git ๊ฐ์ธ ํ์ด์ง ๋ณ๊ฒฝ

1. **centos5 vm ์์ฑ**
    1. vm-projects์ centos5 ๋๋ ํ ๋ฆฌ ์์ฑ
    2. VagrantFile ์์ฑ
    3. log ๋ถ์ฌ๋ฃ๊ธฐ & ํธ์คํธ์ด๋ฆ ์ค์ 
    4. VM ์คํ
2. **centos5 vm ์ ์**
3. **git ๊ฐ์ธ ํ์ด์ง ๋ณ๊ฒฝ**
    1. git ์ค์น
    2. nano ์๋ํฐ ์ค์น
    3. git config ์ name & email ์ค์ 
    4. [README.md](http://README.md) ํธ์ง
    5. git commit & push
    
    โจ nano ์๋ํฐ
    
    ```
    # ์๋ฒ ์ ์ ์ํ์์
    sudo yum install git -y
    # complete ํ ๋ฒ์  ํ์ธ
    git --version
    # print working directory : ํ์ฌ ๋๋ ํ ๋ฆฌ๋ฅผ ์๋ ค์ฃผ๋ ๋ช๋ น์ด
    pwd
    
    mkdir git
    cd git
    git clone <URL>
    
    sudo yum install nano editor -y
    cd yunol.github.io
    nano README.md
    
    # Your Name ์ ๋ณ๊ฒฝํด์ฃผ์ธ์
    git config --global user.name "Your Name"
    # user@email.com ์ ๋ณ๊ฒฝํด์ฃผ์ธ์
    git confit --global user.email "user@email.com"
    git add -A
    git commit -m ""
    git push
    ```
    

    ```
    # ๋ฆฌํฌ์งํ ๋ฆฌ clone  
    git clone <URL>
    # Your Name ์ ๋ณ๊ฒฝํด์ฃผ์ธ์
    git config --global user.name "Your Name"
    # user@email.com ์ ๋ณ๊ฒฝํด์ฃผ์ธ์
    git confit --global user.email "user@email.com"
    # ์ปค๋ฐ ํ์ผ ์ถ๊ฐ
    git add -A
    # ์ปค๋ฐ ๋ฐ ์ธ๋ฑ์ค ์ถ๊ฐ
    git commit -m โmessageโ
    # push
    git push origin main

    vagrant init -m "cenetos/7" : VagrantFile ์์ฑ
    vagrant up : Vagrantfile ์ ํตํ ๊ฐ์ ๋จธ์  ์์ฑ

    dir : ๋ก ํ์ธ

## 3. ํด์ฆ 

- 11.21.์ ์ค์   
- ์์ ๋ด์ฉ:

    1. VirtualBox์ Vagrant ๋๊ตฌ๋ฅผ ์ด์ฉํ์ฌ ๋ก์ปฌ์ ๋ฆฌ๋์ค ๊ฐ์ ๋จธ์ ์ 3๊ฐ ์์ฑํ์์ค.
    2. ๊ฐ ๊ฐ์ ๋จธ์ ์ ์ด๋ฆ์ host1.bitcamp, host2.bitcamp, host3.bitcamp ๋ก ์ค์ ํ์์ค.
    3. ๊ฐ ๊ฐ์ ๋จธ์ ์ "https://github.com/eomjinyoung/bitcamp-study" ์ ์ฅ์๋ฅผ ๋ณต์ ํ์์ค.

    ๋ณต์ ํ ์ ์ฅ์์ ์์น: ~/git/bitcamp-study

    ```
    # ๋๋ ํ ๋ฆฌ ์์ฑ
    # Vagrantfile ์์ฑ > ์๋ฒ์ด๋ฆ ํจ๊ป ์์  : log ๋ถ์ฌ๋ฃ๊ธฐ
    vagrant init -m ""

    vagrant up

    # ์๋ฒ ์ ์
    vagrant ssh

    # ์๋ฒ ์ด๋ฆ ํ์ธ
    hostname

    # git ์ค์น ๋ฐ ๋ณต์  ~/git/bitcamp-study ์ ๋ง๋๋๊ฒ ์ค์
    mkdir git
    cd git
    sudo yum install git -y
    git clone https://github.com/eomjinyoung/bitcamp-study

    # ํ์ธ
    git ssh
    hostname
    cd bitcamp-study
    ls : docs README. ํ์ธ ๊ฐ๋ฅ
    pwd : /home/vagrant/git/bitcamp-study
    ```
