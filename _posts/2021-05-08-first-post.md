---
title: "github.io 블로그 시작하기"
excerpt: "GitHub Blog 서비스인 github.io 블로그 시작하기로 했다."
---

GitHub Blog 서비스인 github.io 블로그 시작하기로 했다.
GitHub Blog 서비스의 이름은 Pages이다.

Pages가 다른 블로그 플랫폼 보다 편한 것 같아서 마음에 든다.
다른 사람들도 같이 많이 사용했으면 좋겠다는 생각이 든다.

YFM에서 정의한 제목을 이중 괄호 구문으로 본문에 추가할 수 있다.
이 글의 제목은 {{ page.title }}이고
마지막으로 수정된 시간은 {{ page.last_modified_at }}이다.

minimal-mistakes 테마는 jekyll 기반으로 만들어졌다.
그렇기 때문에 local에서 test하기 위해서는 jekyll이 필요하다.
jekyll은 Gem 이라는 Ruby 기반의 패키지 매니저를 통해서 받을 수 있다. 고로 Ruby를 설치하고 gem 관리를 위해 bundler를 설치하자.

소스코드 폴더로 들어가서 "bundle exec jekyll serve" 를 통해서 localhost:4000으로 확인 가능하다.
확인하고 push 하자

### 참고로 api path는 markdown file name을 따라간다
