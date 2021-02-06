<template>
  <div class="splice-app" :style="customStyle">
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
    },
    position: {
      type: Object,
      require: true
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
    },
    customStyle : function() {
      return {
        "grid-template-columns": `repeat(${this.nums}, 1fr)`,
        ...this.position
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.splice-app {
  position: absolute;
  display: grid;
  .splice-item {
    box-shadow: 1px 1px #f2aaaa;
  }
}
</style>