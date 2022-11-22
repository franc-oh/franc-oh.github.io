---
layout: post
title: '깃허브 블로그 만들기 [3/3]'
subtitle: 블로그 커스텀, 포스팅, 편의기능 붙이기
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

## 1. 블로그 커스텀

---

앞서 테스트로 블로그 타이틀 정도만 수정했을 뿐, 그 외 모든 정보가 테마의 디폴트 값으로 적용되어 있다.  
블로그 타이틀을 포함한 블로그 기본정보와, 메뉴 등을 내 입맛에 맞게 변경하여 나만의 블로그로 커스텀하려 한다.

### 1-1. 프로젝트 구조
커스텀에 앞서, 내려받은 프로젝트 구조에 대해 간략히 알아본다.  
Jekyll 테마를 적용했다면 기본적인 구조는 아래와 같을 것이다.

```text

[중요한 항목은 '*'로 표시]

_config.yml* : 
    - 해당 블로그에 대한 기본 설정정보를 관리한다.
    - 기본적으로 이 곳의 설정을 고치는 것만으로, 웬만한 커스텀 작업이 끝난다.    
  
_includes : 
    - 해당 블로그를 이루는 UI 모듈들이 포함
      . 헤더/푸터/메뉴바부터, 검색/댓글/데이터 분석 등의 편의기능까지...
    
_layouts :
    - 블로그의 기본 레이아웃 소스가 포함
    
_posts* :
    - 포스팅할 블로그 글들을 여기에 위치시킨다.
    - 해당 디렉토리의 글들은 자동으로 포스팅 된다.
    
assets/img* :
    - 블로그의 모든 이미지들을 보관하는 폴더
    - 기본적으로 백그라운드 이미지나 로고 등의 기본 이미지가 존재하며,
       앞으로 포스팅에 업로드 할 이미지 또한 여기서 관리한다.

index.html :
    - 블로그 메인화면으로, 보통의 경우 별도의 구현체를 참조만 한다. 
    - 테마에 따라 커스텀 해야 할 요소가 있을 수도 있다.

```

<br/>

### 1-2. 블로그 커스텀(_config.yml 수정)

기본적인 블로그 커스텀은 `_config.yml` 에서 이루어진다.  
아래는 내 블로그의 설정파일로, 테마에 따라 커스텀 할 수 있는 항목이 조금씩 다를 순 있지만, 기본적인 구조는 비슷하다.

아래 테마에서 제공하는 커스텀 항목들을 내 입맛대로 수정한다.

```yaml

############################
# --- 기본설정 --- #
############################

# 블로그 타이틀 (헤더 상단에 홈링크)
title: 5 Francs - Dev & Life

# 유저이름 (푸터에 노출)
author: Franc Oh


############################
# --- 로고 이미지 설정 --- #
############################
avatar: "/assets/img/avatar-icon.jpeg"
round-avatar: true

###############################################
# --- 네비게이션 바 구성 --- #
###############################################
navbar-links:
  Category : "tags"
  About: "aboutme"
  
########################################
# 푸터에 배치된 소셜네트워크 설정
#   - 'social-networks-links.html'
########################################

social-network-links:
  email: "franc-oh@naver.com"
  # rss: true
  github: franc-oh
  velog: franc
  #  twitter: daattali
  #  facebook: deanattali
  #  patreon: DeanAttali
  #  youtube: c/daattali
  
  ~ 중략 ~

```

<br/>

`_config.yml`의 몇가지 항목을 수정함으로써, 블로그의 빨간색 테두리로 표시된 부분이 커스텀됐다.  
(사진에는 나오지 않았지만, 로고 이미지 또한 내 이미지로 변경했다.)

![modify_config_result](https://drive.google.com/uc?export=view&id=14QsfaeUPeyRB808t493HxcFtP9YJB0AY&authuser)

테마들은 이와 같이 `_config.yml`를 통해 커스텀 할 수 있는 틀을 제공한다.  
'제공하지 않는 항목을 추가'하는 등 제공된 틀을 벗어나지만 않는다면, 소스 수정 없이 블로그 커스텀을 끝낼 수 있다.

<br/>
<br/>

## 2. 블로그 포스팅

---

블로그를 포스팅하는 방법은 다음과 같다.
1. 마크다운 양식(.md) 으로 작성한다.
2. 파일 이름은 `yyyy-mm-dd-제목.md` 형식으로 작성한다. 
3. `_posts` 폴더안에 위치시킨다.

<br>

한가지 유의할 점은, 글 머리 부분에 `YAML` 헤더를 넣어줘야 한다는 점인데,  
보통 '제목', '부제', '카테고리' 등의 정보를 여기서 설정한다.

```markdown

---
layout: post
title: '깃허브 블로그 만들기 [1/3]'
subtitle: 깃허브 블로그에 대한 이해와 블로그 개발환경 구축
gh-repo: franc-oh/franc-oh.github.io/actions
tags:
  - (대분류) DEV
  - (소분류) git/github
comments: true
published: true
---

~ 글 본문 작성 ~

```

테마에 따라 헤더에 설정할 수 있는 항목에 차이가 있을 수 있다.  
가장 좋은 방법은, 테마에서 샘플로 제공하는 글을 참고하는 방법이다.

<br/>

`YAML` 헤더를 통해 블로그 글 제목, 부제, 태그가 설정된 모습이다.

![blog_posting_yaml_header_result](https://drive.google.com/uc?export=view&id=14TMQJwQjlDy4p-WjqoMMukExxB8-piKl)

<br/>
<br/>

## 3. 편의기능 붙이기

---



### 3-1. Comment 기능 붙이기 (Disqus)

<br/>

### 3-2. 블로그 구글/네이버에서 검색되도록 설정

<br/>

### 3-3. Google Analytics

<br/>

### 3-4. 블로그 광고 붙이기

<br/>
<br/>

## 🔎 참고
- [https://wlqmffl0102.github.io/posts/Making-Git-blogs-for-beginners/](https://wlqmffl0102.github.io/posts/Making-Git-blogs-for-beginners-1/)
- [https://www.irgroup.org/posts/jekyll-chirpy/](https://www.irgroup.org/posts/jekyll-chirpy/)