<template>
  <div class="splice-app" :style="`grid-template-columns: repeat(${nums},1fr)`">
    <div class="splice-item" v-for="item in items" :key="item.id"></div>
  </div>
</template>

<script>
export default {
  data(){
    return {}
  },
  props: {
    nums: {
      type: Number,
      require: true,
      default: 2
    }
  },
  computed: {
    items : function(){
      let items = [];
      for (let index = 0; index < this.nums*this.nums; index++) {
        items.push({
          id: index
        })
      }
      return items
    }
  }
}
</script>

<style lang="scss" scoped>
.splice-app {
  position: absolute;
  width: 100vw;
  height: 100vh;
  display: grid;
  .splice-item {
    box-shadow: 1px 1px #ffffff;
  }
}
</style>