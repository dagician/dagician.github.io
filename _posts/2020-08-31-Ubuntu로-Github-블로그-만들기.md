---
title: Ubuntu로 Github 블로그 만들기
author: dagician
date: 2020-08-31 00:42:00 +0900
categories: [git, github page]
tags: [github page, 깃허브 페이지, 깃허브 블로그]
toc: true
pin: false
comments: true
published: true


---

과거 깃허브 블로그를 만들어야겠다는 생각이 들어 이런 저런 정보를 찾아봤지만 포기했었다.  

이왕 블로그를 시작한다면 당연히 예쁘게 만들고 싶었지만 필자의 디자인 능력이 거의 전무하기에 만들어진 테마를 이용하고자 했고, 가장 유명한 jekyll 테마를 적용하려 했지만 윈도우에서 jekyll을 공식적으로 지원하지 않아 결국 tistory 블로그를 이용할 수밖에 없었다.

그런데 비오는 주말, 할 일 없이 유튜브만 보며 낄낄거리다 문득 깃허브 블로그 만들기에 재도전 해보면 어떨까 하는 생각이 들었고 결론부터 말하자면 여러 삽질 끝에 결국 설치에 성공했다.

<br>

## Virtual box + Ubuntu + Jekyll + git = 깃허브 블로그

내가 성공한 방법은 위 방법이다.

결국 윈도우에서는 막히는 부분이 너무 많았고 microsoft store에 있는 Ubuntu app 앱을 이용해 설치해 봤지만 포스팅과 소스의 수정이 필요할 경우 파일 편집과 이동에서 귀찮은 과정들이 자주 발생했다.  결국 Ubuntu 내에서 직접 수정 하고 바로 화면을 확인 하려면 리눅스 GUI 환경을 구성하는게 좋겠다고 생각해 위 조합을 선택했다.

<br>

## Virtual box & Ubuntu 설치

이 영상을 참고했다.

[Windows에 설치된 VirtualBox 6.1을 사용하여 Ubuntu 20.04 설치하기](https://www.youtube.com/watch?v=gj1sU2Qs9y4)

성격 급한 나에게 딱 맞게, 쓸데없는 설명 없이 설치법만 알려주는 고마운 영상이었다.


<br>

## Ruby 설치

- 업데이트

```
sudo apt-get update
```

<br>

- 루비 설치

```
sudo apt-get install ruby-full build-essential zlib1g-dev
```

<br>

- 터미널에 다음과 같이 입력한다. `.bashrc` 파일을 수정하는 코드이다.

```
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

<br>

- 마지막으로 지킬 설치!

```
gem install jekyll bundler
```

<br>

## 테스트 블로그 만들어보기!

- 블로그 만들기 (현재 폴더에 myblog 라는 이름의 블로그 project 프로젝트 폴더가 만들어진다.)

```
jekyll new myblog
```

<br>

- 폴더 이동

```
cd myblog
```

<br>

- 사이트 빌드 및 로컬 서버 실행

```
bundle exec jekyll serve
```

<br>

- 접속

http://localhost:4000

명령 프롬프트에서 ctrl + c 를 눌러 서버를 종료한다.

<br>

## 깃 계정 생성 & 연동

깃허브 페이지를 만들겠다고 마음먹은 사람이라면 깃 계정정도는 있을테니 pass!
(깃 계정을 만들고 설정하는 내용은 다른 포스트를 참고하도록 한다.)

<br>

- Ubuntu 쉘에서 깃 설치

```
sudo apt-get install git
```

<br>

- git global config

```
git config --global user.name "username"
git config --global user.email "user@example.com"
```

<br>

- ssh-keygen

```
# 홈 디렉토리로 이동
cd ~

# ssh 키 생성
ssh-keygen

# 파일 내용 조회
vi .ssh/id_rsa.pub
```

`id_rsa.pub` 의 모든 내용을 복사해서 깃허브 사이트의 ` 사용자 아이콘 > Settings > SSH and GPG keys > new key` 로 이동한뒤 적당한 타이틀을 입력, key에는 복사한 내용을 입력해준다.

리눅스에 공인인증서를 만들고, 그 공인인증서를 깃에 등록했다고 생각하면 될 것이다.

<br>

## jekyll 테마 적용

구글에서 jekyll theme 이라 검색하면 이 사이트가 나온다.
http://jekyllthemes.org/


나는 chirpy 테마를 선택했다.

가장 상단에 있는 테마라 아무 생각없이 설치해봤는데 생각보다 예뻐서 이 녀석으로 결정!



jekyll의 테마들은 github에 올라가 있다. README.md 파일에 Installation 부분부터 잘 확인해보자

- Fork 받기

``` 
https://github.com/cotes2020/jekyll-theme-chirpy/fork
```

<br>

- git clone

```
git clone git@github.com:<username>/jekyll-theme-chirpy -b master --single-branch
```

<br>

- 프로젝트 폴더로 이동하고 bundle 설치

```
cd jekyll-theme-chirpy

bundle install
```

<br>

- coreutils 설치

```
sudo apt-get install coreutils
```

<br>

- 서버 실행

```
bundle exec jekyll serve
```

<br>

- 접속

http://localhost:4000

<br>

## 포스팅

`_posts` 폴더에 있는 기존 포스팅을 복사해서 새로운 포스팅을 만든 후 적당한 내용을 입력한다.

- 깃에 변경 사항을 커밋

```
git add -A
git commit -m "first commit"
git push
```

<br>

- 퍼블리싱 명령을 통해 자동으로 카테고리와 태그 파일을 생성할 수 있다.

```
bash tools/publish.sh
```

<br>

- 로컬 서버 실행

```
# 1. 테마에서 제공하는 방법
bash tools/run.sh

# 2. 지킬에서 제공하는 방법
bundle exec jekyll serve

# 두 방법 다 가능하지만 개인적으로는 2번 방법을 좀 더 선호한다.
```



- 접속
  http://localhost:4000