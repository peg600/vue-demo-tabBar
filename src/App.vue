<template>
  <div class="wrapper">
    <div class="content">
      <navBar :dpr="dpr" @show-list="showList" :show="show"></navBar>
      <div class="main">
      </div>
    </div>
    <buttons :dpr="dpr" @show-list="showList" :show="show"></buttons>
    <tabBar :items="items" :show="show" :listArray="listArray" :firstUrl="firstUrl" :firstLength="firstLength"></tabBar>
  </div>

</template>

<script>
import axios from "axios"
import $ from "jquery"
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
      firstUrl:"https://www.zhaoxinzx.top/server/index.php?m=default&c=category",
      firstLength:0
    }
  },

  created() {
    this.dpr=window.devicePixelRatio;
    this.getAjax();
  },

  mounted() {

  },

  methods:{
    getAjax() {
      const _vue = this;
      $.ajax({
        url:_vue.firstUrl,
        type:'GET', //GET
        async:true, //或false,是否异步
        timeout:5000, //超时时间
        dataType:'json', //返回的数据格式：
        success:function(data,textStatus,jqXHR) {
          _vue.items = data.list;
          let itemsArray = Object.keys(_vue.items);
          _vue.firstLength = itemsArray.length;
          //console.log(_vue.items);
        },
        complete:function(){
          for (let i = 0; i < _vue.firstLength; i++) {
            _vue.listArray[i+2] = [];
            //console.log(_vue.listArray)
            let secondUrl = `${_vue.firstUrl}&a=getproducts&id=${i + 2}`;
            for (let j = 1; j < 4; j++) {
              let itemUrl = `https://www.zhaoxinzx.top/server/?c=category&a=getproducts&id=${i+2}&page=${j}`;
              $.ajax({
                url: itemUrl,
                type: 'GET', //GET
                async: true, //或false,是否异步
                timeout: 5000, //超时时间
                dataType: 'json', //返回的数据格式：
                success: function (data2, textStatus, jqXHR) {
                  if(data2.list[0]) {
                    let temporary = data2.list;
                    _vue.renderList(i,j,temporary);
                  }
                },
                complete: function () {}
              });
            }
          }
        }
      });
    },

    showList() {
      this.show = true;
      this.getAjax();
      console.log(this.items);
      console.log(this.listArray)
      /*let address = "";
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
      }*/
    },
    hideList() {
      this.show = false;
    },

    renderList(i,j,temporary){
      this.listArray[i+2][j] = temporary;
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
  background-image: url("../static/background.jpg");
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
