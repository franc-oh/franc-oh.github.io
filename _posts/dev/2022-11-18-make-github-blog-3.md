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
[3. 블로그 커스텀, 포스팅, 편의기능 붙이기](/2022-11-18-make-github-blog-3)

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

글의 본문은 마크다운 형식으로 작성, 마크다운 작성법은 <u>[여기](https://velog.io/@yuuuye/velog-%EB%A7%88%ED%81%AC%EB%8B%A4%EC%9A%B4MarkDown-%EC%9E%91%EC%84%B1%EB%B2%95)
</u>를 참조한다.  
이렇게 작성한 글을 깃허브에 푸시하면 블로그 포스팅이 완료된 것이다.

<br/>

`YAML` 헤더를 통해 블로그 글 제목, 부제, 태그가 설정된 모습이다.

![blog_posting_yaml_header_result](https://drive.google.com/uc?export=view&id=14TMQJwQjlDy4p-WjqoMMukExxB8-piKl)

<br/>
<br/>

## 3. 외부기능 붙이기

---

현재 내 블로그는 포스팅만 가능한 상황으로, 다음과 같은 점을 개선해야 한다.

1. 누군가 내 글에 댓글을 남길 수 있어야 한다.
2. 내 블로그가 포털사이트에서 검색 되어야 한다.
3. 방문자 수, 조회 수를 집계하고 수치를 확인할 수 있어야 한다.
4. 블로그에 광고를 붙여 수익을 창출할 수 있어야 한다.

네이버 블로그나 티스토리와 같은 블로그 사이트에서는 신경쓰지 않았던 점들을, 깃허브 블로그에서는 직접 구현해야 한다.  
그나마 다행인건, 이러한 점들을 쉽게 해결할 수 있는 외부기능이 존재한다는 점과, 대부분의 Jekyll 테마에서 이러한 외부기능들을 쉽게 연동할 수 있도록 대비를 해놨다는 점이다.

<br/>

### 3-1. 댓글 기능

대부분의 Jekyll 테마에서는 외부기능을 쉽게 연동할 수 있도록 대비가 되어있다.  
`_config.yml`에서 어떤 외부기능을 사용할 수 있는지 확인할 수 있다.

```yaml

###### ex. Beautiful Jekyll의 _config.yml

####################
# --- Comments --- #
####################

## 댓글 시스템 (Disqus)
# To use Disqus comments, sign up to https://disqus.com and fill in your Disqus shortname (NOT the userid)
#disqus: ""

## 댓글 시스템 (Facebook Comments)
# To use Facebook Comments, create a Facebook app and fill in the Facebook App ID
#fb_comment_id: ""

## 댓글 시스템 (CommentBox)
# To use CommentBox, sign up for a Project ID on https://commentbox.io
#commentbox: "" # Project ID, e.g. "5694267682979840-proj"

~~ 그외 몇 가지 ~~

```

위 예시처럼 대부분의 Jekyll 테마는 설정만으로, 자동으로 기능이 연동되도록 개발된 상태다.  
(`_config.yml`에 설정이 없거나, 지원하는 기능 외의 기능을 사용할 경우 직접 코딩을 해야 한다.)

위의 예시를 보면 댓글기능을 제공하는 툴에는 'Disqus', 'Facebook Comments', 'CommentBox' 등이 있다는 것을 유추해볼 수 있다.  
이중에서 사용하고 싶은 툴을 골라, 설정에 필요한 값을 부여받아야 한다.

나의 경우 보편적으로 많이 사용하는 'Disqus'를 연동하려 한다.  
Disqus 연동에 필요한 'shortname'은 가입 시 입력하게 되는 ID값이며,  
가입 후 '[Disqus Admin](https://disqus.com/admin/) > Settings' 메뉴에서 확인할 수 있으니 찾아서 설정에 추가한다.

![disqus1](https://drive.google.com/uc?export=view&id=1_yvqOxwd_MlfosQcvpAKDx9zNaw17Kbd)


```yaml

####################
# --- Comments --- #
####################

# 댓글 시스템 (disqus)
# To use Disqus comments, sign up to https://disqus.com and fill in your Disqus shortname (NOT the userid)
disqus: "'shortname' 기입"

```

<br/>

설정에 추가 후 로컬 Jekyll 서버를 재기동하면, 아래와 같이 댓글 기능이 활성된 것을 확인할 수 있다.

![disqus2](https://drive.google.com/uc?export=view&id=1QsZXJhqWL_BJSea_vH0H_mfTDu4ZocV8)

이처럼 대부분의 테마는 웬만한 기능은 간단한 설정만으로 해결될 수 있도록 기능을 제공한다.

<br/>

### 3-2. 블로그가 구글에서 검색되도록 설정

지금 블로그는 깃허브-페이지를 통해 호스팅 되고 있는 상태지만, 포탈사이트에서 검색은 되지 않는다.  
이런 문제는 각 포탈사이트가 제공하는 서비스와 연동하여 해결할 수 있다.

국내에서 많이 사용하는 검색엔진은 '네이버'와 '구글'이다.  
두 포털사이트 모두 별도의 서비스를 통해 내 블로그가 검색엔진에 노출되도록 설정할 수 있는데,  
구글은 [여기](https://search.google.com/search-console/welcome) , 네이버는 [여기](https://searchadvisor.naver.com/) 에서 설정할 수 있다.

<br/>

**[구글]**  

'Google Search Console'에 접속 > 'URL 접두어'에서 본인 블로그 URL을 기입하고 [계속]  
![google-search-console1](https://drive.google.com/uc?export=view&id=1loBMmdxFp9W4_nu1Kg6ttdTtnQzb3yu7)

<br/>

본인 블로그 URL을 기입하면, 본인 소유인지 소유권을 확인하는 작업을 거쳐야 한다.  
소유권을 인증하는 방법은 여러 방법이 있지만, 구글에서 제시한 html 파일을 본인 블로그 소스에 넣어 인증하는 방법을 많이 사용한다.  

구글에서 제시한 html 파일을 다운 > 본인 소스에 업로드(루트 디렉토리) > 'Git Push'를 한다.  
(인증 전까진 '소유권 확인' 창을 닫지 않는다.)  
![google-search-console2](https://drive.google.com/uc?export=view&id=1S8-ZlcdMQcOLpAn4ab0B1NY2l8gAT9ZF)

![google-search-console3](https://drive.google.com/uc?export=view&id=1H28UBn8XKtzSoNOeBMSOf3K1Ylfo46DN)


<br/>

### 3-3. Google Analytics

<br/>

### 3-4. 블로그 광고 붙이기

<br/>
<br/>

## 🔎 참고
- [https://wlqmffl0102.github.io/posts/Making-Git-blogs-for-beginners/](https://wlqmffl0102.github.io/posts/Making-Git-blogs-for-beginners-1/)
- [https://www.irgroup.org/posts/jekyll-chirpy/](https://www.irgroup.org/posts/jekyll-chirpy/)
- [https://velog.io/@yuuuye/](https://velog.io/@yuuuye/velog-%EB%A7%88%ED%81%AC%EB%8B%A4%EC%9A%B4MarkDown-%EC%9E%91%EC%84%B1%EB%B2%95)