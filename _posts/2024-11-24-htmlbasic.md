---
title: HTML - HTML에 기본 구조에 대해서 알아보자.
date: 2024-11-24 02:22:00 
categories: [Web, Frontend]
tags: [web, html]
---

vue.js를 공부하던 어느날 html, css, javaScript에 대한 이해가 너무 부족하다고 느끼게 되었고..기본기부터 새로 다시 시작하자는 생각으로 HTML 부터 다시 공부하게 되었다.

오늘은 HTMl에 구조에 대해 공부한 내용을 소개하겠다.

## 🏗️ **HTML에 구조**
HTMl에 기초 구성은 아래와 같이 생겼다.
```html
<!DOCTYPE html>
<html lang="en">
	<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
	</head>
	<body>
    
	</body>
</html>
```
이 구조를 기준으로 하나씩 뜯어보겠다.

### **DOCTYPE 태그**
```html
<!DOCTYPE html>
```
이 태그는 HTML **버전을 지정하는 태그**이다.

웹 표준 HTML 버전은 HTML 5 이며 별도에 문구가 더 없다면 HTML 5를 사용한다는 뜻이다.

### **html 태그** 
HTML이 어디에서 시작하고, 어디에서 끝나는지를 지정하는 코드이다.
```html
<html lang="en">
```
이때 lang 속성은 language에 줄임말로 웹 페이지에 언어를 설정한다.

en으로 설정할 경우 웹 페이지를 영문 웹 페이지로 브라우저가 인식하고 구글 번역기 사용 여부를 묻는데
```html
<html lang="ko">
```
이렇게 설정하면 브라우저가 한글 웹페이지로 인식해서 구글 번역기 사용 여부를 묻지 않는다.
### **head 태그**
HTML의 정보를 나타내는 태그이다.<br>

웹 브라우저가 해석해야할 웹 페이지의 제목, 설명 등등 **웹 페이지에 보이지 않는 정보를 작성하는 태그**이다. 
```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
```
그 안에 들어가있는 요소들을 하나씩 뜯어보면서 마저 설명하겠다.

**title 태그**

HTML의 제목을 지정하는 태그이다.
브라우저에서 웹 페이지를 열면 탭 부분에 나타나는 문자열을 정하는데
```html
<title>Hello</title>
```
위처럼 title 태그를 Hello로 작성하면<br>

![image](https://github.com/PetOfLSE/PetOfLSE.github.io/blob/main/assets/img/pagetab.png?raw=true)

이런식으로 브라우저 탭에 적용된다.

**meta 태그**

HTMl의 내용, 키워드 같은 여러 정보를 검색 엔진이나 브라우저에게 제공하는 역할을 한다.
```html
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
위처럼 사용된다.

**charset 속성**

문자 인코딩 방식을 지정한다.
> 문자 인코딩이란? <br>
> 문자나 기호들을 컴퓨터가 이해할 수 있게 변환시키는 것 

웹에서는 UTF-8을 권장한다.

**name 속성**

정보의 종류를 지정한다.

**content 속성**

정보의 값을 지정한다.

여기서 viewport를 가르키고 있는 meta 태그는 무슨 의미인지 알아보겠다.

**meta 태그에 viewport**

모바일에서 웹 페이지의 가로 너비를 모바일 환경의 가로 너비와 일치 시키거나 웹 사이트가 처음 출력될때 확대나 축소 여부 같은 것들을 결정한다. 

### **body 태그**
HTML의 구조를 나타내는 태그

사용자 화면을 통해 보여지는 로고, footer, header, 메뉴 와 같은 **웹 페이지의 보여지는 구조**를 나타낸다.

```html
<body>
  <h1>Hello hello</h1>
</body>
```
이런식으로 body 태그에 내용을 작성하면

![image](https://github.com/PetOfLSE/PetOfLSE.github.io/blob/main/assets/img/exampleh1.png?raw=true)

이런식으로 화면에 나타나는 구조를 body 태그에 작성한다.

## 🗂️ 정리
HTML의 기본 구조는 DOCTYPE, html, head, body 형식에 구조로 이루어져 있다.

DOCTYPE: html의 버전 지정
html: HTML의 시작과 끝 지정
head: 웹 페이지의 보이지 않는 정보 지정
body: 웹 페이지의 눈에 보이는 구조 지정

## 💭 느낀점
HTML에 기본 구조에 대해 알아보면서 사용할땐 모르고 그냥 넘어갔던 head 태그의 의미와 meta 태그에 사용에 대해 자세히 알고 넘어갈 수 있어서 좋았다.