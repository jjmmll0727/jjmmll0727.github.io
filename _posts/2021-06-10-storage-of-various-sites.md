---
title: "첫번째 연합동아리 - mini project"
excerpt: "storage of various sites"
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
<center><strong>first cooperation</strong></center><br><br>
</div>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
그렇게 대규모라고 할 수는 없지만, 연합동아리에 들어와서 처음으로 모르는 사람들과 아이디어 회의를 하고 기획팀, 디자인팀, 개발팀이 서로 협력하며 소통하는 경험이었다. <br><br>
교내에서는 모두 개발자 역할을 수행하며 프로젝트를 진행했지만, 전문적인 기획자와 디자이너분들과 함께 협업하니 뭔가 새로운 기분이 들며 매우 재밌었다. <br><br>
<code>MVC 모델</code>을 접목하며 기본적인 회원가입, 로그인, DB와의 연계 등 nodejs 만의 여러 모듈을 사용하며 restful api 프로젝트를 진행하였다. <br><br>
물론 지금 보면 refactoring 도 안되어있는 엉망인 코드지만 그래도 내가 서버 개발자로 발돋움 할 수 있는 좋은 경험이었다고 생각한다. <br><br> 
그 중에 기억에 남는 코드는 로그인 및 회원 인증 기술인 <code>JWT token</code>이다.
</div>
<br><br><br>
<div style = "font-size: 28px; line-height: 25px;">
<center><strong>JWT token</strong></center><br>
<div style = "font-size: 15px; line-height: 25px; text-align: left; text-family: monospace;">
JWT token은 <code>Json Web Token</code>의 줄임말로 웹 표준<code>(RFC 7519)</code>으로서 JSON 객체를 이용하여 정보를 안전하게 전달해주는 방법이다. <br><br>
<strong>jwt token의 대표 기능</strong>
<ul>
<li>회원 인증</li>
<li>정보 전달</li>
</ul>
<br><br>
<img src = "\assets\images\jwt.png"  border=0 width = "600" height = "300"><br><br>
유저가 로그인을 하면 서버가 유저의 회원정보와 암호화 키를 기반으로 한 암호화된 <code>token</code>을 유저에게 제공한다. 유저는 그 토큰을 가지고 있다가 서버에 요청을 할 때 마다 해당 토큰을 서버에 넘겨준다. 서버는 토큰이 유효하고 인증되었는지 확인하고 이를 처리한다. <br><br>
그렇기 때문에 서버는 유저의 세션을 유지할 필요가 없고, 또 유저가 로그인을 했는지 안했는지 확인할 필요가 없다. 단지 토큰만 신경쓰면 되는 방식이기 때문에 서버의 자원을 아낄 수 있다. 
<br><br>
나는 처음에 로그인을 할 때 토큰을 지급하고, 추후에 인증해야 하는 라우터에서 미들웨어로 처리하였다. <br><br>
</div>
<div style = "font-size: 20px; line-height: 25px;">
&#9995;<strong>token 발급</strong><br><br>
<img src = "\assets\images\givetoken3.png"  border=0 width = "700" height = "400">
</div>
<br><br>
<div style = "font-size: 15px; line-height: 25px;">
유저가 회원가입을 할 때 <code>bcryptjs</code> 모듈로 비밀번호를 암호화한다. <br><br>로그인을 할때 유저가 입력한 비밀번호와 암호화된 비밀번호를 bcryptjs 모듈의 <code>compare</code> 함수를 통해 비교한다.<br><br>
일치한다면 <code>jsonwebtoken</code> 모듈의 sign함수를 통해 token을 지급한다. 만기 시간은 3시간으로 설정한다.  
</div><br>


<div style = "font-size: 20px; line-height: 25px;">
&#9995;<strong>미들웨어로 사용자 인증 처리</strong><br><br>
<img src = "\assets\images\tokenauth2.png"  border=0 width = "700" height = "400">
</div>
<br><br>
<div style = "font-size: 15px; line-height: 25px;">
유저가 사용자 인증을 하려고 요청을 할 때 header의 <code>authorization</code>에 token을 담아서 서버로 보내준다. <br><br>
서버에서는 <code>jsonwebtoken</code> 모듈의 verify함수를 통해 일치하는지 확인한다. <br><br>



<p style = "font-size: 15px;"><a href = "https://velopert.com/2389">출처</a></p>
<p style = "font-size: 15px;"><a href = "https://github.com/jjmmll0727/5th-mini-team3-web/blob/master/team3_mini/Backend/routes/api/login/login.controller.js">github - token 발급</a></p>
<p style = "font-size: 15px;"><a href = "https://github.com/jjmmll0727/5th-mini-team3-web/blob/master/team3_mini/Backend/routes/api/middleware/jwt-verify.js">github - 사용자 인증 처리</a></p>