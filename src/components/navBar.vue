<template>
    <div class="nav-wrapper">
      <div class="nav-content">
        <ul class="nav-list">
          <li class="nav-item" v-for="(navImg,nav,index) in navData" @click="navShowList(navImg,nav,index)">
            <img class="pic" :src="dpr>2 ? navImg.img2x : navImg.img3x" >
            <img class="dot" :src="dpr>2 ? currentDot.img2x : currentDot.img3x" v-show="currentNav===nav">
          </li>
        </ul>
      </div>
    </div>
</template>

<script>
    export default {
      name: "navBar",
      props:{
        dpr: {
          type:Number
        },
        show: {
          type:Boolean
        }
      },
      data() {
        return {
          currentNav: "",
          navData:{
            all:{
              img2x:require("./全部@2x.png"),
              img3x:require("./全部@3x.png"),
            },
            recommend:{
              img2x:require("./推荐@2x.png"),
              img3x:require("./推荐@3x.png")
            },
            change:{
              img2x:require("./换一批@2x.png"),
              img3x:require("./换一批@3x.png")
            },
            share:{
              img2x:require("./分享@2x.png"),
              img3x:require("./分享@3x.png")
            }
          },
          currentDot: {
            img2x:require("./椭圆1@2x.png"),
            img3x:require("./椭圆1@3x.png")
          },
        }
      },
      methods:{
        navShowList(navImg,nav,index) {
          this.$emit("show-list");
          this.currentNav = nav;
        }
      }
    }
</script>

<style scoped>
  .nav-wrapper {
    flex: 0 42px;
    width: 100%;
    margin: 0;
    padding: 0;
    z-index: 10;
  }

  .nav-content {

    height: 42px;
    width: 100%;
  }

  .nav-list {
    padding: 0;
    margin: 0;
    height: 42px;
    line-height: 42px;
    text-align: center;
    font-size: 0;
    vertical-align: middle;
  }

  .nav-item {
    display: inline-block;
    box-sizing: border-box;
    height: 42px;
    width: 25%;
    padding: 12px 0;
    line-height: 18px;
    text-align: center;
    vertical-align: middle;
    list-style-type: none;
    color: rgb(255,255,255);
  }

  .pic {
    height: 18px;
  }

  .dot {
    position: absolute;

    height: 6px;
  }


</style>
