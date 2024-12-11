---
title: Vue.js - Vue에 기본 구조에 대해서 알아보자.
date: 2024-12-07 11:01:00 
categories: [Web, Frontend]
tags: [vue, directory]   
---

스위프트 기본 문법을 다 공부하고 UI로 넘어가려던 미뤄두었던 Vue.js 공부가 시급해졌다. <br>
어쩔 수 없이 Vue.js를 다시 공부하게 되었고...제대로 배우고 싶은 마음에 기초부터 배우기 시작했다.

오늘은 Vue.js에 파일 구조에 대해서 알아보자.

## **Vue.js 디렉토리 구조**

구조
```
📦vue-learn
 ┣ 📂.vscode
 ┃ ┣ 📜extensions.json
 ┃ ┗ 📜settings.json
 ┣ 📂public
 ┃ ┗ 📜favicon.ico
 ┣ 📂src
 ┃ ┣ 📂assets
 ┃ ┃ ┣ 📜base.css
 ┃ ┃ ┣ 📜logo.svg
 ┃ ┃ ┗ 📜main.css
 ┃ ┣ 📂components
 ┃ ┃ ┣ 📂icons
 ┃ ┃ ┃ ┣ 📜IconCommunity.vue
 ┃ ┃ ┃ ┣ 📜IconDocumentation.vue
 ┃ ┃ ┃ ┣ 📜IconEcosystem.vue
 ┃ ┃ ┃ ┣ 📜IconSupport.vue
 ┃ ┃ ┃ ┗ 📜IconTooling.vue
 ┃ ┃ ┣ 📜HelloWorld.vue
 ┃ ┃ ┣ 📜TheWelcome.vue
 ┃ ┃ ┗ 📜WelcomeItem.vue
 ┃ ┣ 📜App.vue
 ┃ ┗ 📜main.js
 ┣ 📜.gitignore
 ┣ 📜README.md
 ┣ 📜index.html
 ┣ 📜jsconfig.json
 ┣ 📜package.json
 ┗ 📜vite.config.js
```

처음 Vue 프로젝트를 생성하면 이런식으로 뷰 프로젝트가 생성된다.<br>
뭔가 복잡하게 느껴지지만 이 파일들 중에서 중요한 파일들은 4가지 정도로 볼 수 있다.

이제 파일들에 대해서 자세하게 파보자.

## **index.html**
index.html은 뷰 프로젝트를 실행하면 제일 먼저 로드되는 파일이다.<br>
이 파일에 내용은 아래와 같다.

index.html
```html
<!DOCTYPE html>
<html lang="en"> 
  <head>
    <meta charset="UTF-8">
    <link rel="icon" href="/favicon.ico">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vite App</title>
  </head>
  <body>
    <div id="app"></div>
    <script type="module" src="/src/main.js"></script> 
  </body>
</html>
```
위 코드처럼 생겼다. 

이제 코드를 하나씩 뜯어보면서 살펴보자.

```html
<html lang="en"> 
```
뷰 프로젝트에 index.html 파일은 언어가 영어로 설정되었디. 그닥 중요한 부분은 아니지만 구글 번역기가 자꾸 실행되는게 거슬린다면 ``ko``로 바꾸는 것을 추천한다.

```html
<div id="app"></div>
```
위 코드는 아주아주아주 중요하다. 아래에서 마저 살펴보겠지만 이 부분은 id 속성의 값이 ``app`` 인 HTML 요소를 루트 컴포넌트로 지정하는 부분이다.

> 루트 컴포넌트란?<br>
> 뷰 프로젝트가 최초로 로드하는 최상위 컴포넌트 

```html
<script type="module" src="/src/main.js"></script> 
```
뷰 프로젝트에 핵심인 main.js 파일을 불러오는 코드이다.
## **main.js**
뷰 프로젝트를 구성하는 굉장히 중요한 파일이다.

뷰 프로젝트를 처음 생성하면 기본적으로 생성되는 main.js파일의 구조는 아래와 같다.

main.js
```javascript
import './assets/main.css' 

import { createApp } from 'vue' 
import App from './App.vue' 

createApp(App).mount('#app') 
```
이제 코드를 하나씩 뜯어보겠다.

