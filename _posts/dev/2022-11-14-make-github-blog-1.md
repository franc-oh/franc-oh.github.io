---
layout: post
title: '깃허브 블로그 만들기 [1/2]'
subtitle: 깃허브 블로그에 대한 이해와 블로그 개발환경 구축
gh-repo: franc-oh/franc-oh.github.io/actions
tags:
  - (대분류) DEV
  - (소분류) git/github
comments: true
published: true
---


## 1. 깃허브 페이지와 깃허브 블로그

- - -

**깃허브 페이지**는 깃허브의 `{username}.github.io` 저장소에 있는 정적 웹 문서들을 무료로 호스팅 해주는 서비스로,
`https://{username}.github.io` 주소를 가진 나만의 웹 사이트를 만들 수 있다.  

**깃허브 블로그** 또한 블로그 웹 사이트를 개발하여, 깃허브 페이지를 통해 호스팅하는 방식으로 만들어진다.

<br/><br/>

## 2. 블로그 개발환경 셋팅 (MacOS 기반)

- - -

깃허브 블로그를 만들기 위해선 먼저 **Jekyll**과 **Ruby**를 설치해야 한다.

### 2-1. Jekyll이란?
- 마크다운 문서를 정적 웹 사이트로 만들어주는 Ruby기반의 프레임워크
- 깃허브 페이지 역시 Jekyll로 동작한다.
- Jekyll을 사용하면 깃허브 페이지와 동일한 환경에서 개발/빌드를 할 수 있다.
- **Jekyll 기반의 다양한 테마 오픈소스가 있어, 블로그 테마를 적용하기 수월하다.**

<br/>

### 2-2. Ruby 설치
먼저 Homebrew를 통해 `rbenv`를 설치한다.

```zsh
$ brew update
$ brew install rbenv ruby-build
```

<br/>

아래 명령어를 통해 결과를 확인

```zsh
# 입력
$ rbenv version

# 결과
* system
```

결과를 보면 현재 System Ruby를 사용하고 있다.  
System Ruby는 기본적으로 Mac에 설치된 Ruby로, OS에 종속된다.

이러한 이유로 Ruby를 독립적으로 사용할 수 있게 해주는 패키지인 `rbenv`를 별도로 설치했으며, 
위의 설정 또한 rbenv로 설치한 Ruby로 변경해야 한다.

<br/>

rbenv Ruby 설치 전, 설치 가능한 Ruby 버젼을 확인한다.  
`$ rbenv install -l`

![Ruby Version](https://drive.google.com/uc?export=view&id=16HeyrAxkUDri1qq77GKVaJZYZMDiWh6H)

<br>

버젼을 골라 설치한다.  
`$ rbenv install 3.1.2`

<br>

설치를 완료했다면, 아래 명령어를 통해 설치 결과를 확인한다.  
여전히 System Ruby로 설정된 상태지만, 신규 설치된 rbenv Ruby도 함께 보인다.

```zsh
# 입력
$ rbenv version

# 결과
* system
  3.1.2 (set by /Users/xxx/.rbenv/version)
```

<br>

명령어를 통해 Ruby 설정을 rbenv Ruby로 변경해준다.

```zsh
# 입력
$ rbenv global 3.1.2

# 결과
  system
* 3.1.2 (set by /Users/xxx/.rbenv/version)
```

<br>

마지막으로 쉘 설정 파일(.zshrc, .bashrc)에 rbenv PATH를 추가해준다.

```zsh
# 1. 쉘 설정 파일 편집
$ vim ~/.zshrc

# 2. 아래 내용을 설정 마지막에 추가 후 저장
[[ -d ~/.rbenv  ]] && \
  export PATH=${HOME}/.rbenv/bin:${PATH} && \
  eval "$(rbenv init -)"

# 3. 설정 적용
$ source ~/.zshrc
```

<br>

### 2-3. Jekyll 설치
명령어를 차례대로 입력하여 Jekyll을 설치한다.

```zsh
$ gem install jekyll bundler 
$ gem install webrick
```

Jekyll 설치를 완료했다면, 깃허브 블로그를 만들기 위한 준비가 모두 끝난 것이다.

<br><br>

## 🔎 참고
- [https://jojoldu.tistory.com/288](https://jojoldu.tistory.com/288)
- [https://wlqmffl0102.github.io/posts/Making-Git-blogs-for-beginners-1/](https://wlqmffl0102.github.io/posts/Making-Git-blogs-for-beginners-1/)
- [https://wlqmffl0102.github.io/posts/Making-Git-blogs-for-beginners-2/](https://wlqmffl0102.github.io/posts/Making-Git-blogs-for-beginners-2/)
- [https://www.irgroup.org/posts/jekyll-chirpy/](https://www.irgroup.org/posts/jekyll-chirpy/)