# ๐ป HTML

๐ ๊ต์ฌ: Do it! ์นํ์ค์์ ์  
โ ์์์ค: In progress  
๐ท ํ๊ทธ: Dev, ์น&๋ชจ๋ฐ์ผ, ์นํ๋ก๊ทธ๋๋ฐ๊ธฐ์ด  
๐ ํ์ต์ผ: 11/23/2022  


## ๋ชฉ์ฐจ
1. HTML, HTTP
2. HTML ๊ธฐ๋ณธ ๊ตฌ์กฐ  
3. ๋ฒ์ธ  


## 1. HTML, HTTP


### 1.1 HTML, HTTP ๋ฑ์ฅ ์ 

- ํ๋กํ ์ฝ : ํต์  ๊ท์น > ๋ฐ์ดํฐ ์ก์์   file transfer protocol
- FTP client : ์นด์นด์คํก ํ๋ก๊ทธ๋จ
- FTP : ์๋ก ํ์ผ์ ์ฃผ๊ณ  ๋ฐ์ ๋์ ํ๋กํ ์ฝ

(๊ทธ๋ฆผ ์ถ๊ฐ ํ  ๊ฒ)

๋จ์  

1. ๋ผ๋ฌธ์ด ์ฐธ์กฐํ๋ ๋ค๋ฅธ ๋ผ๋ฌธ์ ๋ค์ด๋ก๋ ๋ฐ๊ธฐ ๋ฒ๊ฑฐ๋กญ๋ค.
2. ๋ผ๋ฌธ ์์ ๋ค๋ฅธ ๋ผ๋ฌธ์ด ์๋ก๋ ๋ ์๋ฒ ์ฃผ์๊ฐ ์๋ค. 

โฌ  (์์ฝ : ๋ผ๋ฌธ์ ์ํํ ์ฃผ๊ณ ๋ฐ์ผ๋ ค๊ณ  http ํ์ / ์ด http ์ ์ด๋ฅผ html)

### 1.2 HTML, HTTP ๋ฑ์ฅ ํ

์ ๋จ์  ๋ณด์์ ์ํด **๋ค๋ฅธ ๋ผ๋ฌธ์ ์์น์ ๋ณด๋ฅผ ์ฝ์ + ํ์คํธ์ ํฌ๋งท์ ์ง์ ** 

**(+ ์ถํ์๋ ๊ทธ๋ฆผ, ์์ฑ, ๋์์ ์ฝ์ +โฆ )**

โฌ ๋ณด์์ผ ์ํด ํ์ํ

- โ**Hyper Text** (๊ณ ๋ํ๋ ํ์คํธ)โ
    
    ๊ณ ๋ํ๋ฅผ ์ํด ๋ณ๋์ ํ์ (ํ์) ์ด ํ์ = **Markup** > **L**anguage ํ์
    
    **๊ณ ๋ํ๋ ๋งํฌ์ ์ธ์ด : HTML ์ ํ์**
    
    > **โMarkupโ**
    > 
    > 
    > ๋ฐ์ดํฐ๋ฅผ ์ค๋ชํ๋ ๋ฐ์ดํฐ, ๋ฐ์ดํฐ๋ฅผ ์ ์ดํ๋ ๋ฐ์ดํฐ = ๋ถ๊ฐ๋ฐ์ดํฐ = meta data 
    > 
    > 
- **HTTP** : Hyer-Text Transfer Protocol
    
    HTML ๋ฌธ์๋ฅผ ์ํํ๊ฒ ๋ฐ๊ณ ๋ค๋ฅธ HTML ๋ฌธ์๋ฅผ ์ฐพ์๊ฐ๊ธฐ ์ฝ๋๋ก ๋ง๋  ํต์  ํ๋กํ ์ฝ
    

### 1.3 HTTP client / server App.

์ก์์  ์์๋ 1. ํด๋ผ์ด์ธํธ์ ์์ฒญ 2. ์๋ฒ์ ์๋ต

- HTTP server (web server) : Apache HTTP server, NginX
    
    > web : HTML ๋ฌธ์๋ค์ ์ฐ๊ฒฐ๋ ๋ชจ์ต์ด ๊ฑฐ๋ฏธ์ค๊ณผ ๊ฐ๋ค
    > 
- HTTP client (web browser) : Chrome, Safari, Firefox, Edge ``` curl, wget
    
    ๋จ์ํ HTML์ ๋ค์ด๋ฐ๋ ๊ฒ๋ง์ด ์๋๋ผ HTML์ ์ถ๋ ฅํ๊ณ  ์ ์ดํ๋ ์ญํ ๋ ํ๋ค.
    
- HTTPS : HTTP + security ์ํธํ

### 1.4 web ๊ธฐ์ ์ ํ์ฉ

- [์น๊ธฐ์ ์ ๋ฑ์ฅ](https://www.notion.so/e6172fe100a24c7082c0ee3b63b6fc53)
- ์น๊ธฐ์  ํ์ฉ์ ๋ณํ
    
   ![์ด๋ฏธ์ง](https://user-images.githubusercontent.com/118426836/203512492-2b84aa93-7912-4d63-acb2-fc98d3a0d2b3.png)

### 1.5 Web Application ์ ์ ๊ธฐ์ 

**ํ๋ฉด ๋ง๋๋ ๊ธฐ์  โํ๋ก ํธ์๋ ๊ฐ๋ฐโ** 

![555ํ๋ฉด ์บก์ฒ 2022-11-23 183444](https://user-images.githubusercontent.com/118426836/203513456-9150abf4-9875-453f-82e4-488b11fdcc46.png)

 

## 2. HTML ๊ธฐ๋ณธ ๊ตฌ์กฐ

![image](https://user-images.githubusercontent.com/118426836/203512931-cd42e2cb-1ac1-4b14-8b02-33e1469b4fd5.png)



![44ํ๋ฉด ์บก์ฒ 2022-11-23 183616](https://user-images.githubusercontent.com/118426836/203513691-a520caaa-5337-45af-86f0-1bf91aeb101d.png)

- **HTML4 doctype**

[https://www.w3.org/TR/html4/sgml/dtd.html](https://www.w3.org/TR/html4/sgml/dtd.html)
![image](https://user-images.githubusercontent.com/118426836/203513089-83d63a52-17c1-4855-80af-925d4523173a.png)



> DTD : old
> 
> 
> Schema : new
> 
> ๋ฌธ์๊ท์น : ํ๊ทธ๋ฅผ ์ฌ์ฉํ๋ ๋ฐฉ๋ฒ. ์ด๋ค ํ๊ทธ๋ ์ด๋ ํ ๊ฒฝ์ฐ์ ์ฌ์ฉํ๋ผ!
> 

  
    
      
        
	
## ๋ฒ์ธ) ๊ธ์ผ ์ค์ต ์  ํ๊ฒฝ ์ค์ 


### git clone URL_[] : ๋ณ์นญ ๋ถ์ฌ์ ํด๋ก  ๊ฐ๋ฅ

```bash
C:\Users\bitcamp\git>git clone https://github.com/eomjinyoung/bitcamp-study bitcamp-ncp-teacher
Cloning into 'bitcamp-ncp-teacher'...
remote: Enumerating objects: 68, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (5/5), done.
Receiving objects: 100% (68/68), 27.90 MiB | 11.20 MiB/s, done.

Resolving deltas: 100% (21/21), done.
```

![Untitled](HTML%20e77d99514ac84dcfa4f742939dd8e52b/Untitled.png)
