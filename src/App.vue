<template>
  <div class="app">
    <div class="work-space">
      <el-tabs v-model="activeName" class="demo-tabs" @tab-click="handleClick">
        <el-tab-pane label="定高虚拟列表" name="first" lazy>
          <div class="list-container">
            <list-container />
          </div>
        </el-tab-pane>
        <el-tab-pane label="不定高虚拟列表" name="second" lazy>
          <div class="list-container">
            <estimated-list-container /></div
        ></el-tab-pane>
        <el-tab-pane label="瀑布流列表" name="third" lazy>
          <div class="waterfall-container">
            <waterfall-container />
          </div>
        </el-tab-pane>
        <el-tab-pane label="瀑布流虚拟列表" name="fourth" lazy>
          <div class="waterfall-container">
            <virtual-waterfall-container />
          </div>
        </el-tab-pane>
      </el-tabs>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import EstimatedListContainer from "./views/estimated-list-container.vue";
import ListContainer from "./views/list-container.vue";
import waterfallContainer from "./views/waterfall-container.vue";
import virtualWaterfallContainer from "./views/virtual-waterfall-container.vue";
import type { TabsPaneContext } from "element-plus";

const activeName = ref("first");

const handleClick = (tab: TabsPaneContext, event: Event) => {
  console.log(tab, event);
};
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
    width: 60vw;
    height: 90vh;
    .list-container {
      width: 100%;
      height: 80vh;
      max-width: 450px;
    }
    .waterfall-container {
      width: 100%;
      height: 80vh;
    }
  }
}
</style>
