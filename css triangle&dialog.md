 # 使用css画三角形
  *css画三角形的原理：利用border来实现三角形。
   1.给div一个border
   ```
    //整个div宽高30px border为10px宽的线条 这样就类似与相框
    <div class="tragger"></div>
    .tragger {
      width: 30px;
      height: 30px;
      border: 10px rebeccapurple solid;
      border-color: #96ceb4 #ffeead #d9534f #ffad60;
    }
   ```
   2.div宽高设置为0
    ```
    //此时一个正方形中由4个三角形拼接而成
    <div class="tragger"></div>
    .tragger {
      width: 0;
      height: 0;
      border: 10px rebeccapurple solid;
      border-color: #96ceb4 #ffeead #d9534f #ffad60;
    }
   ```
   3.任意方向的三角形 （以下三角为例，其他方向类似）
   ```
    //此时一个正方形中由4个三角形拼接而成
    <div class="tragger"></div>
    .tragger {
      width: 0;
      height: 0;
      border-style: solid;  //实线
      border-width: 0 10px 20px; //线宽 要下 则上的宽度去掉 
      border-color: transparent transparent #d9534f ; //上 右 左 透明 下 存在有颜色
    }
   ```
   
   *css 聊天气泡对话框实现
    实现原理：行内块元素+伪类做小三角
   ```
    <div class="text-area">
      <span>聊天气泡对话框</span>
    </div>
    
    .text span{
        display: inline-block;//行内元素
        background-color: darkgray;
        padding: 5px 8px;
        margin: 10px 0 10px 10px;        
        border-radius: 4px;
        position: relative;
    }
    .text span::before{
        content: "";
        position: absolute;//调整对话框得位置
        left:-8px;
        width: 0;//画三角形
        height: 0;
        border-style: solid;
        border-width: 4px 8px 4px 0;
        border-color: transparent darkgray transparent;
    }
   ```
