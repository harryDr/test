# test

### 使用Vue+Element前端导入导出Excel

* npm install --save xlsx file-saver npm install -D script-loader 样式的话需要：npm install --save xlsx-style (安装后没有 xlsx-style得话需要下载npm install --save yxg-xlsx-style) 
    注意：如果安装了npm install --save xlsx-style 会报错：This relative module was not found: . /cptable in . /node_modules/xlsx-style@0. 8. 13@xlsx-style/dist/cpexcel. js 
    可以直接修改源 码： 在\node_modules\xlsx-style\dist\cpexcel. js 807行 的 var cpt = require(’. /cpt’ + ‘able’); 改成 var cpt = cptable; 

* 需要下载 (放在同一个文件夹下 src/vendor) Blob. js -- 无需修改 Export2Excel. js -- 需要改样式的话需要修改文件 
* vue文件中调用 (导出按钮触发事件) 
```exportExcel(res) { 
    require. ensure([], () => { const { export_json_to_excel } = require("@/vendor/Export2Excel");
    const tHeader = [["商品名称", "描述", "价格", "数量", "图片"]]; //对应表格输出的title 
    const filterVal = ["shopName", "description", "price", "number", "img"]; // 对应表格输出的数据 
    const list = this. tableData; 
    const data = this. formatJson(filterVal, list); //根据Export2Excel中的方法可以进行修改 定制化 
    export_json_to_excel({header: tHeader, data, filename: '筛分录入', autoWidth: false, bookType: 'xlsx'}); });
  }, 
  formatJson(filterVal, jsonData) { return jsonData. map(v => filterVal. map(j => v[j])); }, 
```
