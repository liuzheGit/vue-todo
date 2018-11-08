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
  components: {}
};
</script>

<style>
.icon {
  width: 1em;
  height: 1em;
  vertical-align: -0.15em;
  fill: currentColor;
  overflow: hidden;
}
#app{
  color: #B2B2B2;
}
header{
  display: flex;
  font-size: 24px;
  justify-content: space-between;
  padding: 8px;
  color: #A4A4A4;
}

header > span{
  /* border: 1px solid gray;      */
}
header .app-title{
  color: #2B2B2B;
}
.bottom{
  font-size: 30px;
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 4px;
  border-top: 1px solid #E9E9E9;
  background: #FFFFFF;
}
.bottom > ul{
  display: flex;
  justify-content: space-between;
}
.bottom li{
  margin: 0 20px;
}
</style>
