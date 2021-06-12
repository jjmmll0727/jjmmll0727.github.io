---
title: "항공대 소프트웨어중심대학사업부 - start"
excerpt: "eslint & prettier 세팅"
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
<center><strong>시작하기</strong></center><br><br>
</div>

<div style = "font-size: 15px; line-height: 25px; text-align: left;">
교수님께서 이번에 우리학교가 소프트웨어 중심대학 사업부에 선정되었는데 이를 위한 사이트를 만들어 달라고 하셨다. &#9994;<br><br>
너무 좋은 기회라 생각하고, 무조건 한다고 했다. 하지만 프론트 담당하는 친구가 필요했고, 그날 바로 구해서 팀을 만들었다. <br><br>
그 다음날 곧 바로 repository 를 새로 팠고, 완벽한 프로젝트를 위해 eslint와 prettier를 적용하여 시작하기로 하였다. <br><br>

<div style = "font-size: 20px; line-height: 25px;">
<center>eslint & prettier 설치하기</center><br><br>
<div style = "font-size: 15px; line-height: 25px;">
1. eslint 설치하기 <br>
적용하고 싶은 프로젝트 디렉토리로 이동하여 <code>$ npm install eslint --save-dev</code><br><br>
2. prettier 설치하기 <br>
같은 디렉토리에서 <code>$ npm install prettier --save-dev --save-exact</code><br>
여기서 보면 eslint와 다르게 <code>--save-exact</code>가 추가된것을 볼 수 있는데, 버전이 달라지면서 생기는 스타일의 변화를 막기 위해서이다. <br><br>

또한 다른 모듈의 설치도 필요하다. 
<ul>
<li><code>eslint-config-prettier</code> : prettier와 충돌할 설정들을 비황성화</li>
<li><code>eslint-config-prettier</code> : prettier에서 인식하는 코드 포맷 오류를 eslint 오류로 출력해준다.</li>
</ul>
<code>$ npm install eslint-plugin-prettier eslint-config-prettier --save-dev</code><br><br>

이제 vscode에서 eslint, prettier extension을 설치해주면 되는데, 중요한 점은 버전을 맞춰줘야 한다. 현재 eslint의 latest 버전과 vscode의 버전이 연동이 되지 않아 설치하는데 많은 시간을 쏟았다. 결국 2.1.17 버전으로 설치하였다. 또한 vscode에서 직접 extension을 받을 수 없고, <a href = "https://marketplace.visualstudio.com/">visual studio의 marketplace </a>에서 vsix 파일을 받아야 한다. <br> vscode에서 <code>install from vsix</code>을 통해서 설치해줘야 한다.<br><br>

eslint와 prettier의 세팅을 각 프로젝트마다 다르게 설정할 수 있기 때문에, vscode -> <code>command + , </code>를 통해서 vscode의 설정으로 들어간다. <br><br>
<center>workspace 탭을 눌러 현재 프로젝트에서만 적용이 되도록 준비를 한다. </center><br>

<center><img src = "\assets\images\vscode setting.png"  border=0 width = "500" height = "200"></center><br><br>

<center>추가로 .vscode/settings.json 파일을 수정해준다. </center><br>
<center><img src = "\assets\images\settingsjson.png"  border=0 width = "500" height = "200"></center><br><br>

<center>eslintrc.json 수정</center><br><br>
<center><img src = "\assets\images\eslintrc.png"  border=0 width = "500" height = "200"></center><br><br>

<center>prettier.json 수정</center><br><br>
<center><img src = "\assets\images\prettierrc.png"  border=0 width = "500" height = "200"></center><br><br>

</div>










<div style = "font-size: 10px; line-height: 25px; text-align: left;">
<a href = "https://feynubrick.github.io/2019/05/20/eslint-prettier.html">출처</a>

