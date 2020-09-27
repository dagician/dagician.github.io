---
title: 깃허브 블로그 만들기(2) - Google Analytics
author: dagician
date: 2020-09-08 19:00:00 +0900
categories: [git, github page]
tags: [github page, 깃허브 페이지, 깃허브 블로그]
toc: true
pin: false
comments: true
published: true
---

지난번 만든 Gihub 블로그에 Google Analytics를 적용해 보도록 하겠습니다.

전체 과정은 꽤 심플합니다.

1. Google Marketing Platform 에서 GA 계정을 생성하고
2. GA 와 깃허브 블로그를 연동합니다.

그럼 시작해보도록 하겠습니다.

<br>



# GA 계정 생성

1. https://analytics.google.com/
   으로 이동하여 '측정 시작' 클릭
2. '계정이름' 입력하고 '다음' 클릭
3. '웹' 선택하고 '다음' 클릭
4. 웹사이트 이름 : ㅇㅇ 블로그
   웹사이트 URL : xxx.github.io
   업종 카테고리 : 인터넷 및 통신
   보고 시간대 : 대한민국
5. '만들기' 선택

<br>



# 깃허브 블로그 연동

1. GA 계정을 생성하고 관리자 화면의 상단에 **추적 ID** 를 복사합니다.
2. 깃허브 블로그 repository 의 _config.yml 파일을 수정합니다.

```python
# /_config.yml

...

google_analytics:
  id: '추적 ID 붙여넣기'  # UA-123456789-1

...
```

<br>



# 연동 성공

![image](../../assets/img/posts/Ubuntu로-Github-블로그-만들기(2)/01.png)











