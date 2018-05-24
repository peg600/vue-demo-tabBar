<template>
  <div class="wrapper">
    <div class="main">
       <p>
         {
         "name":"帽子4",
         "avatar":"http://fuss10.elemecdn.com/f/28/a51e7b18751bcdf871648a23fd3b4jpeg.jpeg?imageView2/1/w/114/h/114",
         "price":33
         },
         {
         "name":"帽子5",
         "avatar":"http://fuss10.elemecdn.com/f/28/a51e7b18751bcdf871648a23fd3b4jpeg.jpeg?imageView2/1/w/114/h/114",
         "price":34
         },
         {
         "name":"帽子6",
         "avatar":"http://fuss10.elemecdn.com/f/28/a51e7b18751bcdf871648a23fd3b4jpeg.jpeg?imageView2/1/w/114/h/114",
         "price":35
         },
         {
         "name":"帽子7",
         "avatar":"http://fuss10.elemecdn.com/f/28/a51e7b18751bcdf871648a23fd3b4jpeg.jpeg?imageView2/1/w/114/h/114",
         "price":36
         },
         {
         "name":"帽子8",
         "avatar":"http://fuss10.elemecdn.com/f/28/a51e7b18751bcdf871648a23fd3b4jpeg.jpeg?imageView2/1/w/114/h/114",
         "price":37
         },
         {
         "name":"帽子9",
         "avatar":"http://fuss10.elemecdn.com/f/28/a51e7b18751bcdf871648a23fd3b4jpeg.jpeg?imageView2/1/w/114/h/114",
         "price":38
         },
         {
         "name":"帽子10",
         "avatar":"http://fuss10.elemecdn.com/f/28/a51e7b18751bcdf871648a23fd3b4jpeg.jpeg?imageView2/1/w/114/h/114",
         "price":39
         },
         {
         "name":"帽子11",
         "avatar":"http://fuss10.elemecdn.com/f/28/a51e7b18751bcdf871648a23fd3b4jpeg.jpeg?imageView2/1/w/114/h/114",
         "price":40
         },
         {
         "name":"帽子12",
         "avatar":"http://fuss10.elemecdn.com/f/28/a51e7b18751bcdf871648a23fd3b4jpeg.jpeg?imageView2/1/w/114/h/114",
         "price":41
         }
         ]
         },
         "earrings":{
         "message":{
         "type":3,
         "name":"耳环",
         "avatar":"http://fuss10.elemecdn.com/d/b9/bcab0e8ad97758e65ae5a62b2664ejpeg.jpeg?imageView2/1/w/114/h/114"
         }
         },
         "hairpins":{
         "message":{
         "type":4,
         "name":"发卡",
         "avatar":"http://fuss10.elemecdn.com/7/72/9a580c1462ca1e4d3c07e112bc035jpeg.jpeg?imageView2/1/w/114/h/114"
         }
         },
         "shoes":{
         "message":{
       </p>
    </div>
    <div class="footer">
      <tabBar :items="items" v-if="this.items"></tabBar>
    </div>
  </div>

</template>

<script>
import axios from "axios"
import tabBar from "./components/tabBar.vue"

export default {
  name: 'App',
  data() {
    return {
      items:{},
      response:{}
    }
  },
  created() {
    axios.get("../static/test.json").then((response) => {
      response = response.data;
      this.items = response.items;
    })
  },
  components:{
    tabBar
  }
}
</script>

<style>
.wrapper {
  display: flex;
  width:100%;
  min-height: 100%;
  flex-direction: column;
}

p {
  word-wrap: break-word;
}

.main {
  flex:1;
  background-color: green;
}

.footer {
  background-color: aqua;
  flex:0 50px;
}
</style>
