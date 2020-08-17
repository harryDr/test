# css Center
  * 行内元素水平垂直居中：
    ```
      单行：
      text-align: center; //父级块元素（非块级则display: block;）
      line-height: 200px;
      
      多行：
      display: table-cell; //父级元素
      vertical-align:middle;

    ```
   * 块级元素水平垂直居中：
    -固定宽高
     ```
      fu:{
         width: 200px;
         height: 200px;
         position: relative;
      }
      zi:{
         width: 100px;
         height: 100px;
         position: absolute;
         
         //利用绝对定位让子元素基于父元素的左上角偏移50% 自身负偏移自己的一半
         top: 50%;
         left: 50%;
         margin-top: -50px;
         margin-left: -50px; 
         
         //calc计算 与上同原理
         top: calc(50% - 50px);
         left: calc(50% - 50px);
         
         //设置各个方向的距离都是0 margin: auto;便可以居中
         top: 0;
         left: 0;
         right: 0;
         bottom: 0;
         margin: auto;     
      }
     ```
    -不固定宽高
    ```
       fu:{
         width: 200px;
         height: 200px;
         position: relative;
       }
       zi:{
         position: absolute;
         top: 50%;
         left: 50%;
         //transform的translate属性 
         transform: translate(-50%, -50%);
       }
    ```
    -flex布局
    ```
     fu:{
         width: 200px;
         height: 200px;
         display: flex;
         justify-content: center;
         align-items: center;
       }
    ```
