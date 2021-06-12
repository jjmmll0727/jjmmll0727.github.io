---
title: "github.io 블로그 시작하기"
excerpt: "GitHub Blog 서비스인 github.io 블로그 시작하기로 했다."
categories: "etc"

---

<style>
code {
  font-family: Consolas,"courier new";
  color: crimson;
  background-color: #f1f1f1;
  padding: 2px;
  font-size: 105%;
}
</style>

minimal-mistakes 테마는 jekyll 기반으로 만들어졌다.
그렇기 때문에 local에서 test하기 위해서는 jekyll이 필요하다.
jekyll은 Gem 이라는 Ruby 기반의 패키지 매니저를 통해서 받을 수 있다. 고로 Ruby를 설치하고 gem 관리를 위해 bundler를 설치하자.

소스코드 폴더로 들어가서 <code>bundle exec jekyll serve</code> 를 통해서 localhost:4000으로 확인 가능하다.
확인하고 push 하자

### 참고로 api path는 markdown file name을 따라간다

##### categories: "..." 이 부분이 어떤 카테고리에 들어가는 post인지 결정해준다.
