---
layout: post
title: "Setting Github Blog with Chirpy"
date: 2024-01-26 10:00:00 +0900
categories: [Blogging]
tags: [Jekyll, Chirpy]
---

# Chirpy 테마로 깃허브 블로그 개설하기

[윈도우용 기본적인 가이드 블로그](<https://devpro.kr/posts/Github-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0-(1)/>)  
[윈도우용 트러블슈팅 가이드 블로그](https://ree31206.tistory.com/entry/github-pages-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0-%ED%85%8C%EB%A7%88-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0Chirpy)  
[커스터마이징 가이드 블로그](https://www.irgroup.org/posts/jekyll-chirpy/)

- 다른 분들도 어느 정도는 파일들을 만져서 기본 설정값을 많이 바꾸셨겠지만 Chirpy 테마 파일도 버전이 있는건지 여러 다른 블로그들에서 적용한 것과 내가 적용한 파일에 차이가 있는 것으로 보인다. 잘 찾아서 설치해야 할 것 같다. 물론 아무거나 설치한 후 폴더를 뒤져서 수정하면 상관없긴 하다.
- Jekyll이 32bit라서 Ruby를 설치할 때 x86으로 골라서 설치하라는 말을 어떤 블로그에서 봤는데 다른 블로그에서는 또 상관없이 x64로 설치하신 것을 보고 어쩌다가 x86 → x64 → x86으로 3번 설치해봤는데 x64로 설치했을 때 상당히 많은 오류를 마주했고... 결국 32bit 버전으로 다시 설치했다. 32bit로 설치하시길 바란다.
- 먼저 `jekyll new ./`를 하고 난 후 로컬 폴더에 생기는 파일들 중 404.html, about.markdown, index.markdown 3개를 먼저 없앤다. 그 후에 Chirpy 테마 파일들을 복사해서 붙여넣기 한다. 이걸 하지 않으면, 실행했을 때 2개의 파일들이 하나의 페이지를 가리키는 문제가 생긴다. 이 파일들 말고 삭제해야 하는 폴더들은 위 링크들에 잘 나와있다.
- Jekyll은 윈도우를 공식적으로 지원하지 않는다. 그래서 윈도우에서 하다가 오류가 생겨도 할말은 없지만... 그래도 윈도우에서 써야하기 때문에 몇가지 트러블슈팅이 필요하다. 특히, 리눅스에서의 init 명령어를 쓰지 않으면 js파일이 assets/js/dist에 생기지 않는 등 골치아픈 오류가 생기는데 위 블로그 링크에서 나온 npm을 이용하는 방식이 상당히 깔끔하다.

# 프로필 이미지 등록하기

- 이게 뭐라고 생각보다 많은 시간을 구글링하느라 허비했다... 만약 assets/img 폴더에 이미지를 넣어서 활용한다면 \_config.yml 파일에서 다음과 같이 하면 된다.

```yml
# The CDN endpoint for images.
# Notice that once it is assigned, the CDN url
# will be added to all image (site avatar & posts' images) paths starting with '/'
#
# e.g. 'https://cdn.com'
img_cdn: ""

# the avatar on sidebar, support local or CORS resources
avatar: /assets/img/pingu.jpg
```

# 죄측 사이드바 html, css 수정하기

HTML 파일 위치 : \_includes\sidebar.html  
CSS 파일 위치 : \_sass\addon\commons.scss

- 나는 프로필 이미지와 블로그 이름 등의 윗부분 요소들이 중앙정렬 되있으면 좋겠어서 고쳤다.

```css
.profile-wrapper {
  @include mt-mb(2.5rem);
  @extend %clickable-transition;

  padding-left: 1.25rem;
  padding-right: 1.25rem;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
```

# Utterances로 댓글 기능 추가하기

[참고한 블로그 가이드 링크](https://www.irgroup.org/posts/utternace-comments-system/)

# 로컬환경에서 테스트해보는 CMD 명령어

```bash
bundle exec jekyll serve
```
