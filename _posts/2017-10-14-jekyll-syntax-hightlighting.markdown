---
layout: post
Title: "Jekyll 블로그의 Code Block에 syntax highlighting 기능 넣기"
Author: bosco lyu
Date: October 14, 2017
Meta: "IT"
---

<img src="https://mycyberuniverse.com/images/thumbnail/jekyll-rouge.png" width="50%">


Jekyll에서 syntax highlighting을 사용하려면 아래 reference 문서를 보시면 됩니다시
간략 요약하면 다음과 같습니다.

# rouge 설치 필요함.
```bash
[user]$ gem install rouge
Successfully installed rouge-3.0.0
Parsing documentation for rouge-3.0.0
1 gem installed
```

# _config.yml에 추가 필요함.
```yml
gems:
  - "jekyll-feed"
  - "jekyll-seo-tag"
  - "jekyll-paginate"
  - "jekyll-sitemap"
  - highlighter: rouge
```

# syntax highlighting css 파일 다운로드 받아서 복사하기
* download link : http://richleland.github.io/pygments-css/
* 블로그 사이트의 css 폴더에 복사함

# 기존 main.css 파일에 highlighting css 파일 집어넣기

```css
@import url(vs.css);
```



# reference
https://mycyberuniverse.com/web/syntax-highlighting-jekyll.html