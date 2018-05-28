<template>
  <div class="goods-content">
    <div class="goods-wrapper" ref="outWrapper">
      <div class="goods-type-wrapper" ref="innerWrapper" :style="this.listWidth">
        <div class="goods-type" v-for="(item_message,itemName,index) in items" ref="goodsType" :style="screenWidth">
          <ul class="goods-list" :class="itemName">
            <li class="goods-item" v-for="(goods,index) in item_message.goods">
              <a class="goods-link">
                <!--<span class="item-name">{{item.name}}</span>-->
                <img :src="goods.avatar" alt="item.name" class="item-img"
                     height="75px" width="75px" >
              </a>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

    import BScroll from "better-scroll"

    export default {
      name: "list",
      props:{
        items:{
          type:Object
        },
        listWidth:{
          type:String
        },
        show:{
          type:Boolean
        },
        screenWidth:{
          type:String
        },
        fullWidth:{
          type:Number
        }
      },
      data() {
        return {
          selected:{},
          flag:false
        }
      },

      created() {

      },

      watch: {
        "items"() {
          this.$nextTick(() => {
            this._initScroll();
          });
        },
      },

      mounted() {

        this.$nextTick(() => {
          this._initScroll();

        })
      },

      methods:{
        _initScroll() {

          this.$nextTick(() => {
            if (!this.scroll) {
              this.scroll = new BScroll(this.$refs.outWrapper, {
                preventDefault: true,
                scrollX:true,
                scrollY:true,
              });
            } else {
              this.scroll.refresh();
            }
          })
        },

        itemScroll(el) {
          this.scroll.scrollToElement(el,300);
        }
      }
    }
</script>

<style scoped>

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


</style>
