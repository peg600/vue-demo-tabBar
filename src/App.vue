<template>
  <div class="wrapper">
    <div class="content">
      <navBar :dpr="dpr" @show-list="showList" :show="show"></navBar>
      <div class="main">
      </div>
    </div>
    <buttons :dpr="dpr" @show-list="showList" :show="show"></buttons>
    <tabBar :items="items" :show="show" :listArray="listArray"></tabBar>
  </div>

</template>

<script>
import axios from "axios"
import navBar from "./components/navBar.vue"
import buttons from "./components/buttons.vue"
import tabBar from "./components/tabBar.vue"

export default {
  name: 'App',
  data() {
    return {
      dpr:1,
      items:{},
      response:{},
      show:false,
      listArray:[],
    }
  },

  created() {
    axios.get("../static/standard1.json").then((response) => {      //@touchmove.prevent
      response = response.data;
      this.items = response.list;
    });
    this.dpr=window.devicePixelRatio;

  },

  mounted() {

  },

  methods:{
    showList() {
      this.show = true;
      let address = "";
      let itemsAddress = Object.keys(this.items);
      let length = itemsAddress.length;
      for (let i = 1;i<length+1;i++) {
        address = `../static/${i}.json`;
        axios.get(address).then((response) => {
          if (response) {
            response = response.data.list;
            this.listArray[i] = response;
          }
        });
      }
    },
    hideList() {
      this.show = false;
    }
  },

  computed:{

  },

  components:{
    navBar,
    buttons,
    tabBar
  }
}
</script>

<style>

html,body {
  height: 100%;
  margin: 0;
  padding: 0;
  overflow: hidden;
  box-sizing: border-box;
  background-image: url("./background.jpg");
}

.wrapper {
  height: 100%;
  width: 100%;
}

.content {
  position: absolute;
  display: flex;
  top: 0;
  bottom: 0;
  max-height: 100%;
  width: 100%;
  flex-direction: column;
}

.main {
  flex: 1;
  box-sizing: border-box;
  width: 100%;
  overflow: auto;
  z-index: 5;
}



</style>
