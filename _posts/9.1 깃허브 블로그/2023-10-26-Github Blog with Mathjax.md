---
layout: post
title: "[Blogging] 깃허브 블로그에 Mathjax로 수식 표시하기"
date: 2024-01-26 11:00:00 +0900
categories: [9.1 깃허브 블로그]
tags: [Jekyll, Chirpy]
---

# Chirpy 테마로 깃허브 블로그 개설하기

## 깃허브 블로그에 Mathjax로 수식 표시하기!

- 중요 참고사항
  - 현재 작성 시점은 2024년 1월이다. 시간이 좀 오래 지났다면 이 글의 설정을 따랐을 때 문제가 생길 수 있다.
  - 이 블로그의 Jekyll 테마는 **Chirpy**이다.
- 선형대수학을 포스팅하려던게 발단이었다... 나는 깃허브 블로그에 수식을 표시하고 싶었고 구글링을 시작했다. 블로그마다 설정 방법이나 Mathjax버전이 달랐고.. 어떤 것을 적용하면 `$`으로 인라인 수식은 되는데 `$$`으로 블록 수식을 작성하면 `\(` 이나 `\)`이 화면에 표시되거나, 그 반대가 안되거나 하는 문제가 있었다. 그런 이유에서 GPT와 함께하는 약간의 해매임 끝에 현재 시점에서 인라인과 블록 양쪽에 문제 없이 적용되었던 방법을 찾았고, 포스팅을 통해 남기려고 한다.
- 이 설정을 사용하면 인라인 수식은 두 개의 `$`안에, 블록 수식은 `$$`안에 넣음으로써 사용할 수 있다. 물론 코드에 나오는 다른 방식도 가능하다.

## 필요한 설정들

### mathjax_support.html 만들기

- \_includes 폴더에 mathjax_support.html 파일을 하나 만든다.
- 코드 내용은 다음을 붙여넣기 한다. (참고로 구글링을 바탕으로 GPT랑 작성했다.)

```html
{% raw %}
<script>
  window.MathJax = {
    tex: {
      inlineMath: [
        ["$", "$"],
        ["\\(", "\\)"]
      ],
      displayMath: [
        ["$$", "$$"],
        ["\\[", "\\]"]
      ],
      processEscapes: true,
      autoload: {
        color: [],
        colorV2: ["color"]
      }
    },
    svg: {
      fontCache: "global"
    }
  };
</script>
<script
  type="text/javascript"
  async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/3.1.2/es5/tex-mml-chtml.min.js"
></script>
{% endraw %}
```

- 참고로 `제공된 스크립트 소스 https://cdn.mathjax.org/mathjax/latest/MathJax.js 는 더 이상 사용되지 않습니다. MathJax CDN은 공식적으로 사용이 중단되었고, 다른 CDN으로 이동했습니다.`라고 한다.

### default.html 수정하기

- \_layouts 폴더의 default.html 파일을 열고 다음 코드를 붙여넣는다.
- 붙여넣는 위치는 <body>앞의 <head>안이다. 나는 <head> 자체가 파일에 없었어서 그냥 <head>도 만들었다.

```html
{% raw %} {% if page.use_math %} {% include mathjax_support.html %} {% endif %}
{% endraw %}
```

- 코드 맥락을 보면 대충 이렇다.

```html
{% raw %}
<html lang="{{ site.alt_lang | default: site.lang }}" {{ prefer_mode }}>
  {% include head.html %}
  <head>
    {% if page.use_math %} {% include mathjax_support.html %} {% endif %}
  </head>
  <body>
    {% include sidebar.html lang=lang %}

    <div id="main-wrapper" class="d-flex justify-content-center">
      <div class="container d-flex flex-column px-xxl-5">{% endraw %}</div>
    </div>
  </body>
</html>
```

### \_posts 폴더의 마크다운 파일에 use_math 옵션 추가하기

포스팅 마크다운 파일 맨 윗부분에 `use_math: true` 줄을 추가한다.

```markdown
## {% raw %}

layout: post
title: "포스팅 제목"
categories: [카테고리]
tags: [태그1, 태그2]
use_math: true

---

{% endraw %}
```

---

- 이렇게 3가지 설정만 완료하면 수식을 쓸 수 있다!
- \_config.yml 파일의 내용을 수정하라는 경우도 있었는데 나는 수정없이 잘 됐다.
- 블록 수식을 쓸 때에는 이전 줄과의 사이에 한줄을 비워주고 `$$`를 시전해야 중앙정렬이 된다.
