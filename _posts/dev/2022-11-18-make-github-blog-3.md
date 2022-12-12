---
layout: post
title: '깃허브 블로그 만들기 [3/3]'
subtitle: 블로그 커스텀, 포스팅, 편의기능 붙이기
category: dev
tags:
- git|github
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

|파일명|설명|  
|:-----:|:-----|
| **_config.yml** | - 해당 블로그에 대한 기본 설정정보를 관리한다. <br/> - 기본적으로 이 곳의 설정을 고치는 것만으로, 웬만한 커스텀 작업이 끝난다.|   
| /_includes | - 해당 블로그를 이루는 UI 모듈들이 포함 <br/> - 헤더/푸터/메뉴바부터, 검색/댓글/데이터 분석 등의 편의기능까지... |
| /_layouts | 블로그의 기본 레이아웃 소스가 포함 |
| **/_posts** | - 포스팅할 블로그 글들을 여기에 위치시킨다. <br/> - 해당 디렉토리의 글들은 자동으로 포스팅 된다. |
| **/assets/img** | - 블로그의 모든 이미지들을 보관하는 폴더  <br/> - 기본적으로 백그라운드 이미지나 로고 등의 기본 이미지가 존재하며, 앞으로 포스팅에 업로드 할 이미지 또한 여기서 관리한다.
| index.html | - 블로그 메인화면으로, 보통의 경우 별도의 구현체를 참조만 한다. <br/> - 테마에 따라 커스텀 해야 할 요소가 있을 수도 있다. |

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

