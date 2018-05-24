<template>
  <div>
    <div class="wrapper" v-if="showList">
      <ul class="list-wrapper">
        <li class="list-item" v-for=""></li>
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
        showList
      }
    }
</script>

<style scoped>

</style>
