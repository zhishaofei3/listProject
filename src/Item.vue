<template>
  <div class="item" :id="item.id">
    <div class="content" v-html="item.showContent"></div>
  </div>
</template>

<script>
  export default {
    name: "Item",
    props: {
      item: Object
    }
  }
</script>
<style>
  .item {
    background-color: hotpink;
    margin-bottom: 10px;
    position: relative;
  }

  .item .content {
    position: relative;
    min-height: 200px;
  }

  .item .content img {
    width: 100%;
  }

  .tags {
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
  }

  .tags a {
    position: absolute;
    width: 10px;
    height: 10px;
    background-color: #3ABB51;
    border-radius: 50%;
  }
</style>