```javascript
import './assets/main.css' 
```
컴포넌트들에 적용시킬 main.css 파일을 불러오는 코드이다.

```javascript
import { createApp } from 'vue' 
```
vue 인스턴스를 생성할 수 있게 해주는 ``createApp`` 메서드를 vue 패키지에서 불러오는 코드이다.

```javascript
import App from './App.vue' 
```
App.vue 파일을 불러오는 코드이다.

```javascirpt
createApp(App).mount('#app') 
```
사실상 제일 중요한 부분이다.

``createApp`` 메서드를 사용해서 vue 인스턴스를 생성하는데 매개변수로 App.vue를 전달는데 이때 전달되는 파일이 루트 컴포넌트가 된다.

또한 ``mount`` 메서드를 사용해서 id 값이 ``app``인 요소에 추가되고 있다.

index.html
```html
<!DOCTYPE html>
<html lang="en"> 
  <head>
    <meta charset="UTF-8">
    <link rel="icon" href="/favicon.ico">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vite App</title>
  </head>
  <body>
    <div id="app"></div>
    <script type="module" src="/src/main.js"></script> 
  </body>
</html>
```

위 index.html 코드에서

```html
<div id="app"></div>
```
이부분에 들어가게 된다.

## **App.vue**
기본적으로 루트 컴포넌트로 지정되는 파일이다.<br>
App.vue은 처음생성되었을 때 아래와 같이 구성된다.

App.vue
```html
<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
```

위 코드처럼 구성된다. 이상한점이 하나 있다면 한 파일 안에 html, css, js가 모두 포함되어있다는 것이다.

이것은 vue만에 독자적인 형식으로 SFC(Single File Component) 라고 한다.

이제 각 영역을 하나씩 뜯어보자.

```html
<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>
```
위 코드처럼 ``<script>`` 영역에는 자바스크립트 문법이 들어간다.<br>
일반 자바스크립트와 대부분 유사하지만 vue가 사용하는 형식에 맞춰서 사용해야한다.

```html
<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>
```
위 코드처럼 ``<template>`` 태그 안에 html 코드를 작성할 수 있다.

```html
<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
```

위 코드처럼 ``<style>`` 태그에는 css 코드가 들어간다.

## **package.json**
vue 프로젝트에 기본 정보, 모듈 정보, 명려엉 정보를 담고 있는 파일이다.

package.json
```json
{
  "name": "vue-learn",
  "version": "0.0.0",
  "private": true,
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "vue": "^3.5.13"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^5.2.1",
    "vite": "^6.0.1",
    "vite-plugin-vue-devtools": "^7.6.5"
  }
}
```
이중에서 중요한 몇가지만 알아보자.

```json
"scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  }
```
vue 프로젝트를 빌드하거나 실행하는 명령어를 등록하는 코드이다.

```json
"dependencies": {
    "vue": "^3.5.13"
  }
```
프로덕션 환경에서 vue 프로젝트를 실행할 때 필요한 모듈들을 정의하는 부분이다.

> 프로덕션이란?<br>
> 프로젝트를 배포하고 서비스하는 단계를 뜻한다.

```json
"devDependencies": {
    "@vitejs/plugin-vue": "^5.2.1",
    "vite": "^6.0.1",
    "vite-plugin-vue-devtools": "^7.6.5"
  }
```
개발 환경에서 필요한 모듈들을 정의하는 부분이다.

## **정리**
vue 프로젝트에서 중요한 파일은 index.html, main.js, package.json, App.vue 이며 다른 파일들이 중요하지 않은 것이 아닌 상대적으로 더 중요한 파일들이다.

index.html: 프로젝트를 실행할 때 가장 먼저 로드되는 파일

main.js: 프로젝트를 구성하는 역할을 하는 파일

package.json: 프로젝트의 기본 정보, 모듈 정보 등을 담고있는 파일

App.vue: 기본적으로 루트 컴포넌트로 지정되는 파일 SFC 구조를 따른다.

## **느낀점**
아무것도 모를때 처음 배웠을때는 어렵게 느껴졌는데 다시 배우니까 확실히 이해가 안됬던 부분들이 이해가되기 시작했고 엄청 쉽게 느껴졌다.