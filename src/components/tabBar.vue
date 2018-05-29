<template>
  <div class="tab-wrapper" ref="tabWrapper" v-show="show">
    <div class="tab-content" ref="itemWrapper">
      <ul class="item-list" ref="itemList" :style="this.itemListWidth">
        <li class="clear">
          <img  class="img-clear" :src="dsr>2 ? require('./关闭@2x.png') : require('./关闭@3x.png')">
        </li>
        <li class="command" :class="{'active-item': activeType === -1}"
            @click="showItemList($event)">
          热销
        </li>
        <li class="item"  :class="{'active-item': activeType === item_message.id}"
            v-for="(item_message,item,index) in items" @click="showItemList($event,item_message,index)">
          <div class="item-content">
            <span class="item-name" >
              {{item_message.name}}
            </span>
          </div>
        </li>
      </ul>
    </div>

    <div class="goods-content">
      <div class="goods-wrapper" ref="outWrapper">
        <div class="goods-type-wrapper" ref="innerWrapper" :style="this.listWidth">
          <div class="goods-type" v-for="(itemType,itemTypeIndex) in items"
               ref="goodsType" :style="screenWidth" :key="itemType.id">
            <ul class="goods-list">
              <div class="item-page" v-for="(page,pageIndex) in listArray[itemType.id]">
                <li class="goods-item" v-for="(goods,$goodsindex) in page"
                    @click="selectItem(goods,$goodsindex)"
                    :class="{'selected-item': selectedindex===$goodsindex}">
                  <a class="goods-link">
                    <!--<span class="item-name">{{item.name}}</span>-->
                    <img :src="goods.goods_thumb" alt="item.name" class="item-img"
                         height="75px" width="75px" >
                  </a>
                </li>
              </div>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  import BScroll from "better-scroll"
  import axios from "axios"

  export default {
    name: "tabBar",
    props:{
      listArray:{
        type:Array
      },
      show:{
        type:Boolean
      },
      items:{
        type:Object
      },
      dsr:{
        type:Number
      },
      firstUrl:{
        type:String
      },
      firstLength:{
        type:Number
      }
    },
    data() {
      return {
        activeType:-1,
        itemMessage:{},
        itemListWidth:"",
        listWidth:"",
        screenWidth:"",
        fullWidth:0,
        selected:[],
        selectedindex:-1,
        scrollX:0,
        distance:[],
        length:0
      }
    },

    created() {
      this.$nextTick(() => {
        this.setWidth();
        this._initScroll();
        this._calculateWidth();
      })
    },

    watch:{
      "listArray"() {
        this._initScroll();
        this._calculateWidth();
      }
    },

    mounted() {
      setTimeout(() => {
        this._initScroll();

      }, 20);
    },

    methods:{
      aaa(itemTypeIndex) {
        console.log(123,itemTypeIndex)
      },
      setWidth() {
        let itemsArray = Object.keys(this.items);
        this.fullWidth = document.body.scrollWidth;
        this.screenWidth = `width: ${document.body.scrollWidth}px;`;
        let width = 67 * (itemsArray.length+1) + 40;    // 计算所有图片总宽度，即ul宽度
        this.length = itemsArray.length;
            // 为图片列表设置宽度，只有宽度大于容器才能滚动
        this.listWidth = `width: ${this.fullWidth * (this.length)}px`;
        this.itemListWidth = `width: ${width}px`;
      },

      _initScroll() {
        this.$nextTick(() => {
          if (this.items) {
            /*let itemsArray = Object.keys(this.items);
            this.fullWidth = document.body.scrollWidth;
            this.screenWidth = `width: ${document.body.scrollWidth}px;`;
            let width = 67 * (itemsArray.length+1) + 40;    // 计算所有图片总宽度，即ul宽度
            this.length = itemsArray.length;
            this.$refs.itemList.style.width = width + "px";    // 为图片列表设置宽度，只有宽度大于容器才能滚动
            this.listWidth = `width: ${this.fullWidth * (this.length)}px`;*/
            this.$nextTick(() => {
                if (!this.itemScroll) {
                  this.itemScroll = new BScroll(this.$refs.itemWrapper, {
                    bounceTime: 300,
                    click: true,
                    scrollX: true,                        // 横向滚动
                    eventPassthrough: "vertical"        // 在横向滚动时忽略纵向滚动
                  });
                } else {
                  this.itemScroll.refresh();
                }


                if (!this.goodsScroll) {
                  this.goodsScroll = new BScroll(this.$refs.outWrapper, {
                    bounceTime: 300,
                    click: true,
                    probeTimer:3,
                    scrollX: true,
                  });
                } else {
                  this.goodsScroll.refresh();
                }

              }
            );
          }
        });

      },

      _calculateWidth() {
        let length = this.length;
        let width = 0;
        this.distance.push(width);
        //console.log(length);
        for(let i=0;i<length;i++) {
          width += this.fullWidth;
          this.distance.push(width);
        }
        //console.log(this.distance)
      },

      showItemList(e,item_message,index) {
        if(e.currentTarget.className === "command"||"command active-item") {
          this.activeType = -1;
          console.log(e.currentTarget.className,111)
        }else{
          this.activeType = item_message.id;
          console.log(e.currentTarget.className,222)
        }
        let goodsList = this.$refs.goodsType;
        let el = goodsList[index];
        this.goodsScroll.scrollToElement(el,300);
      },

      selectItem(goods,$goodsindex) {
        this.selectedindex = $goodsindex;
        console.log(this.selectedindex,$goodsindex)
      }

    },

    computed:{

    },

    components:{

    }
  }