글의 본문은 마크다운 형식으로 작성, 마크다운 작성법은 [여기](https://velog.io/@yuuuye/velog-%EB%A7%88%ED%81%AC%EB%8B%A4%EC%9A%B4MarkDown-%EC%9E%91%EC%84%B1%EB%B2%95) 를 참조한다.  
이렇게 작성한 글을 깃허브에 푸시하면 블로그 포스팅이 완료된 것이다.

<br/>

`YAML` 헤더를 통해 블로그 글 제목, 부제, 태그가 설정된 모습이다.

![blog_posting_yaml_header_result](https://drive.google.com/uc?export=view&id=14TMQJwQjlDy4p-WjqoMMukExxB8-piKl)

<br/>
<br/>

## 3. 외부기능 붙이기

---

현재 내 블로그는 포스팅만 가능한 상황으로, 다음과 같은 점을 개선해야 한다.

1. **누군가 내 글에 댓글을 남길 수 있어야 한다.**
2. **내 블로그가 포털사이트에서 검색 되어야 한다.**
3. **내 블로그의 방문 현황을 집계하고 수치를 확인할 수 있어야 한다.**
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
구글은 [여기](https://search.google.com/search-console/welcome) 에서 설정할 수 있다.

<br/>

'Google Search Console'에 접속 > 'URL 접두어'에서 본인 블로그 URL을 기입하고 [계속]  
![google-search-console1](https://drive.google.com/uc?export=view&id=1loBMmdxFp9W4_nu1Kg6ttdTtnQzb3yu7)

<br/>

본인 블로그 URL을 기입하면, 해당 도메인이 본인 소유인지 인증하는 절차를 거쳐야 한다.  
소유권을 인증하는 방법은 여러 방법이 있지만, 구글에서 제시한 html 파일을 본인 블로그 소스에 넣어 인증하는 방법을 많이 사용한다.  

구글에서 제시한 html 파일을 다운 > 본인 소스에 업로드(Root 디렉토리) > 'Git Push'를 한다.  
![google-search-console2](https://drive.google.com/uc?export=view&id=1S8-ZlcdMQcOLpAn4ab0B1NY2l8gAT9ZF)  
![google-search-console3](https://drive.google.com/uc?export=view&id=1H28UBn8XKtzSoNOeBMSOf3K1Ylfo46DN)

<br/>

Git 저장소에 푸시까지 했다면, '소유권 확인' 화면으로 가서 [확인]을 누른다.  
아래와 같이 소유권 확인이 완료됐음을 알 수 있다.
![google-search-console4](https://drive.google.com/uc?export=view&id=18FLzpn1AIFb9JLh86uoq1-6GJ6EUfaFw)

<br/>

소유권을 인증했다면 포털사이트가 내 블로그를 크롤링할 수 있도록 `sitemap`을 생성해야한다.  
프로젝트에 있는 `Gemfile`으로 가서 아래 문구를 입력한다. 

`$ gem 'jekyll-sitemap'`

<br/>

그 다음 터미널에서 아래 명령어를 입력한다.  
`$ bundle install`

'jekyll-sitemap'이 설치된 것을 확인할 수 있다.
![google-search-console5](https://drive.google.com/uc?export=view&id=1iqQl-9eCDQskFvRhP5SCIyOX2fSYAvhw)

<br/>

Jekyll 서버를 재기동한 후, `http://localhost:4000/sitemap.xml` 로 접속한다.  
XML형식이 보인다면, 'Gemfile'과 동일한 위치에 `sitemap.xml` 파일을 생성하여 해당 내용 전체를 붙여넣는다.  
(본문의 'http://localhost:4000'은 본인 깃허브-페이지 URL로 변경한다.)

마지막으로 같은 위치에 `robots.txt` 파일을 생성하여 아래 내용을 입력, Git 저장소에 Push한다.  

```text

User-agent: *
Allow: /

Sitemap: https://{본인의 깃허브페이지 url}/sitemap.xml

```

<br/>

깃 저장소에 Push가 완료됐다면, [Google-Search-Console](https://search.google.com/search-console?hl=ko) 에서, 아래와 같이 sitemap.xml을 제출한다.  

![google-search-console5](https://drive.google.com/uc?export=view&id=1_ppa_gwUK8VmmJMITXX31wYF76A2tri9)

심사 등의 이유로 포털에 검색되기까지 몇 일 걸린다고 한다.  
일정기간 후 구글 검색창에 `site:{username}.github.io` 를 검색해서 결과를 확인한다.  
정상적으로 등록됐다면 본인의 블로그가 검색될 것이다.

(네이버의 경우 [여기](https://searchadvisor.naver.com/) 를 통해 설정)

<br/>

### 3-3. 집계/분석 기능 연동

내 블로그에 '얼마나 많은 사람이 방문했고, 언제/어떤 글을 많이 봤는 지' 등을 집계하고 데이터를 분석해주는 기능을 붙이려 한다.  
이 기능을 지원하는 툴로는 대표적으로 [Google Analytics](https://analytics.google.com/analytics/web/provision/#/provision) 가 있으며, 이 기능 역시 대부분의 Jekyll 테마가 설정을 통한 간단한 연동을 지원한다.

```yaml

###### ex. Beautiful Jekyll의 _config.yml

#################################
# --- Web Analytics Section --- #
#################################

# Fill in your Google Analytics gtag.js ID to track your website using gtag
#gtag: ""

# Fill in your Google Analytics ID to track your website using Google Analytics
google_analytics: ""

# Fill in your Cloudflare Analytics beacon token to track your website using Cloudflare Analytics
#cloudflare_analytics: ""

# Google Tag Manager ID
#gtm: ""

```

위 설정을 보면 Google Analytics 연동을 위해 추적_ID가 필요하다고 적혀있는데,  
가입 후에 부여받기 때문에, 일단 가입부터 한다.  

<br/>

'계정이름'은 식별이 가능한 문구를 기입한다.  
(ex. 'my-gh-blog')
![google-analytics1](https://drive.google.com/uc?export=view&id=1T6fcTvIh6UbUUQxZcKe4vT4BlH-ViC9Z)

'속성 설정'은 아래와 같이 기입/설정 후 [고급 옵션 보기] 클릭
![google-analytics2](https://drive.google.com/uc?export=view&id=1OkyIAPHR30L2FbOIrKnF4IaatIeHgYQn)

'유니버설 애널리틱스 속성'을 활성화 후, 아래 형식으로 주소 기입하고 [다음] 클릭
![google-analytics3](https://drive.google.com/uc?export=view&id=1YXvkg2q08hKIlAr_w_Xhs1nktcfNilbd)

어떤목적으로 사용하는지에 대해 묻는 단계로, 의도에 맞게 설정한다.
![google-analytics4](https://drive.google.com/uc?export=view&id=19v3bHJbjPL6xitcOmvF-D6CErz3Oqcv9)

마지막으로 약관 동의만 하면 생성이 완료되는데, 추적_ID는 다음과 같이 찾을 수 있다.   
![google-analytics5](https://drive.google.com/uc?export=view&id=1mUvN1uOvAgkHM45gCn9AYQvRCkrKjyRc)  
![google-analytics6](https://drive.google.com/uc?export=view&id=129JskuRduWG7QGdGeME6EmRtQ8aHC0xL)  
![google-analytics7](https://drive.google.com/uc?export=view&id=1p6l2Wd1CpWz0RaVoiDl-N6IT3U3JpeKJ)  
![google-analytics8](https://drive.google.com/uc?export=view&id=15bngwXAA1JF1K4yquKrHZy-NmSg6hIGK)  

<br/>

추적ID를 아래 `_config.yml`에 붙여넣고, Git 저장소에 푸시한다.

```yaml

###### ex. Beautiful Jekyll의 _config.yml

#################################
# --- Web Analytics Section --- #
#################################

# Fill in your Google Analytics ID to track your website using Google Analytics
google_analytics: "측정 ID"

```

<br/>

푸시 후 블로그에 접속해본다.  
아래와 같이 방문 내역이 집계되는 걸 확인할 수 있다.

![google-analytics9](https://drive.google.com/uc?export=view&id=1Jt4bz8g7V79YAH3KjTXQjD0q07M950Fb)

현재는 단순히 '언제/어디에/얼마나' 방문했는지 정도만 집계되는 상태다.   
하지만 별도의 작업을 통해 '행동 패턴' 등의 딥한 데이터 수집도 가능하니, 뜻이 있다면 이를 적절히 활용하도록 한다.

<br/>

이 외에도 블로그에 광고를 노출해, 수익을 창출할 수 있는 'Google Adsense' 도 연동이 가능하다.  
나의 경우 포스팅 수가 너무 적으면 승인이 안난다는 얘기가 있어서 추후 적용 할 예정이다.

<br/>
<br/>

## 🔎 참고
- [https://wlqmffl0102.github.io/posts/Making-Git-blogs-for-beginners/](https://wlqmffl0102.github.io/posts/Making-Git-blogs-for-beginners-1/)
- [https://www.irgroup.org/posts/jekyll-chirpy/](https://www.irgroup.org/posts/jekyll-chirpy/)
- [https://velog.io/@yuuuye/](https://velog.io/@yuuuye/velog-%EB%A7%88%ED%81%AC%EB%8B%A4%EC%9A%B4MarkDown-%EC%9E%91%EC%84%B1%EB%B2%95)