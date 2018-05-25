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
         hats":{
         "message":{
         "type":2,
         "name":"帽子",
         "avatar":"http://fuss10.elemecdn.com/c/6b/29e3d29b0db63d36f7c500bca31d8jpeg.jpeg?imageView2/1/w/114/h/114"
         },
         "goods":[
         {
         "name":"帽子1",
         "avatar":"http://fuss10.elemecdn.com/f/28/a51e7b18751bcdf871648a23fd3b4jpeg.jpeg?imageView2/1/w/114/h/114",
         "price":30
         },
         {
         "name":"帽子2",
         "avatar":"http://fuss10.elemecdn.com/f/28/a51e7b18751bcdf871648a23fd3b4jpeg.jpeg?imageView2/1/w/114/h/114",
         "price":31
         },
         {
         "name":"帽子3",
         "avatar":"http://fuss10.elemecdn.com/f/28/a51e7b18751bcdf871648a23fd3b4jpeg.jpeg?imageView2/1/w/114/h/114",
         "price":32
         },
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

       </p>
    </div>
    <tabBar :items="items" @show-list="showList" @hide-list="hideList"></tabBar>
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
  methods:{
    showList() {

    },
    hideList() {
      console.log("hide")
    }
  },
  components:{
    tabBar
  }
}
</script>

<style>

html,body {
  height: 100%;
  margin: 0;
  padding: 0;
}

.wrapper {

  position: relative;
  width:100%;
  min-height: 100%;
}

p {
  word-wrap: break-word;
}

.main {

  background-color: green;
}



</style>
