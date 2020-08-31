#websocket 通信
  1.HTTP协议是一种无状态、无连接、单向的应用层协议，只能由客户端发起请求，服务端响应请求。 （长轮询实现双向通信，缺点就是效率低、非常耗费资源）
  2.websocket协议是一个长连接，客户端可以给服务端发送消息，服务端也可以给客户端发送消息，这便是全双工通信。node中使用ws模块来实现websocket。
  ```
    sockit.js//服务器js文件
    
    const WebSocket = require('ws');//引入ws模块
    const server = new WebSocket.Server({ port: 8080 }); //端口8080
    server.on('open', function open() { //监听开启服务
      console.log('connected');
    });

    server.on('close', function close() { //监听关闭服务
      console.log('disconnected');
    });

    server.on('connection', function connection(ws, req) { //监听连接通道 新用户加入、某一个用户发信息等
      const ip = req.connection.remoteAddress;
      const port = req.connection.remotePort;
      const clientName = ip + port;
      console.log('%s is connected', clientName)
      // 初次连接 发送欢迎信息给客户端
      ws.send("Welcome " + clientName);
      ws.on('message', function incoming(message) {
        console.log('received: %s from %s', message, clientName);
        // 广播消息给所有客户端
        server.clients.forEach(function each(client) {
          if (client.readyState === WebSocket.OPEN) {
            client.send( clientName + " -> " + message);
          }
        });
      });
    });
    
    //html
    <body>
      <form onsubmit="return false;">
          <h3>WebSocket 聊天室：</h3>
          <textarea id="responseText" style="width: 500px; height: 300px;"></textarea>
          <br>
          <input type="text" name="message" style="width: 300px" value="Welcome to waylau.com">
          <input type="button" value="发送消息" onclick="send(this.form.message.value)">  //js事件
          <input type="button" onclick="javascript:document.getElementById('responseText').value=''" value="清空聊天记录">
      </form>
      <br>
      <br>
    </body>
  
    //js
    var socket;
    if (!window.WebSocket) {
        window.WebSocket = window.MozWebSocket;
    }
    if (window.WebSocket) {
        socket = new WebSocket("ws://127.0.0.1:8080/ws");  //新建一个websocke连接 IP（服务器IP）：端口
        socket.onmessage = function (event) {
            var ta = document.getElementById('responseText');
            ta.value = ta.value + '\n' + event.data
        };
        socket.onopen = function (event) {
            var ta = document.getElementById('responseText');
            ta.value = "连接开启!";
        };
        socket.onclose = function (event) {
            var ta = document.getElementById('responseText');
            ta.value = ta.value + "连接被关闭";
        };
    } else {
        alert("你的浏览器不支持 WebSocket！");
    }

    function send(message) {
        if (!window.WebSocket) {
            return;
        }
        if (socket.readyState == WebSocket.OPEN) {
            socket.send(message);
        } else {
            alert("连接没有开启.");
        }
    }
  ```
