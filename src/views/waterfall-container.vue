<template>
  <div class="waterfall-container">
    <FsWaterFall :gap="20" :column="6" :request="requestData" :page-size="30">
      <template #item="{ item }">
        <el-image :src="item.url" alt="图片" class="image" lazy></el-image>
      </template>
    </FsWaterFall>
  </div>
</template>

<script setup lang="ts">
import FsWaterFall from "../components/FsWaterFall.vue";
import type { IImageItem } from "../components/type";

const requestData = (page: number, pageSize: number): Promise<IImageItem[]> => {
  return new Promise<IImageItem[]>((resolve) => {
    fetch(`https://www.vilipix.com/api/v1/picture/public?limit=${pageSize}&sort=hot&offset=${--page * pageSize}`).then(async (res) => {
      const result = await res.json();
      const imageList: IImageItem[] = result.data.rows.map((i: any) => ({
        id: i.picture_id,
        url: i.original_url,
        height: i.height,
        width: i.width,
      }));
      resolve(imageList);
    });
  });
};
</script>

<style scoped lang="scss">
.waterfall-container {
  width: 100%;
  height: 100%;
  .image {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
}
</style>
