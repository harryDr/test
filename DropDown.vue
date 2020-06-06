<template>
  <div class="dropdown-container">
    <div class="search-module clearfix">
      <input
        class="search-text"
        @keyup="search($event)"
        :placeholder="placeholder"
        v-model="inputText"
        @click="show"
      />
      <span :class="isShowData?'search-icon-top':'search-icon-bottom'" @click="show"></span>
    </div>
    <ul class="list-module" v-if="isShowData" :class="isShowNone?'none':''">
      <li v-for="(item,index) in datalist" @click="appClick(item)" :key="index">
        <span class="list-item-text">{{item}}</span>
      </li>
    </ul>
    <ul class="list-module" v-show="isShowNone">
        <li>
            <span class="list-item-text">{{nodatatext}}</span>
        </li>
    </ul>
    <!-- <div class="tip__nodata" v-show="isShowNone">{{nodatatext}}</div> -->
  </div>
</template>
 
<script>
export default {
  data() {
    return {
      datalist: [],
      inputText: "",
      isShowData: false,
      isShowNone: false
    };
  },
  props: {
    itemlist: Array,
    placeholder: String,
    nodatatext: String
  },
  methods: {
    appClick: function(data) {
      this.$emit("item-click", data);
      this.inputText = data;
      this.isShowData = false;
    },
    // dataList : 需要展示的数据列表
    // serchString: 过滤所包含的字符串
    // return: 过滤后的list
    dataFilter(dataList, serchString) {
      let tempList = [];
      for (let i = 0; i < dataList.length; i++) {
        if (dataList[i].search(serchString) != -1) {
          tempList.push(dataList[i]);
        }
      }
      return tempList;
    },
    search: function(e) {
      this.datalist = this.itemlist;
      let searchvalue = e.currentTarget.value;
      this.$emit("inputValue", searchvalue);
      this.datalist = this.dataFilter(this.datalist, e.currentTarget.value);
      if (this.datalist.length === 0) {
        this.isShowNone = true;
        this.isShowData = false;
      } else {
        this.isShowData = true;
        this.isShowNone = false;
      }
    },
    show() {
      if (this.datalist.length === 0) {
        this.isShowNone = true;
        // this.isShowData = false;
      } else {
        // this.isShowData = true;
        this.isShowNone = false;
      }
      this.isShowData = !this.isShowData;
      if (this.inputText) {
        this.datalist = this.dataFilter(this.datalist, this.inputText);
      } else {
        this.datalist = this.itemlist;
      }
    }
  },
  mounted() {
    this.datalist = this.itemlist;
  }
};
</script>
 
<style scoped>
.dropdown-container {
  position: absolute;
  width: 200px;
  /* z-index:10; */
  /* box-shadow:0px 0px 10px #ccc; */
}
.dropdown-container._self-show {
  display: block !important;
}
.dropdown-container .search-module {
  position: relative;
  cursor: pointer;
}
.search-text {
  width: 96%;
  height: 30px;
  /* padding-right:2em; */
  padding-left: 0.5em;
  border-radius: 0.5em;
  box-shadow: none;
  border: 1px solid #ccc;
}
.dropdown-container .search-module .search-text:focus {
  border-radius: 0.5em;
  border-color: #2198f2;
}
.search-icon-top {
  position: absolute;
  top: 45%;
  right: 0.5em;
  color: #aaa;
  border-left: 6px solid transparent;
  border-right: 6px solid transparent;
  border-bottom: 6px solid #008fd4;
}
.search-icon-bottom {
  position: absolute;
  top: 45%;
  right: 0.5em;
  color: #aaa;
  border-left: 6px solid transparent;
  border-right: 6px solid transparent;
  border-top: 6px solid #008fd4;
}
.dropdown-container .list-module {
  max-height: 200px;
  overflow-y: auto;
  text-align: left;
  list-style: none;
  padding-left: 0.5em;
  box-shadow: 0px 0px 10px #ccc;
  border-radius: 0.5rem;
  margin-top: 0.5rem;
}

.dropdown-container .list-module li {
  list-style: none;
  padding: 0px;
  margin: 0.5em 0;
}
.dropdown-container .list-module li._self-hide {
  display: none;
}
.dropdown-container .list-module li:hover {
  cursor: pointer;
  color: #00a0e9;
  background: rgb(245, 247, 250);
}
.tip__nodata {
  font-size: 12px;
  margin-top: 1em;
}
.none{
    display: none;
}
</style>