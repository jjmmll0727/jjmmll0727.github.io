---
title: "간단한 로그인"
excerpt: "로그인 구현"
categories: "spring-self-project"
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
<center><strong>simple login function</strong></center><br><br>
</div>

<div style = "font-size: 15px; line-height: 25px; text-align: left; text-family: monospace;">
저번에 구현한 회원가입을 추가로 로그인을 구현해보았다.<br><br>
<strong>로그인 순서</strong>
<ol>
<li>userform에 입력한 이메일로 findByEmail을 통하여 비밀번호를 추출한다. </li>
<li>추출한 비밀번호와 입력한 비밀번호의 일치여부를 판단한다. Bcrypt를 사용해야 하지만 지금은 일단 기본적인 기능만 구현햤다. Bcrypt 부분은 다음에 이어서..</li>
<li>입력한 이메일이 디비에 있는지 없는지 여부와 비밀번호의 일치여부 또한 Exception 처리를 해준다.</li>
</ol>
</div>
<br><br>
<div style = "font-size: 15px; line-height: 25px; text-align: left">
<center>login service</center>
</div>
<center><img src = "\assets\images\login.png"  border=0 width = "600" height = "400"></center><br><br>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
<center>validation 확인</center><br>
여기서 중요한 점! 이렇게 jpql이 아닌 <code>네이티브 쿼리문</code>을 작성할 때는 반드시 인자값으로 <code>nativeQuery = True</code> 이 필요하다.<br>
또한 @Param annotation을 통해서 정리하는 것이 유지보수에도 좋다.
</div>
<center><img src = "\assets\images\validation.png"  border=0 width = "600" height = "400"></center><br><br>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
<center>login controller</center><br>
</div>
<center><img src = "\assets\images\logincontroller.png"  border=0 width = "600" height = "400"></center><br><br>

