# 左右布局
  * 左列定宽,右列自适应
  ```
    <div class="left">123</div>
    <div class="right">123</div>
    
    .left {
      float: left;
      width: 20%;
      height: 100%;
      background-color: fuchsia;
    }
    .right {
      margin-left: 100px; /*设置间隔，大于等于#left的宽度*/ //overflow: hidden;
      height: 100%;
      background-color: rosybrown;
    }
  ```
    Tip: 不设置float默认div默认是块级元素（display:block），占用一行。div设置float后脱离文档流宽度为内容的实际宽度（没有设置定宽）
    position实现
  ```
    <div class="parent">
      <div class="left">123</div>
      <div class="right">123</div>
    </div>
    .parent{position: relative;}  /*父相*/
    .left {
      position: absolute; /*子绝*/
      top: 0;
      left: 0;
      background-color: #f00;
      width: 100px;
      height: 500px;
    }
    .right {
      position: absolute; /*子绝*/
      top: 0;
      left: 100px; /*值大于等于#left的宽度*/
      right: 0;
      background-color: #0f0;
      height: 500px;
    }
  ```
  flex布局 使用flex:1/*均分了父元素剩余空间*/
  * 左列自适应,右列定宽 (反过来实现就可以)
  * 一列不定,一列自适应
    左列定宽中的定宽去除 left需要浮动
    
 *三列布局 
  左中定宽右自适应
  ```
    <div class="left">12312312312</div>
      <div class="mid">mid</div>
    <div class="right">123</div>
    .left {
      float: left;
      width: 200px;
      height: 100%;
      background-color: fuchsia;
    }
    .mid {
      float: left;
      width: 200px;
      height: 100%;
      background-color: forestgreen;
    }
    .right {
      height: 100%;
      background-color: rosybrown;
    }
  ```
  * 两侧定宽,中间自适应 (双飞翼布局)
  ```
      <div class="header">header</div>
        <!--中间栏需要放在前面-->
        <div class="parent">
            <div class="center">中间自适应</div>
            <div class="left">左列定宽</div>
            <div class="right">右列定宽</div>
        </div>
        <div class="footer">footer</div>
      </div>
      
      .header{
          height: 30px;
          background-color: floralwhite;
      }
      .parent{
          height: 500px;
      }
      .left{
          float: left;
          width: 100px;
          height: 500px;
          margin-left: -100%; /*调整#left的位置,值等于自身宽度*/
          background-color: darkblue
      }
      .center{
          float: left;
          width: 100%;
          height: 500px;
          background-color: #eeff2b;
      }
      .right{
          float: left;
          width: 100px;
          height: 500px;
          background-color: salmon;
           margin-left: -100px;  /*使right到指定的位置,值等于自身宽度*/
      }
      .footer{
          height: 30px;
          background-color: darkgray;
      }
  ```
  * 两侧定宽,中间自适应 (圣杯布局)  parent使用padding流出左右位置
  ```
    <div class="header">header</div>
      <!--中间栏需要放在前面-->
      <div class="parent">
        <div class="center">中间自适应</div>
        <div class="left">左列定宽</div>
        <div class="right">右列定宽</div>
      </div>
    <div class="footer">footer</div>
    .header {
      height: 30px;
      background-color: floralwhite;
    }
    .parent {
      padding: 0 220px 0 200px;
      overflow: hidden;
    }
    .left,
    .center,
    .right {
      position: relative;
      float: left;
      min-height: 130px;
      word-break: break-all;
    }

    .left {
      margin-left: -100%;
      left: -200px;
      width: 200px;
      background-color: red;
    }

    .right {
      margin-left: -220px;
      right: -220px;
      width: 220px;
      background-color: green;
    }

    .center {
      width: 100%;
      background-color: blue;
    }

    .footer {
      height: 30px;
      background-color: darkgray;
    }
  ```
  
  * 多列布局（等宽）
  ```
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
    <div class="item">4</div>
    
    .item{
      float: left;
      width: 25%; //取均值
      border: 1px red solid;
    }
    //或者使用flex
    .item{
      flex: 1; /*一起平分parent*/
    }
  ```
