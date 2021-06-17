---
title: "항공대 소프트웨어중심대학사업부 - npm run dev"
excerpt: "프론트에서 백단 서버 동시 접속"
categories: "kau-sw-business"
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
<center><strong>프론트 & 백 서버 연결</strong></center><br><br>
</div>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
<strong>백단에서 서버를 열고 프론트에서 또 서버를 열지 말고 한번에 두곳의 서버를 모두 열어서 확인하자.</strong><br><br>

<code>concurrently 라이브러리</code><br><br>
설치방법 : <code>npm install concurrently --save</code>
최상위 디렉토리의 package.lock 파일을 수정하면 된다. <br><br>
<center><img src = "\assets\images\concurrency.png"  border=0 width = "500" height = "200"></center><br><br>
<code>npm run dev</code> 를 통해서 프론트와 백엔드 둘다 서버를 열 수 있다. <br>
하지만 프론트와 백 둘다 같은 port를 열면 백엔드 서버에 우선권이 가는 것 같다. 나는 다른 port 번호로 서버를 구동하였다. 
</div>

