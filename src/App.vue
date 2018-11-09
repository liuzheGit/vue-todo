<template>
  <div id="app">
    <header>
      <span>
        <svg class="icon" aria-hidden="true">
            <use xlink:href="#icon-liebiao"></use>
        </svg>
      </span>
      <span class="app-title">TODO</span>
      <span>
        <svg class="icon" aria-hidden="true">
            <use xlink:href="#icon-moreread"></use>
        </svg>
      </span>
    </header>
    <!-- 主体 -->
    <div class="app-content">
      <ul class="list-container">
        <li v-for="item in noFinish" v-bind:key="item.id">
          <label>
            <input type="checkbox" class="check-input" v-bind:checked="item.state" @input="changeBox(item.id)">
            <span></span>
          </label>
          <span class="list-words">{{item.text}} <span class="del-btn" @click="deleteItem(item.id)">删除</span></span>
        </li>
      </ul>
    <div class="untodo-title">已完成</div>
    <ul class="list-container untodo-ul">
        <li v-for="item in yesfinish" v-bind:key="item.id">
          <label>
            <input type="checkbox" class="check-input" v-bind:checked="item.state" @input="changeBox(item.id)">
            <span></span>
          </label>
          <span class="list-words">{{item.text}} <span class="uodo-btn del-btn" @click="deleteItem(item.id)">删除</span></span>
        </li>
      </ul>
    </div>
    <div class="app-add">
      <svg class="icon" aria-hidden="true">
        <use xlink:href="#icon-jiaru"></use>
      </svg> 
    </div>
<!-- 底部 -->
    <div class="bottom">
      <ul>
        <li>
          <svg class="icon" aria-hidden="true">
            <use xlink:href="#icon-wancheng"></use>
          </svg>
        </li>
        <li>
          <svg class="icon" aria-hidden="true">
            <use xlink:href="#icon-shangdian"></use>
          </svg>
        </li>
        <li>
          <svg class="icon" aria-hidden="true">
            <use xlink:href="#icon-fanqie-danse-"></use>
          </svg>
        </li>
        <li>
          <svg class="icon" aria-hidden="true">
            <use xlink:href="#icon-shezhi"></use>
          </svg>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  components: {},
  data() {
    return {
      initId: 100,
      myList: [
        {
          id: 0,
          text: '选项1',
          state: true
        },
        {
          id: 1,
          text: '选项2',
          state: false
        }, 
        {
          id: 3,
          text: '选项3',
          state: true
        }, 
        {
          id: 4,
          text: '选项4',
          state: true
        } 
      ],
      newItem:{
        id: this.initId,
        state: false,
        text: ''
      }
    };
  },
  computed: {
    noFinish(){
      return this.myList.filter((item) =>{
        return item.state === false
      })
    },
    yesfinish(){
      return this.myList.filter((item) =>{
        return item.state === true
      })
    }
  },
  methods: {
    changeBox(id){
      var item = this.myList.filter((item) =>{
        return item.id === id
      })
      item[0].state =!item[0].state
    },
    deleteItem(id){
      var temp = this.myList.filter((item)=>{
        return item.id !== id
      })
      this.myList = temp;
    }
  }
};
</script>

<style>
html,body{
  height: 100%;
}


.icon {
  width: 1em;
  height: 1em;
  vertical-align: -0.15em;
  fill: currentColor;
  overflow: hidden;
}
#app {
  height: 100%;
  background: #EFF1F0;
  color: #b2b2b2;
}
header {
  display: flex;
  font-size: 24px;
  justify-content: space-between;
  padding: 8px;
  color: #a4a4a4;
  background: #fff;
  border-bottom: 3px solid #EFF1F0;
}

header .app-title {
  color: #2b2b2b;
}
.bottom {
  font-size: 30px;
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 4px;
  border-top: 1px solid #e9e9e9;
  background: #ffffff;
}
.bottom > ul {
  display: flex;
  justify-content: space-between;
}
.bottom li {
  margin: 0 20px;
}

.check-input {
  appearance: none;
  -webkit-appearance: none;
  display: none;
  outline: none;
}
.check-input + span {
  width: 16px;
  height: 16px;
  display: inline-block;
  background: #f00;
  background: url("./assets/checkbox-icon.png");
  background-position-x: -5px;
  background-position-y: -31px;
  cursor: pointer;
}
.check-input:checked + span {
  background-position-y: -5px;
}


.list-container{
  padding: 12px;
  color: #000;
  background: #fff;
}
.list-container > li{
  margin-top: 4px;
}
.list-container .del-btn{
  border: 1px solid gray;
  font-size: 14px;
  padding: 2px 4px;
  border-radius: 3px;
  float: right;
}

.untodo-ul .list-words{
  color: #0b040470;
}

.untodo-ul .uodo-btn{
  color: #0b040470;
}
.list-container .list-words{
  margin-left: 16px;
}

.untodo-title{
  padding: 4px 8px;
  color: #9C9C9C;
  font-weight: 200;
  font-size: 12px;
}


.app-add{
  position: fixed;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  bottom: 50px;
  right: 10px;
  background: #7E7F83;
  text-align: center;
  line-height: 40px;
  box-shadow: 0px 1px 8px 0px black;
}
</style>
