---
layout: post
title: '깃허브 블로그 만들기 [2/3]'
subtitle: 블로그 웹 페이지 구현과 호스팅
gh-repo: franc-oh/franc-oh.github.io/actions
tags:
  - (대분류) DEV
  - (소분류) git/github
comments: true
published: true
---

### 시리즈

[1. 깃허브 블로그에 대한 이해와 블로그 개발환경 구축](/2022-11-14-make-github-blog-1)  
[2. 블로그 웹 페이지 구현과 호스팅](/2022-11-16-make-github-blog-2)  
[3. 블로그 커스텀, 포스팅, 편의기능 붙이기](/_ready/dev/2022-11-18-make-github-blog-3.md)

<br/>

## 1. Jekyll 테마

---

### 1.1 Jekyll 테마 선택

많은 사람이 지킬을 사용하는 만큼, 수많은 테마가 존재한다.  
여기서 테마라는 것은 디자인적인 부분에만 국한된 것이 아닌, 블로그 프로젝트 그 자체를 의미한다.

예를 들어 '티스토리 스타일' 테마를 적용한다는 것은, 티스토리 디자인과 기능이 구현된 프로젝트를 내려받는 것이다.   
사용자는 그저 테마가 제공하는 틀 안에서 커스텀하고 글을 쓰기만 하면 된다.

<br/>

다양한 지킬 테마들을 한 곳에서 볼 수 있는 사이트는 아래와 같다.

