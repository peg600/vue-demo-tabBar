<template>
  <div>
    <div class="wrapper" v-if="showList">
      <ul class="list-wrapper">
        <li class="list-item" v-for="(item,index) in itemMessage.goods">
          <div class="content">
            <span class="item-name">{{item.name}}</span>
            <img :src="item.avatar" alt="item.name" class="item-img"
            height="30px" width="30px" >
            <span class="item-price">{{item.price}}</span>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
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
      
    }
</script>

<style scoped>
  .wrapper {
    height: 300px;
    width: 100%;
    margin-top: 10px;
    background-color: red;
    z-index: 10;
  }

  .list-wrapper {
    display: flex;
    flex-wrap: wrap;
  }

  .list-item {
    list-style-type: none;
  }


</style>
