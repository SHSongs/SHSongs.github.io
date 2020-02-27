---
layout: post
title: "github pages에서 disqus 사용하기"
date: 2018-07-08
excerpt: "jekyll테마에 포함되어 있던 diqus 플러그인을 사용하기 위한 방법"
tag:
- Disqus
category: [ Jekyll 블로그 ]
feature: https://png93.github.io/assets/img/title/basic.jpg
comments: true
---

Disqus, 댓글 플러그인
==
<a href = "https://disqus.com/"><img src = "https://png93.github.io/assets/img/post/disqus_home.PNG"/></a>

<br>

github 블로그에 적용할 jekyll 테마를 고를 때 댓글 여부를 확인한 후 다운 받았었는데, 요게 disqus라는 플러그인을 사용한거였다.

그런데, Demo에서는 잘 되던 댓글 창이 내 블로그에서는 실행할 수 없다는(?) 메세지 한 줄이 뜨면서 동작하지 않았다.

왜 안되는지 알아보니 disqus라는 사이트에서 뭔가 설정을 해줘야 한단다.

다행히 다음의 과정을 완료한 후 댓글 창이 정상적으로 나타났다.

1. [Disqus](https://disqus.com/) 에서 가입하고 로그인
2. '내 site에 disqus 설치하기' 선택
3. github pages URL 입력, category, 언어 선택
4. **3번 완료 후 이동하는 Admin 페이지에서 settings 탭 선택**
    * **두번 째 문단에 보면 나한테 부여된 'shortname'을 확인 할 수 있음!**
    github 저장소에 `_config.yml` 파일을 살펴보니까 disqus_shortname을 입력하는 곳이 있어서 여기에다가 써줌.
<img src = "https://png93.github.io/assets/img/post/disqus_settings.PNG"  width = "60%"/>
