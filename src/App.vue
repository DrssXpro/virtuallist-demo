<template>
  <div class="app">
    <div class="work-space">
      <div class="tip">不定高虚拟列表</div>
      <EstimatedListContainer />
    </div>
    <div class="work-space">
      <div class="tip">定高虚拟列表</div>
      <ListContainer />
    </div>
  </div>
</template>

<script setup lang="ts">
import EstimatedListContainer from "./views/estimated-list-container.vue";
import ListContainer from "./views/list-container.vue";
</script>

<style scoped lang="scss">
.app {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
  .work-space {
    position: relative;
    width: 40vw;
    height: 80vh;
    max-width: 450px;
    border: 1px solid red;
    padding: 20px;
    .tip {
      position: absolute;
      top: -30px;
      width: 100%;
      text-align: center;
    }
  }
}
</style>
