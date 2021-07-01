---
title: "about setTimeout"
excerpt: "setTimeout function"
categories: "research"
---

<style>
code {
  font-family: Consolas,"courier new";
  padding: 2px;
  font-size: 105%;
}
</style>


<div style = "font-size: 28px; line-height: 25px;">
<center><strong>setTimeout</strong></center><br><br>
</div>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
nodejs에서 사용되는 setTimeout 함수에 대해 알아보자. 언제한번 동아리에 지원할 때 저 함수에 대해 물어본 적이 있었다. 그 당시에 몰랐기에 구글링해서 지원했었다는... <br><br>
setTimeout 함수는 쉽게 말해 예약제라고 보면 좋을 것 같다. 흔히 말해 호출 스케줄링이라고 하는데, <br>
<ul>
<li>setTimeout: 일정 시간이 지난 후에 함수를 실행한다. </li>
</ul>
</div>
<br><br>

<div style = "font-size: 20px; line-height: 25px;">
1. setTimeout
</div>
<div style = "font-size: 15px; line-height: 25px; text-align: left">
<Blockquote>
문법 : setTimeout(func, delay, arg1, arg2, ...)
</Blockquote>
<ul>
<li>func : 호출하고자 하는 콜백함수</li>
<li>delay : 지연시키고자 하는 시간 (단위: ms)</li>
<li>arg1, arg2, ... : 호출하는 콜백함수의 인자값</li>
</ul>
<br><br>
예를 들어, 
</div>

```javascript
function sayHi(who, phrase) {
  alert( who + ' 님, ' + phrase );
}

setTimeout(sayHi, 1000, "홍길동", "안녕하세요."); // 홍길동 님, 안녕하세요.
``` 
<div style = "font-size: 15px; line-height: 25px; text-align: left">
즉 1초 후에 홍길동, 안녕하세요 인자값을 sayHi 함수에게 넘겨주며 실행된다. 
<br><br>

<Blockquote>
setTimeout 여러개일 경우
</Blockquote>
</div>

```javascript
setTimeout( () => { console.log('j'); aaa(); }, 2000 ); // 1
setTimeout( () => { console.log('a'); aaa1(); }, 2000 ); // 2
setTimeout( () => { console.log('v'); aaa(); }, 0 ); // 3

const aaa = () => {
    setTimeout( () => { console.log('d'); }, 0);
    console.log('c');
};
const aaa1 = () => {
    setTimeout( () => { console.log('d1'); }, 0);
    console.log('c1');
};
```

<div style = "font-size: 15px; line-height: 25px; text-align: left">
&#9995; 기본적으로 setTimeout 함수간의 순서는 딜레이 시간이 기준이다. 즉 위와 같은 코드에서 3 -> 1 -> 2 순서로 실행된다. 
또한, 메모리에 같이 쌓인 다른 함수를 먼저 실행시키고 나서 딜레이 시간을 가진 후에 setTimeout 함수를 실행하게 된다. 
<ol>
<li>v 가 먼저 출력되고 aaa 함수를 실행한다. </li>
<li>setTimeout( () => { console.log('d'); }, 0); 를 실행하기 전에 c를 먼저 출력한다. </li>
<li>다른 setTimeout 함수들의 딜레이가 2초이기 때문에 3번 함수를 실행(v를 출력한다)한다.</li>
<li>1번과 2번 모두 딜레이가 2초이므로 먼저 선언된 1번 먼저 실행한다.</li>
<li>3번과 마찬가지로 j를 출력하고, aaa 함수를 실행한다.</li>
<li>c를 출력하고 d를 출력해야 하는데,</li>
<li>같은 딜레이를 가진 함수 2번이 기다리고 있기 때문에 2번 함수가 실행된다.</li>
<li>마찬가지로 a가 출력되고, aaa1함수가 실행된다.</li>
<li>c1이 출력되고, 아까 예약제로 걸어둔 d가 출력된다.</li>
<li>마지막으로 d1이 출력된다. </li>
</ol>
<strong>v c d j c a c1 d d1</strong>
</div>
<br><br>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
<Blockquote>
setTimeout 중첩인 경우
</Blockquote>
</div>

```javascript
const fs = require('fs');

const aaa = () => {
    setTimeout( () => { console.log('d'); }, 0);
    console.log('c');
};

setTimeout( () => {
    fs.readFile('any.txt', () => {
        setTimeout(() => {
            console.log('e');
        }, 0);
        setImmediate(() => {
            console.log('f');
        });
    });
}, 100 );

setTimeout( () => { console.log('a'); aaa(); }, 0 );

Promise.resolve().then( () => { aaa(); console.log('b'); });
```

<div style = "font-size: 15px; line-height: 25px; text-align: left">
<ol>
<li>aaa 함수를 실행시킨다. setTimeout( () => { console.log('d'); }, 0); console.log('c');
c를 출력하고 d를 출력하게 된다. 하지만 console.log('b'); 가 예약되어 있기 때문에 b가 먼저 출력되고 d의 출력은 예약이 된다. </li>
<li>그 후 딜레이가 0ms인 setTimeout함수가 실행되는데 console.log('a'); 가 실행되고 함수aaa가 실행된다.</li>
<li>1번과 마찬가지고 c가 먼저 출력되고 d는 또다시 예약이 된다. </li>
<li>자 이제 딜레이가 0인 setTimeout함수가 끝이 났다. 1번에서 예약된 d가 출력되고, 3번에서 예약된 d가 연달아 출력하게 된다. </li>
<li>이제 가장 마지막으로 미뤄진 딜레이가 0ms인 setTimeout함수가 실행된다. any.txt파일을 읽고 나서 e를 출력해야 하는데 마찬가지로 딜레이가 생겨 나중으로 예약된다. setimmediate 함수로 인해 f는 연기되지 않고 바로 출력하게 된다 </li>
<li>마지막으로 e가 출력된다.</li>
</ol>
<strong>c b a c d d f e </strong><br><br><br>
&#9995; 코드를 보면 처음에 aaa함수를 정의한 부분 아래 부터 진행이 되는데, 두개의 setTimeout함수를 보면 하나는 딜레이 100ms, 하나는 딜레이 0ms이다. 여기서 주의할 것이 딜레이가 0ms라고 바로 실행하는 것이 아니라 여기서 말하는 딜레이는 예약제라고 생각하면 편하다. <strong>즉, 딜레이가 0ms인 setTimeout 함수가 딜레이가 100ms인 setTimeout함수보다 먼저 실행된다는 뜻이다. </strong>하지만 setTimeout함수는 기본적으로 예약되어있는 함수의 실행을 먼저 실행시키기 때문에 Promise.resolve.then을 먼저 실행하게 된다. <br><br>
</div>
<a href = "https://ko.javascript.info/settimeout-setinterval"> 참고자료 </a>