- [https://jekyllthemes.io/free](https://jekyllthemes.io/free)
- [http://themes.jekyllrc.org/](http://themes.jekyllrc.org/)
- [https://github.com/topics/jekyll-theme](https://github.com/topics/jekyll-theme)

![Jekyll Theme Site](https://drive.google.com/uc?export=view&id=1NHpAHx3nIKKoppcW46_3MN9kJKtn83vx)

<br/>

**테마를 선택할 때는 자기만의 기준을 가지는 게 좋다.**  
나의 경우 [Beautiful Jekyll](https://github.com/daattali/beautiful-jekyll) 을 선택했는데, 아래의 기준을 충족했기 때문이다.  

1. 검색기능 : 블로그는 나의 Doc이기도 하다. 급하게 참고해야 하는 경우를 대비해 검색 기능은 필수로 있어야 했다.
2. 가독성 : 개취의 영역, 개인적으로는 어느정도 여유있는 행간이 보기 좋았다.
3. 카테고리를 나눌수 있어야 함 : 직접적인 카테고리 기능을 제공하진 않지만, 벨로그 처럼 Tag로 구분해서 그룹핑이 가능
4. 많은 사람이 사용하는 테마 : 아무래도 인기가 많은 만큼, 적용 시 참고할 수 있는 글도 많을 것 같았다.

<br/>

### 1.2 Jekyll 테마 적용

테마를 적용하는 방법은 크게 두가지다.

1. github에서 fork 받기
2. 테마 소스를 zip으로 받아 직접 설치

(나의 경우 설치 순서 상 '1'의 방법으로 적용했다.)

<br/>

선택한 테마의 저장소로 가서, Fork > ‘Create a new fork’ 선택

![Fork Theme1](https://drive.google.com/uc?export=view&id=1MjArPVZN6UIzMfEDdBxOyA48V8Dxcpbt)

<br/>

내 저장소로 fork

![Fork Theme2](https://drive.google.com/uc?export=view&id=1jUY-O9d43ra29-gBCMsEF9CKJhhmiPLe)  
![Fork Theme3](https://drive.google.com/uc?export=view&id=1z-PUECA19Q7RSmypsZWZLX2sHvmt4O3n)

<br/>

깃허브 페이지의 도메인은 `https://{userName}.github.io` 다.  
따라서 Repository 이름 또한 `{userName}.github.io` 으로 변경해야 한다.


‘Settings’ > ‘General’ 에서 `{userName}.github.io` 로 변경 후 ‘Rename’

![Fork Theme4](https://drive.google.com/uc?export=view&id=1iAaEuHreGjeMPWnp7rboT8C1WRoZ_d-x)  
![Fork Theme5](https://drive.google.com/uc?export=view&id=1akRhND9Eb2UXH6kSYDOMKCG3dGy66Z2M)

<br/>

## 2. 개발 및 배포

---

현재 깃허브 저장소에 내 블로그가 만들어진 상태다.  
이제 남은 일은 블로그 타이틀 등의 기본정보 수정 및 메뉴 구성과 같은 커스텀 작업과, 블로그 글 작성 뿐이다.

앞서 로컬에 Jekyll 개발환경도 구성했기 때문에, 위의 작업은 로컬에서 개발/테스트 할 수 있다.  
우선 **저장소의 소스를 로컬로 클론 받는다.**

<br/>

### 2-1. 로컬에서 개발 및 테스트

터미널 실행 후 클론 받은 프로젝트 소스 경로로 이동, 아래의 명령어를 입력한다.  
(해당프로젝트가 의존하는 모든 모듈을 설치)  
`$ bundle`

<br/>

모듈 설치가 모두 끝났다면 다음 명령어를 통해 Jekyll 서버를 실행시킨다.  
`$ bundle exec jekyll serve`

![Jekyll Server Run1](https://drive.google.com/uc?export=view&id=1dv8U6MPJdKiUTcz4YrrGrSkZiuGk-c1g)

❓ `in 'require': cannot load such file -- webrick (LoadError)` 에러 발생 시  
&nbsp;&nbsp;&nbsp;&nbsp; ⇒ `$ bundle add webrick` 명령어 실행 후 Jekyll 서버 재실행

<br/>

http://localhost:4000 으로 접속하면 내가 적용한 테마의 블로그 화면이 나타난다.

![Jekyll Server Run2](https://drive.google.com/uc?export=view&id=1k_NOl13W-wSPsOMVneIHmZ3uCqZ1Ll9o)

<br/>

로컬에서 실행되는 것을 확인하니, 이 화면을 실제 서비스인 '깃허브 페이지'를 통해 보고 싶어진다.   
깃허브 페이지 호스팅 전, 간단하게 타이틀 정도만 변경하여 배포하려 한다. 

타이틀 수정을 위해 프로젝트에서 ‘config.yml’을 연다.  
‘config.yml’은 블로그의 기본설정 파일로, 블로그 타이틀과 메뉴 구성 등의 설정을 담당하는 파일이다.  

타이틀을 변경하고 Jekyll 서버를 재실행하여 변경내용을 확인해본다.

![Modify Title1](https://drive.google.com/uc?export=view&id=1SKVTbpuuIMMzQbCHVtNPz8QYtH1ZIOZ1)  
![Modify Title2](https://drive.google.com/uc?export=view&id=1F2zSRQBgbAsWUqbPxOP3qsC7HLQd5orL)

<br/>

### 2-2. 깃허브 페이지 호스팅 및 배포

깃허브 페이지 호스팅을 위해 깃허브에서 설정을 아래와 같이 변경한다.  

‘Settings > Pages’로 이동, ‘Branch’ 항목 `root`로 변경 후 [Save]

![Gh-pages Hosting1](https://drive.google.com/uc?export=view&id=1LKVJhsmlqkDRQUs8fVD4jeYnHHrgrJAA)

<br/>

이제 내 블로그가 서비스 되기 위한 준비는 모두 끝났다.  
배포를 위해 로컬의 변경사항을 원격 저장소로 푸시한다.

![Gh-pages Hosting2](https://drive.google.com/uc?export=view&id=1_RFQuOsMfeLDLsUc42TuQ26rfP6POyru)

<br/>

푸시 후 깃허브에서 ‘Actions’ 탭을 클릭, 작업 상태를 확인한다.  
깃허브 페이지의 경우 저장소 커밋 뿐만 아니라, page build와 deployment도 같이 수행한다.  
(적용되기까지 1~2분에서 5분이상 걸릴 때도 있다.)

![Gh-pages Hosting3](https://drive.google.com/uc?export=view&id=1SOXz6CClDldsaZgOKDtF0e8G02-smbbw)

<br/>

아래와 같이 정상적으로 커밋이 완료됐다면, `https://{userName}.github.io` 로 접속,  
로컬에서 봤던 결과물이 그대로 보인다면, 깃허브 블로그가 정상적으로 개설된 것이다.

![Gh-pages Hosting4](https://drive.google.com/uc?export=view&id=1m_urc2CvvfmjhNUwMu4RndGsy2ICbW_v)  
![Gh-pages Hosting5](https://drive.google.com/uc?export=view&id=1YFGcza_LLiZwsqdRxd1I1mMU2R866ptX)

<br/>
<br/>

## 🔎 참고
- [https://wlqmffl0102.github.io/posts/Making-Git-blogs-for-beginners/](https://wlqmffl0102.github.io/posts/Making-Git-blogs-for-beginners-1/)
- [https://www.irgroup.org/posts/jekyll-chirpy/](https://www.irgroup.org/posts/jekyll-chirpy/)