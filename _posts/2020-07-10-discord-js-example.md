---
title:  "discord.js 예제"
excerpt: "기본적인 예제"

toc: true
toc_sticky: true
toc_label: "페이지 목차"

categories:
  - discord
tags:
  - discord
  - example
  - javascript
last_modified_at: 2020-07-10T08:49:00+09:00
---


## 기본적인 예제

```js
const Discord = require('discord.js');
const client = new Discord.Client();

client.on('ready', () => {
  console.log(`로그인 이름: ${client.user.tag}`);
});

client.on('message', message => {
  if (message.content === '핑') {  //핑이라는 문자를 받으면 실행
    message.channel.send('퐁'); // 퐁이라고 출력
  }
});

client.login('token');
```
이런식으로 활용할수 있다