</script>

<style scoped>

  .tab-wrapper {
    position: fixed;
    bottom: 0;
    width: 100%;
    height: 230px;
    box-sizing: border-box;
    transform: translate(0,0%);
    overflow: hidden;
    white-space: nowrap;
    z-index: 30;
    background-color: rgba(0,0,0,.3);
  }

  .tab-content {
    height: 40px;
    width: 100%;
  }

  .item-list {
    font-size: 0;
    padding-left: 0;
    color: rgb(255,255,255);
    box-sizing: border-box;
  }

  .clear {
    display: inline-block;
    height: 40px;
    line-height: 40px;
    width: 40px;
    text-align: center;
    font-size: 15px;
    list-style-type: none;
    vertical-align: middle;
  }

  .img-clear {
    height: 20px;
    width: 20px;
    margin: 0 auto;
  }

  .command {
    display: inline-block;
    height: 40px;
    line-height: 40px;
    width: 67px;
    text-align: center;
    font-size: 15px;
    list-style-type: none;
  }

  .item {
    display: inline-block;
    height: 40px;
    line-height: 40px;
    width: 67px;
    text-align: center;
    font-size: 15px;
    list-style-type: none;
  }



  .item:last-child {
    margin-right: 0;
    border-right: none;
  }

  .item-name,.item-avatar {

  }

  .active-item{
    color: rgb(255,189,69);
  }


  .goods-content {
    overflow: hidden;
  }

  .goods-wrapper {
    position: absolute;
    width: 100%;
    top: 40px;
    bottom: 0;
    overflow: hidden;
    font-size: 0;
    border-top: 2px solid rgba(242,242,242,.15);
    box-sizing: border-box;
    background-color: rgba(0,0,0,.3);
  }

  .goods-type-wrapper {

  }

  .goods-type {
    display: inline-block;
    width: 375px;
    min-height: 188px;
    margin: 0;
    padding: 0;
  }

  .goods-list {
    display: flex;
    flex-wrap: wrap;
    margin: 0;
    padding: 0;
  }

  .goods-item {
    text-align: center;
    list-style-type: none;
    flex: 0 75px;
  }

  .selected-item {
    box-sizing: border-box;
    border-radius: 10px;
    border: 2px solid rgb(255,189,69);
    overflow: hidden;
    height: 75px;
  }

  .selected-item img{
    border-radius: 10px;
  }


  .test {
    width: 200px;
    height: 200px;
    z-index: 500;
  }
</style>
