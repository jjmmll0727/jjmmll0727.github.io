---
title: "항공대 소프트웨어중심대학사업부 - husky"
excerpt: "husky & lint-staged 세팅"
categories: "project"
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

<div style = "font-size: 28px; line-height: 25px;">
<center><strong>husky & lint-staged</strong></center><br><br>
</div>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
<strong>husky : 오류가 있는 코드는 commit이 되지 않도록 세팅해주는 도구이다. </strong><br><br>

<code>$ npm install husky --save-dev</code><br><br>

이렇게 해놓으면 커밋을 할 때 위와 같은 명령어를 실행하고, 자동으로 고쳐지지 않으면, 커밋을 취소하게 한다.<br>
여기서 <code>eslint . --fix</code> 를 통해 현재 디렉토리에 있는 모든 코드를 eslint를 통해서 수정한다. <br> 이 작업이 끝나면, 
<code>prettier --write</code> 를 통해 prettier 규칙을 적용하고 코드를 수정하게 된다.
</div>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
<strong>하지만 위에서 말한 것 처럼 현재 디렉토리에 있는 모든 코드를 검사하는 낭비가 생기게 된다.</strong><br><br>
그래서 <code>staged</code> 된 코드만 검사하도록 하는 도구가 lint-staged 모듈이다.<br><br>

<code>$ npm install lint-staged --save-dev</code><br><br>
이렇게 최상위 디렉토리의 package.json 파일을 수정하여 husky와 lint-staged 모듈을 세팅해준다. <br><br>
<center><img src = "\assets\images\husky-lint.png"  border=0 width = "500" height = "200"></center><br><br>

이를 <code>git-hook</code>이라고 부른다. git hook은 git 과 관련된 어떠한 이벤트가 일어날때 실행시키는 스크립트를 말한다.<br>
프로젝트를 진행하면서 다른 git hook도 세팅을 해봐야겠다. 
</div>

