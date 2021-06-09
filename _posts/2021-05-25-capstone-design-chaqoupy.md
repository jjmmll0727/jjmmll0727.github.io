---
title: "capstone design - chaqoupy"
excerpt: "chaqoupy - connection with android and python script"
categories: "project"
---

<style>
code {
  font-family: Consolas,"courier new";
  padding: 2px;
  font-size: 90%;
}
</style>

<div style = "font-size: 28px; line-height: 25px;">
<center><strong>chaqoupy</strong></center><br><br>
</div>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
android안에 학습모델을 넣기 위해 온갖 tool을 찾아보던 와중에 chaqoupy라는 android sdk를 알아냈다.<br>
안드로이드 프로젝트 안에 파이썬 스크립트를 삽입하여 돌릴 수 있는 엄청난 툴이다. <br>

<img src = "\assets\images\chaqoupy-code1.png"  border=0 width = "300" height = "50"><br>
<br>
<img src = "\assets\images\chaqoupy-code2.png"  border=0 width = "400" height = "70"><br>


간단한 파이썬 코드를 돌리는데 성공하였지만, 문제는 camera api 였다. <br>
chaqoupy 를 통해 camera api와의 연동이 불가능하다는 글을 보았다. <br>
물론 더 찾아봐야 알겠지만, 우리는 1학기 안에 일차적으로 기능을 구현하고, 2학기에 더 많은 데이터 준비, 모델 학습을 통한 완성도 높은 서비스 구축을 만들고자 하였기 때문에, 일단은 chaqoupy를 사용하지 않고, 학습모델을 서버쪽에 저장해서 android client와의 통신을 통해 기능을 구현하려고 한다. 
</div>


<p style = "font-size: 15px;"><a href = "https://www.ericdecanini.com/2019/10/21/run-python-scripts-in-the-android-front-end-with-chaquopy/">출처</a></p>
