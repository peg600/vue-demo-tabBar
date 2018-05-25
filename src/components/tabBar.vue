<template>
  <div class="tabBar-content" ref="tabBarContent">
    <div class="wrapper" ref="itemWrapper">
      <ul class="item-wrapper" v-if="items" ref="itemList">
        <li class="item" :class="{'active-item': activeType === item_message.message.type}" v-for="(item_message,item,index) in items"
            @click="showItemList($event,item_message)">
          <div class="content">
            <span class="item-name" >{{item_message.message.name}}</span>
            <img class="item-avatar" v-if="item_message.message.avatar"
               :src="item_message.message.avatar" height="20px" width="20px">
          </div>
        </li>
      </ul>
      <list :showList="showList" :itemMessage="itemMessage"></list>
    </div>
  </div>
</template>
<script>
  import BScroll from "better-scroll"
  import list from "./list.vue"

  export default {
    name: "tabBar",
    props:{
      items:{
        type:Object
      }
    },
    data() {
      return {
        showList:false,
        activeType:0,
        itemMessage:{}
      }
    },
    watch: {
      "items"() {
        this.$nextTick(() => {
          this._initScroll();
        });
      }
    },
    mounted() {
      this.$nextTick(() => {
        this._initScroll();
      });
    },
    methods:{
      _initScroll() {
        if (this.items) {
          let itemsArray = Object.keys(this.items);
          let screenWidth = document.body.scrollWidth;
          let margin = 6;
          let itemWidth = (screenWidth-2*margin)/4;
          let width = (itemWidth + margin) * itemsArray.length - margin;    // 计算所有图片总宽度，即ul宽度
          this.$refs.itemList.style.width = width + "px";    // 为图片列表设置宽度，只有宽度大于容器才能滚动
          this.$nextTick(() => {
            if (!this.itemScroll) {
              this.itemScroll = new BScroll(this.$refs.itemWrapper, {
                scrollX: true,                        // 横向滚动
                eventPassthrough: "vertical"        // 在横向滚动时忽略纵向滚动
              });
            } else {
              this.itemScroll.refresh();
            }
          });
        }
      },
      showItemList(e,item_message) {
        if(this.activeType && this.activeType === item_message.message.type) {
          this.showList = false;           // 若点击的是展示状态的tab，则取消展示状态并收起列表
          this.activeType = 0;
          this.itemMessage = {};
          this.$emit("hide-list");
          this.$refs.tabBarContent.style.height = 50+"px";
          console.log(this.itemMessage,this.showList,this.activeType);
        }else{                              // 若点击非展示状态的tab，将其标记为展示中并弹出列表
          this.activeType = item_message.message.type;
          this.showList = true;
          this.itemMessage = item_message;// 准备将itemMessage传给list组件
          this.$emit("show-list");
          this.$refs.tabBarContent.style.height = 300+"px";
          console.log(this.itemMessage,this.showList,this.activeType);
        }
      }
    },
    components:{
      list
    }
  }
</script>

<style scoped>

  .tabBar-content {
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 50px;
    background-color: aqua;
  }

  .wrapper {
    width: 100%;
    overflow: hidden;
    white-space: nowrap;
  }

  .item-wrapper {
    display: flex;
    font-size: 0;
    margin-top: 10px;
    padding-left: 0;
    box-sizing: border-box;
  }

  .item {
    flex:1;
    height: 24px;
    line-height: 24px;
    color: #059;
    font-size: 20px;
    padding-right: 6px;
    list-style-type: none;
    border-right: solid red 1px;
  }

  .item:last-child {
    margin-right: 0;
    border-right: none;
  }

  .content {
    text-align: center;
    margin: 0;
    padding: 0;
  }

  .item-name,.item-avatar {
    display: inline-block;
    vertical-align: middle;
  }

  .active-item{
    flex:1;
    height: 24px;
    line-height: 24px;
    color: #059;
    font-size: 20px;
    padding-right: 6px;
    list-style-type: none;
    border-right: solid red 1px;
    background-color: chartreuse;
  }
</style>
