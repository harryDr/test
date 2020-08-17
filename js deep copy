# js深浅拷贝
  * js基础类型和引用类型
  ```
    js 基础类型：(基本数据类型存放在栈中) 
      String、Number、boolean、null、undefined
    js 引用类型：(引用类型存放在堆中)
      Object、Array、Function、Data
  ```
  * 基础类型的拷贝(基础类型的拷贝是在栈中存储的值)
  ```
      栈内存
      name  val
       a     1
  ```
  * 引用类型的拷贝(引用类型的拷贝是在栈内存中存储堆内存的值)
  ```
      栈内存
      name      val
       a     堆内存地址
  ```
  * 深浅拷贝(只针对引用类型)
    * 浅拷贝：(只是拷贝堆内存的地址)
    ```
      let a = [1,2,3];
      let b = a;
      b[1] = '二';
      console.log(a,b) // [1, "二", 3] (3) [1, "二", 3]
    ```
    * 深拷贝：(堆内存的值也拷贝)
    ```
      //递归
      function deepClone(data){
         var type = typeof(data);
         var obj;
         if(type === 'array'){
             obj = [];
         } else if(type === 'object'){
             obj = {};
         } else {
             //不再具有下一层次
             return data;
         }
         if(type === 'array'){
             for(var i = 0, len = data.length; i < len; i++){
                 obj.push(deepClone(data[i]));
             }
         } else if(type === 'object'){
             for(var key in data){
                 obj[key] = deepClone(data[key]);
             }
         }
         return obj;
     }
     
     //JSON 方式
     function deepClone(data) {
        return JSON.parse(JSON.stringify(data));
      }
    ```
