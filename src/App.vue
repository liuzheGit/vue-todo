<template>
  <div id="app">
    <header>
      <!--<span>-->
        <!--<svg class="icon" aria-hidden="true">-->
            <!--<use xlink:href="#icon-liebiao"></use>-->
        <!--</svg>-->
      <!--</span>-->
      <span class="app-title">TODO</span>
      <!--<span>-->
        <!--<svg class="icon" aria-hidden="true">-->
            <!--<use xlink:href="#icon-moreread"></use>-->
        <!--</svg>-->
      <!--</span>-->
    </header>
    <!-- 主体 -->
    <div class="app-content">
      <div v-if="noFinish.length === 0" class="noList">
        任务完成的很好 继续加油
      </div>
      <ul v-else class="list-container">
        <li v-for="item in noFinish" v-bind:key="item.id">
          <label>
            <input type="checkbox" class="check-input" v-model="item.state">
            <span></span>
          </label>
          <span class="list-words">{{item.text}} <span class="del-btn" @click="deleteItem(item.id)">删除</span></span>
        </li>
      </ul>
    <div class="untodo-title">已完成</div>
    <ul class="list-container untodo-ul">
        <li v-for="item in yesfinish" v-bind:key="item.id">
          <label>
            <input type="checkbox" class="check-input" v-model="item.state">
            <span></span>
          </label>
          <span class="list-words">{{item.text}} <span class="uodo-btn del-btn" @click="deleteItem(item.id)">删除</span></span>
        </li>
      </ul>
    </div>
    <div class="app-add" v-on:click="showInput">
      <svg class="icon" aria-hidden="true">
        <use xlink:href="#icon-jiaru"></use>
      </svg> 
    </div>

    <div class="app-input" v-bind:class="{active : inputState}">
      <input type="text" placeholder="例如: 6点下班去超市买零食" v-model="newItemText"><button class="input-add" @click="addList">添加</button>
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
      initId: null,
      myList: [
        {
          id: 0,
          text: '新建todo项目',
          state: true
        },
        {
          id: 1,
          text: 'input加上',
          state: false
        },
        {
          id: 3,
          text: '获取设备',
          state: true
        },
        {
          id: 4,
          text: 'iscroll',
          state: true
        },
        {
          id: 5,
          text: '看react文档',
          state: false
        },
        {
          id: 6,
          text: '买菜',
          state: false
        }
      ],
      newItemText: '',
      myChecked: true,
      inputState: false
    };
  },
  created() {
    let localData = localStorage.getItem("todo");
    this.myList = JSON.parse(localData) || [];
    let randomId = localStorage.getItem('todoId') || this.getRandom(10, 50);
    this.initId = +randomId;
  },
  computed: {
    noFinish() {
      return this.myList.filter((item) => {
        return item.state === false;
      });
    },
    yesfinish() {
      return this.myList.filter((item) =>{
        return item.state === true;
      });
    }
  },
  methods: {
    addList() {
      let temp = this.newItemText;
      if(temp !== ''){
        this.initId = this.initId + 1;
        let id = this.initId;

        let newObj = {
          id,state: false,text: temp
        };
        this.myList.unshift(newObj);
        this.newItemText = '';
      }
      this.saveStore(this.myList);
    },
    deleteItem(id) {
      let temp = this.myList.filter((item)=>{
        return item.id !== id;
      });
      this.myList = temp;
      this.saveStore(this.myList);
    },
    saveStore(data) {
      localStorage.setItem('todo', JSON.stringify(data));
      localStorage.setItem('todoId', this.initId);
    },
    myLog(){
      // console.log('我出发了')
    },
    getRandom(min, max){
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min)) + min;
    },
    showInput(){
      this.inputState = !this.inputState;
    }
  },
  watch: {
    myList:{
      handler(newValue){
        this.saveStore(newValue);
      },
      deep: true
    }
  }
};
</script>

<style>
html,
body{
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
  background: #eff1f0;
  color: #b2b2b2;
}
header {
  display: flex;
  font-size: 24px;
  justify-content: center;
  padding: 8px;
  color: #a4a4a4;
  background: #fff;
  border-bottom: 3px solid #eff1f0;
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
  display: none;
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
.list-container,.noList {
  padding: 12px;
  color: #000;
  background: #fff;
}
.noList {
  font-size: 12px;
}
.list-container > li {
  margin-top: 4px;
}
.list-container .del-btn {
  border: 1px solid gray;
  font-size: 14px;
  padding: 2px 4px;
  border-radius: 3px;
  float: right;
}

.untodo-ul .list-words {
  color: #0b040470;
}

.untodo-ul .uodo-btn {
  color: #0b040470;
}
.list-container .list-words {
  margin-left: 16px;
}

.untodo-title {
  padding: 4px 8px;
  color: #9c9c9c;
  font-weight: 200;
  font-size: 12px;
}

.app-add {
  position: fixed;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  bottom: 50px;
  right: 10px;
  background: #7e7f83;
  text-align: center;
  line-height: 40px;
  box-shadow: 0 1px 8px 0 black;
}

.app-input {
  position: fixed;
  bottom: 0;
  z-index: 10;
  background: #f0f0f0;
  padding: 6px 8px;
  width: 100%;
  box-shadow: 0 -1px 20px 0 #0000006e;
  display: none;
}
.app-input.active{
  display: block;
}
.app-input input {
  width: 100%;
  vertical-align: top;
  border: none;
  outline: none;
  margin: 2px 4px;
  border-radius: 3px;
  height: 30px;
  padding: 0 20px 0 4px;
  font-size: 16px;
}

.app-input .input-add {
  margin-left: 5px;
  position: absolute;
  right: 12px;
  top: 12px;
  outline: none;
  border: none;
  font-size: 14px;
  padding: 2px 8px;
  border-radius: 2px;
}
</style>
