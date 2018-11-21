<template>
  <div class="app-content">
    <!--这边是没完成的展示区-->
    <ul class="list-container" v-if="noFinish.length">
      <li v-for="item in noFinish" v-bind:key="item.id">
        <label>
          <input type="checkbox" class="check-input" v-model="item.state">
          <span></span>
        </label>
        <span class="list-words">{{item.text}} </span><span class="del-btn" @click="$emit('delete', item.id)">删除</span>
      </li>
    </ul>
    <div v-else class="noList">任务完成的很好 继续加油</div>
    <!--展示区end 下边是已完成-->
    <div class="untodo-title">已完成</div>
    <ul class="list-container untodo-ul">
      <li v-for="item in yesfinish" v-bind:key="item.id">
        <label>
          <input type="checkbox" class="check-input" v-model="item.state">
          <span></span>
        </label>
        <span class="list-words">{{item.text}} </span><span class="uodo-btn del-btn" @click="$emit('delete', item.id)">删除</span>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: "TodoList",
    props:['myList'],
    computed: {
      noFinish(){
        return this.myList.filter((item) => {
          return item.state === false;
        });
      },
      yesfinish(){
        return this.myList.filter((item) =>{
          return item.state === true;
        });
      }
    }
  }
</script>

<style scoped>
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
</style>