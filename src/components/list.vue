<template>
  <div>
    <div class="wrapper" v-if="showList" ref="listContent">
      <ul class="list-wrapper">
        <li class="list-item" v-for="(item,index) in itemMessage.goods" ref="listItem">
          <a class="content">
            <span class="item-name">{{item.name}}</span>
            <img :src="item.avatar" alt="item.name" class="item-img"
            height="30px" width="30px" >
          </a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>

    import BScroll from "better-scroll"

    export default {
      name: "list",
      props:{
        itemMessage:{
          type:Object
        },
        showList:{
          type:Boolean
        }
      },

      watch:{
        "itemMessage"() {
          this.$nextTick(() => {
            this._initScroll();
          });
        }
      },

      methods:{
        _initScroll() {
          if (!this.scroll) {
            this.scroll = new BScroll(this.$refs.listContent, {
              click: true
            });
          } else {
            this.scroll.refresh();
          }
        },
      }
    }
</script>

<style scoped>
  .wrapper {
    position: absolute;
    width: 100%;
    top: 50px;
    bottom: 0;
    overflow: hidden;
    box-sizing: border-box;
    background-color: red;
  }

  .list-wrapper {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    padding: 0 10px;
  }

  .list-item {
    text-align: center;
    list-style-type: none;
    flex: 1 1 33.33%;
  }


</style>
