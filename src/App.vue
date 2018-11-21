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
    <TodoList
      v-bind:myList="myList"
      v-on:delete="deleteItem"
    />
    <div class="app-add" v-on:click="showInput">
      <svg class="icon" aria-hidden="true">
        <use xlink:href="#icon-jiaru"></use>
      </svg> 
    </div>

    <div class="app-input" v-bind:class="{active : inputState}">
      <input ref="inputAdd" type="text" @keydown.enter="addList" placeholder="例如: 6点下班去超市买零食" v-model="newItemText"><button class="input-add" @click="addList">添加</button>
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
import TodoList from './components/TodoList'
export default {
  name: "app",
  components: { TodoList },
  data() {
    return {
      initId: null,
      myList: [],
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
    getRandom(min, max){
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min)) + min;
    },
    showInput(){
      this.inputState = !this.inputState;
      if (this.inputState === true) {
        setTimeout(() => {
          this.$refs.inputAdd.focus();
        }, 10);
      }
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
