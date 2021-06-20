---
title: "springboot self project"
excerpt: "구조파악 및 간단한 회원가입"
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
<center><strong>spring boot self project</strong></center><br><br>
</div>

<div style = "font-size: 15px; line-height: 25px; text-align: left; text-family: monospace;">
스프링 부트를 이용해서 스스로 프로젝트를 만들어보고자 한다. 강의를 듣고 있지만, 내가 직접 맨땅에 헤딩 하듯 프로젝트를 만들어봐야 더 와닿을 것 같아서 시작하게 되었다. 개발하면서 알게 된 사항들을 정리하고자 한다.<br><br>
<strong>기본주조</strong>
<ul>
<li>domain - 실제 DB에 접속하는 기능을 가지며, table의 구조를 띈다. @Entity annotation을 사용하여 디비에 접속할 수 있다. </li>
<li>repository - JpaRepository에 접근하는 인터페이스</li>
<li>DTO - 컨트롤러를 통해 받은 데이터를 entity 전달해주기만 하는 매개체 역할. 데이터의 변경이 없어서 용이하다. 반드시 하나의 entity에 하나의 dto가 매칭되는 것은 아니다.</li>
<li>serivce - rpository를 통해서 db에서 가져온 데이터를 처리하여 controller에게 다시 보내준다.</li>
<li>controller - 라우터 역할. 프론트에서 데이터를 받아와 백단으로 넘겨주고 백단에서 처리된 데이터를 다시 프론트로 보내준다.</li>
</ul>
</div>
<br><br>
<div style = "font-size: 15px; line-height: 25px; text-align: left">
<center>프로젝트 구조</center>
</div>
<center><img src = "\assets\images\스프링구조.png"  border=0 width = "500" height = "200"></center><br><br>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
<center>1. repository</center>
</div>
<center><img src = "\assets\images\repo.png"  border=0 width = "500" height = "200"></center><br><br>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
<center>2. entity</center>
</div>
<center><img src = "\assets\images\entity.png"  border=0 width = "500" height = "200"></center><br><br>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
<center>3. dto</center>
</div>
<center><img src = "\assets\images\dto.png"  border=0 width = "500" height = "200"></center><br><br>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
<center>4. controller</center><br><br>
여기서 중요한 점이 라우터 앞부분에 <code>@ResponseBody</code> 와 함수 인자 값으로 <code>@RequestBody</code> 가 중요하다!
</div>
<center><img src = "\assets\images\controller.png"  border=0 width = "500" height = "200"></center><br><br>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
<center>5. service</center>
</div>
<center><img src = "\assets\images\service.png"  border=0 width = "500" height = "200"></center><br><br>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
<center>postman 결과</center>
</div>
<center><img src = "\assets\images\postman.png"  border=0 width = "500" height = "200"></center><br><br>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
<center>실제 h2 database 확인</center>
</div>
<center><img src = "\assets\images\h2.png"  border=0 width = "500" height = "200"></center><br><br>




<div style = "font-size: 15px; line-height: 25px; text-align: left">
진짜 짜증나는 오류가 발생함... 로컬에서 gradle 프로젝트를 생성하고 개발하다가 github 로컬 저장소에 저장 하고 나니 run이 안됨....
디렉토리와 관련이 깊은 것 같은데 build tools에서 아예 설정이 안됨... 이런... 이것 때문에 한시간을 날린 것 같다... 아직도 이유를 모르겠음... terminal에서는 build, run 모두 잘되는데 왜 intellij에서는 안될까... <br><br>
더 이상 이 문제로 시간을 버리고 싶지 않아서 일단은 다시 새롭게 프로젝트를 생성했다. 반드시 해결해야 하는 문제이지만 도저히 모르겠다... 구글링해도 답을 모르겠다... 왜 이럴까...<br><br>
하는 도중에, 갑자기 생각났다. project를 오픈할 때 반드시 <code>build.gradle 파일</code>을 open as project로 열면 된다는 것을........ 바보 같은 짓이었고, 한번더 기록의 중요성을 깨달았다.
</div>
