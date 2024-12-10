---
title: Error - Docker 사용 똑같은 테이블 생성 오류 해결 
date: 2024-12-11 00:01:00 + 09:00
categories: [Error, Docker]
tags: [error, solved, docker]   
---

프론트 공부를 뒤로하고 백엔드로 프로젝트를 만들던 중 도커로 MySql을 띄우는데 자꾸 전에 생성했던 테이블이 재생성되는 오류가 발생했다.

급하게 해결하느라 사진은 따로 찍지 못했다..

어쨌든 해결 방법은 아주 간단했다

```
docker-compose down -v 
docker-compose up -d
```

위 명령어를 통해서 해결이 가능하다

```
docker-compose down -v
```
위 명령어를 사용해서 모든 컨테이너를 중단시킨 후 

```
docker-compose up -d
```
위 명령어를 사용해서 다시 실행시켰더니 해결되었다.


