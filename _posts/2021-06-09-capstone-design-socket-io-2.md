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
tensorflow lite 를 사용하여 android와 통신하는 것이 가장 좋은 방법이지만, 시간적 여유가 없어서 서버와 통신하는 방식으로 구현하다가 중요한 점을 알게 되었다. <br>
android에서 서버로 받은 데이터를 학습모델에 입력값으로 넣어야 하기 때문에 우리는 nodejs와 python script를 연동하는 방법을 시도했다.<br>
<ol>
<li><code>child_process</code> 모듈을 사용하여 자식프로세스를 생성한다.</li>
<li>python script를 실행하고 반환값을 받는다. </li>
</ol>
이렇게 nodejs 와 python script 간의 연동을 성공했다. <br>
또한 옵션으로 <code>파라미터</code>를 포함하여 연동할 수 있었다. 
<br><br>
하지만 <strong>문제</strong>가 발생했다. <br>
nodejs와 python 간의 주고 받는 데이터의 <code>크기</code>가 중요한 문제였다.<br>
android에서 넘어온 데이터는 영상을 캡쳐한 <code>byte array</code>이다. <br>
즉 사이즈가 매우 컸다. 결국 이 큰 데이터를 python script로 넘기는 것을 실패하였다...<br>
혹시나 해서 작은 사이즈의 데이터로 테스트 해봤는데, 성공하였다. <br><br>
&#9989; <strong>너무 큰 사이즈의 데이터는 <code>child_process</code> 모듈로 주고 받을 수 없다 </strong>&#10060; <br>
<br><br>
<div style = "font-size: 15px; line-height: 25px; font-family: monospace;">
전송에 실패한 코드 (big size data)
</div>
<img src = "\assets\images\childprocess_fail.png"  border=0 width = "500" height = "200"><br><br>
<img src = "\assets\images\no.jpg"  border=0 width = "500" height = "200"><br><br>

<div style = "font-size: 15px; line-height: 25px; font-family: monospace;">
전송에 성공한 코드 (small size data)
</div>
<img src = "\assets\images\childprocess_success.png"  border=0 width = "500" height = "200"><br><br>
<img src = "\assets\images\yes.jpg"  border=0 width = "500" height = "200"><br><br>
<div style = "font-size: 15px; line-height: 25px; font-family: monospace;">
test를 위한 python script
<br>
<img src = "\assets\images\pytest.png"  border=0 width = "300" height = "100"><br>
android에서 받은 data buffer 0 0 0 000000.... 를 보낼 시 데이터의 사이즈가 너무 커서 python script로 전송을 실패하는 것을 볼 수 있다. <br>
반면에 임시 데이터 "sendingdata" 를 보낼 시에는 데이터의 사이즈가 작아 python script와의 연동이 성공함을 볼 수 있다. <br><br>


&#9989; 이번학기에는 이렇게 끝났지만, 많은 시행착오를 통해 성장할 수 있는 중요한 시간이었다. 
<div style = "font-size: 15px; line-height: 25px; font-family: monospace;">
<ol>
<li>chaqoupy는 android background camera api와 통신이 되지 않는다.</li>
<li>response없이 request를 반복적으로 보내기 위해서는 restful api가 아닌 <code>socket io protocol</code>을 사용해야 한다.</li>
<li>child_process 모듈을 통해서는 큰 사이즈의 데이터를 주고 받을 수 없다. (그래서 이런 방식으로 하지 않고 <code>tensorflow lite</code> 라는 android 전용 새로운 툴을 만들어냈구나...)</li>
</ol>

<p style = "font-size: 15px;"><a href = "https://github.com/jjmmll0727/Capstone_Design/tree/main/socketio">github-repository</a></p>


