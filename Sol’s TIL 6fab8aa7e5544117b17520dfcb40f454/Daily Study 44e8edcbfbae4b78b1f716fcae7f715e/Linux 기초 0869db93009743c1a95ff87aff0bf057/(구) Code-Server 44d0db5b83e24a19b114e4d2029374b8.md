# (구) Code-Server

## 설치

---

- cd /opt
    
    /opt 로 이동
    이곳이 뭐하는 곳인지는 검색하셈
    
- wget [https://github.com/cdr/code-server/releases/download/v3.3.1/code-server-3.3.1-linux-x86_64.tar.gz](https://github.com/cdr/code-server/releases/download/v3.3.1/code-server-3.3.1-linux-x86_64.tar.gz)
    
    [https://github.com/cdr/code-server/releases](https://github.com/cdr/code-server/releases) 최신 버전을 다운로드
    (2020.05.25 기준 최신 버전임)
    
- tar xf [code-server-3.3.1-linux-x86_64.tar.gz](https://github.com/cdr/code-server/releases/download/3.0.0/code-server-3.0.0-linux-x86_64.tar.gz)
    
    압축 풀기
    
- mv [code-server-3.3.1-linux-x86_64](https://github.com/cdr/code-server/releases/download/3.0.0/code-server-3.0.0-linux-x86_64.tar.gz) code-server
    
    이름 바꾸기
    
- cd code-server
- mkdir data extensions
- nano /etc/systemd/system/code-server.service
    
    ```jsx
    [Unit]
    
    Description=Visual Studio Code Server
    
     
    
    [Service]
    
    Environment="PASSWORD=비밀번호"
    
    Environment="PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/opt/code-server"
    
    WorkingDirectory=/opt/code-server
    
    User=root
    
    Group=root
    
    Type=simple
    
    ExecStart=/opt/code-server/code-server --auth password --extensions-dir /opt/code-server/extensions --user-data-dir /opt/code-server/data --locale ko-KR --cert --host 0.0.0.0 --port 포트번호
    
    Restart=always
    
     
    
    [Install]
    
    WantedBy=multi-user.target
    ```
    
- systemctl daemon-reload
    
    
- systemctl start code-server
- systemctl status code-server

또는

`./code-server --host 0.0.0.0 --port 8096`

접속 주소는 [https://ip](https://ipaddr/)주소:포트

---

## 임시 작성 구간

```prolog
[Unit]

Description=Visual Studio Code Server

 
[Service]

Environment="PASSWORD=phw030700_v"

Environment="PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/opt/code-server"

WorkingDirectory=/opt/code-server

User=root

Group=root

Type=simple

ExecStart=/opt/code-server/code-server --auth password --extensions-dir /opt/code-server/extensions --user-data-dir /opt/code-server/data --locale ko-KR --cert --host 0.0.0.0 --port 2096

Restart=always

 

[Install]

WantedBy=multi-user.target
```