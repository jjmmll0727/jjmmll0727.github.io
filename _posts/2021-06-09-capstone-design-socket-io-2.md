---
title: "capstone design - socket.io - 2"
excerpt: "posibility according to data size"
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
<center><strong>data size is important</strong></center><br><br>
</div>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
android 와 양방향 통신하기 위해 서버에서 <code>restful api</code>가 아닌 <code>socket io</code> 프로토콜을 사용하였다. <br>
기존에는 항상 rest api를 기반으로 서버를 구축했었는데, 이번 프로젝트의 중요한 점은 양방향 통신이라는 것이다.<br>
기존에 http 기반의 rest api는 클라이언트의 request가 있으면 그에 맞는 responde를 하고, 그 다음에 추가적으로 request를 할 수 있는 구조이다. <br>
하지만 우리는 눈을 깜빡였다는 response가 있을때 까지 이미지를 보내는 요청을 멈출 수 없는 구조라고 판단하였다. <br>
그렇기 때문에, 인앱채팅을 구현할 때 주로 쓰이는 양방향 통신 socket.io를 사용하기로 하였다. <br>

</div>