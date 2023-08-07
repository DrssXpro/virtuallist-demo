<template>
  <div class="virtual-waterfall-container">
    <fs-virtual-water-fall :request="req" :gap="15" :column="6" :request-size="30">
      <template #item="{ item }">
        <img class="test-item" :src="item.src" />
      </template>
    </fs-virtual-water-fall>
  </div>
</template>

<script setup lang="ts">
import FsVirtualWaterFall from "../components/FsVirtualWaterFall.vue";
import type { FsVirtualWaterfallReuqest } from "../components/type";

const req: FsVirtualWaterfallReuqest = async (page, pageSize) => {
  // 请求，并传入分页参数
  const rep = await fetch(
    `https://www.vilipix.com/api/v1/picture/public?limit=${pageSize}&sort=hot&offset=${--page * pageSize}`
  );
  // 数据处理
  let {
    data: { rows, count },
  } = await rep.json();
  rows = rows.map((item: any) => ({
    id: item.picture_id, 
    width: item.width, 
    height: item.height, 
    src: item.regular_url + "?x-oss-process=image/resize,w_240/format,jpg",
  }));

  return {
    total: count,
    list: rows,
  };
};
</script>

<style scoped lang="scss">
.virtual-waterfall-container {
  width: 100%;
  height: 100%;
}
.test-item {
  width: 100%;
  height: 100%;
  box-sizing: border-box;
  animation: identifier 0.25s; // 添加动画，使其出现时更加丝滑
}
@keyframes identifier {
  from {
    opacity: 0;
    transform: translateY(200px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
