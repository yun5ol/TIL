# ๐ CSS ์ฌ์ฉ๋ฒ

๐ ๊ต์ฌ: Do it! ์นํ์ค์์ ์  
โ ์์์ค: In progress  
๐ท ํ๊ทธ: Dev, ์น&๋ชจ๋ฐ์ผ, ์นํ๋ก๊ทธ๋๋ฐ๊ธฐ์ด  
๐ ํ์ต์ผ: 11/28/2022  

# ๋ชฉ์ฐจ
1. CSS

## 1. CSS

Cascading Style Sheet : HTML element ์ ๋ชจ์์ ์ ์ํ๋ค.  
๋ถ๋ชจํ๊ทธ์ ์คํ์ผ์ด ์์ํ๊ทธ์ ์์๋๊ฑฐ๋, ์ค์ฒฉ๋๊ธฐ๋ ํ๋ฉฐ,  
์์๋๋ ํ๊ทธ๊ฐ ์๋ ๊ฒ๋, ์๋ ๊ฒ๋ ์๋ค.  

![image](https://user-images.githubusercontent.com/118426836/204231887-6688f749-8987-4957-8cb0-8abbc063e2f1.png)


**< CSS ์ ํต์ฌ >**

- selector ์ฌ์ฉ๋ฒ !!
    - ์๋ ํฐ { ์คํ์ผ:๊ฐ; ์คํ์ผ:๊ฐ;โฆ }
    - ๋์ผํ ์คํ์ผ์ ๋ฃ์ผ๋ ค๋ ๋ฐ๋ณต์ด ๊ท์ฐฎ์์ SASS ๋ผ๋ ๋ณํ์ ์ฌ์ฉํ๊ธฐ๋
- specificity : ์คํ์ผ ์ ์ฉ ์์ !!
- box ๋ค๋ฃจ๋ ๋ฐฉ๋ฒ : ํ๋๋ฆฌ, ์ฌ๋ฐฑ, ๋ฐ์ค ๊ณ์ฐ๋ฒ
- ํฐํธ ๋ค๋ฃจ๋ ๋ฐฉ๋ฒ
- ์์ ์ง์  ๋ฐฉ๋ฒ
- ๋ฐฐ๊ฒฝ ๋ค๋ฃจ๋ ๋ฐฉ๋ฒ
- ๋ธ๋ก๊ณผ ์ธ๋ผ์ธ ๋ค๋ฃจ๋ ๋ฐฉ๋ฒ
- ์์น ์กฐ์ ํ๋ ๋ฐฉ๋ฒ

โฆ.. ๊ทธ ์ด์์ CSS ๊ณ ๊ธ์์ ๋ค๋ฃฐ ๊ฒ

### 1.1 Selector

- ์๋ ํฐ { ์คํ์ผ:๊ฐ; ์คํ์ผ:๊ฐ;โฆ }
- ๋์ผํ ์คํ์ผ์ ๋ฃ์ผ๋ ค๋ ๋ฐ๋ณต์ด ๊ท์ฐฎ์์ SASS ๋ผ๋ ๋ณํ์ ์ฌ์ฉํ๊ธฐ๋

| ์ข๋ฅ | ์์  |
| --- | --- |
| * { } |  |
| ํ๊ทธ๋ช { } | body { } |
| ํ๊ทธ๋ช, ํ๊ทธ๋ช, ํ๊ทธ๋ช { }  | img, ul { } |
| .๊ทธ๋ฃน๋ช { }  | .c1, .c2 { } |
| #ํ๊ทธ์์ด๋ { } |  #content { } |
| -[์์ฑ๋ช:๊ฐ] { } |  |
| -:์ํ๋ช { }    pseudo selector |  li:hover { } |

![image](https://user-images.githubusercontent.com/118426836/204231991-470640dd-149f-443a-bfe8-056477601806.png)


![image](https://user-images.githubusercontent.com/118426836/204230733-c3c11732-4302-4228-9fa2-494d396534af.png)


![image](https://user-images.githubusercontent.com/118426836/204232042-95b33017-140e-47a0-a5e9-da95d7777eda.png)

- ๋ถ๋ชจ ํ๊ทธ์ ์์ ํ๊ทธ์ ๊ณ์ธต ๊ตฌ์กฐ : UI๋ ์๋์ ๊ฐ์ด ์ฐจ๊ณก์ฐจ๊ณก ๊ณ์ธตํ๋จ

![image](https://user-images.githubusercontent.com/118426836/204230811-e10e5780-d97b-4f81-aec5-b1b448e6c243.png)

> body์ ๋ฐฐ๊ฒฝ์ ๊ทธ๋ ์ด๋ก ์ค์ 
> 
> 
> p๊น์ง ๋ฐฐ๊ฒฝ ์์์ด ์์ ๋  ํ๋ฐ, p์ ๋ค์ ํ๋ฒ ๋ฐฐ๊ฒฝ์ ์ค์ ?
> 
> ์ด๋ ๊ฒ ์ธ๋ฐ ์๋ ์ถ๋ ฅ์ ์ค์ด๋๊ฒ ์ค์! ํ๋ก ํธ์ค๋์ ๊ธฐ์ ์ด๋ค. =Virtual DOM????
> 

  
![image](https://user-images.githubusercontent.com/118426836/204232214-325e2979-a24a-4cdf-a66f-812a9dba991b.png)


![image](https://user-images.githubusercontent.com/118426836/204230895-55fbb0ac-1cb3-4efb-a500-cae1e3e505ce.png)
> liํ๊ทธ๋ ๋ธ๋กํ๊ทธ : ํ๋ผ์ธ ๋์   

![image](https://user-images.githubusercontent.com/118426836/204232376-fb7b4430-efdd-4886-8a6d-17f08af81337.png)


![image](https://user-images.githubusercontent.com/118426836/204231086-e1223ffa-af35-464f-8d01-d664815ed521.png)


![image](https://user-images.githubusercontent.com/118426836/204232469-2946fa07-aa1d-46de-a0ec-4dc5515059c0.png)

![image](https://user-images.githubusercontent.com/118426836/204231180-30447649-46f5-42dc-acb4-502880577d9f.png)
> โ๋ค์ ํ๊ทธโ์ ๊ฐ๋! โํ์ โ, ์์x  


![image](https://user-images.githubusercontent.com/118426836/204232794-fdbf9b86-0461-4ca2-9a50-c9fdeae95e12.png)
![image](https://user-images.githubusercontent.com/118426836/204232846-14c813e4-0079-477d-8c4a-fbb3bb7cbf0e.png)
![image](https://user-images.githubusercontent.com/118426836/204232905-42ded649-9d45-4919-b52a-91834daf28ee.png)


### 1.2 checkbox, radio, select
![image](https://user-images.githubusercontent.com/118426836/204233032-0d9c4c87-79b2-4d7c-8243-5e3997b918a4.png)
![image](https://user-images.githubusercontent.com/118426836/204233099-d789eed3-7f9e-4622-9fcc-6f8c08b3d9e8.png)


