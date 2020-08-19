# vue 插槽(slot)
  插槽: 子组件中预留一个槽，父组件在对应的槽中插入自己的内容(有默认的槽)。
  
  * 内容插槽 (填充内容，可以使用默认槽) 
  ```
    //father.vue
    <child></child> //使用默认插槽
    <child>提交</child> //插入自己内容
    
    //child.vue
    <div>
      <button>
        <slot>Submit</slot>
      </button>
    </div>
  ```
  * 具名插槽 (一个组件中又多个插槽 使用name来区分插槽)
  ```
  //father.vue
    <child>
      i am default  //使用默认插槽
      <div slot="header">i am header</div>
      <div slot="footer">i am footer </div>
    </child> 
    
    //child.vue
    <div>
      <header>
        <slot name="header"></slot>
      </header>

      <main>
        <slot></slot>  //没有name则是默认的插槽
      </main>

      <footer>
        <slot name="footer"></slot>
      </footer>
    </div>
    
    //输出
    i am header
    i am default
    i am footer

  ```
  
