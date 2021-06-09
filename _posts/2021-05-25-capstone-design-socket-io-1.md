---
title: "capstone design - socket.io - 1"
excerpt: "consecutive protocol"
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
<center><strong>socket.io</strong></center><br><br>
</div>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
android와 학습모델을 집어넣은 서버와 통신하는데 socket.io 프로토콜을 사용한다.<br>
기존에는 항상 rest api를 기반으로 서버를 구축했었는데, 이번 프로젝트의 중요한 점은 양방향 통신이라는 것이다.<br>
기존에 http 기반의 rest api는 클라이언트의 request가 있으면 그에 맞는 responde를 하고, 그 다음에 추가적으로 request를 할 수 있는 구조이다. <br>
하지만 우리는 눈을 깜빡였다는 response가 있을때 까지 이미지를 보내는 요청을 멈출 수 없는 구조라고 판단하였다. <br>
그렇기 때문에, 인앱채팅을 구현할 때 주로 쓰이는 양방향 통신 socket.io를 사용하기로 하였다. <br>

</div>

```javascript
var express = require('express');
var socket = require('socket.io');

// App Setup
var app = express();
// Create server and listen to specific port number
var server = app.listen(4000, function(){
	console.log('Listening to requests on port 4000');
});

// Socket setup; provide server reference to work with
var io = socket(server);

// Listening to an connection event; socket parameter refers to created/particular socket
io.on('connection', function(socket){
	// Print socket id on new connection
	console.log(`made socket connection, ${socket.id}`);

	// Listen for chat message being sent from client
	socket.on('chat', function(data){
		// Send received chat message to all connected clients
		io.sockets.emit('chat',data);
	});

    socket.on('disconnect', () => {
        console.log(`Socket disconnected : ${socket.id}`)
    })
});
```
<div style = "font-size: 15px; line-height: 25px; text-align: left">
코드는 간단하다. <br>
socket io 모듈을 가져와서 클라이언트와의 연결을 시도한다. <br>
나는 localhost로 열었기 떄문에 외부에서 접속할 수 있는 ip주소를 통해 안드로이드 담당 팀원과 연결하였다. <br>
chat 이라는 이벤트명을 통해 안드로이드와 통신하는데 안드로이드에서 보내는 데이터가 <code>io.sockets.emit('chat',data);</code>의 <code>data</code>로 들어오게 된다. <br>
<br>
</div>
하지만 여기서 <strong>중요한 점</strong>이 있다. <br>
바로 클라이언트와 서버 측의 socket.io 버전을 맞춰야 한다는 것이다.<br>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
<strong>android</strong><br>
<strong>nodejs</strong><br>
<img src = "\assets\images\socketio-version.png"  border=0 width = "400" height = "100"><br>
</div>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
여기서 2시간을 버렸다... 안드로이드는 내파트는 아니지만, 항상 보면 버전문제가 많은 것 같다..
</div>



