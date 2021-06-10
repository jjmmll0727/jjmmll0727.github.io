---
title: "raspberry pi to notice for blind"
excerpt: "device for blind"
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
video { 
  max-width: 80%; 
  display: block; 
  margin: 20px auto; 
}
    
</style>

<div style = "font-size: 25px; line-height: 25px;">
<center>raspberry pi</center><br><br>
</div>


<div style = "font-size: 15px; line-height: 25px;">
교내에서 ict make-a-thon 대회가 열렸다. 사회적 약자들을 위해 어떠한 서비스를 만들어보고 싶었던 찰나에, 교내에서 비슷한 방향성을 띈 대회를 개최하여 참가하게 되었다. <br>
한번쯤은 라즈베리파이를 해보고 싶었었고, 학습모델을 담아야 하기 때문에 라즈베리파이 구매부터 시작하여 세팅 장치 연동 등 모든 하드웨어 작업을 경험할 수 있었다. <br><br>
생각보다 라즈제리파이를 세팅하는 과정에서 애를 먹었다. <br>
가장 높은 성능을 보이는 <code>라즈베리파이 4B</code>를 사용했지만, 수용가능한 <code>tensorflow</code> 버전이 <code>1.14</code> 였지만, 우리가 학습시킨 모델에서 필요한 <code>tensorflow</code> 버전은 <code>2.2</code> 이상이었다. <br>
결국 url을 통해서 direct로 다운을 받았었다. <br> 
</div>

<br>
<div style = "font-size: 15px; line-height: 25px;">
<center>부품</center>
</div>
<center><img src = "\assets\images\장치.JPG"  border=0 width = "200" height = "50"></center><br>

<div style = "font-size: 15px; line-height: 25px;">
<center>완성작</center>
</div>
<center><img src = "\assets\images\device.JPG"  border=0 width = "200" height = "50"></center><br>

<div style = "font-size: 15px; line-height: 25px;">
<center>결과1 - 초록붙</center>
</div>
<center><img src = "\assets\images\bluelight.png"  border=0 width = "200" height = "50"></center><br>

<div style = "font-size: 15px; line-height: 25px;">
<center>결과2 - 빨간불</center>
</div>
<center><img src = "\assets\images\redlight.png"  border=0 width = "200" height = "50"></center><br>

<div style = "font-size: 15px; line-height: 25px;">
<center>시연동영상</center>
</div>
<video controls>
  <source src="\assets\videos\final_makertone.mp4" type="video/mp4">
  <strong>Your browser does not support the video tag.</strong>
</video>

<br>
<div style = "font-size: 15px; line-height: 25px;">
<center> <a href="/assets/ppt/makeathon.pptx">발표자료(ppt) 다운로드</a>  </center>