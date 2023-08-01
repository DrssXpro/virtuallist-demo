<template>
  <div class="test-estimated-list-container">
    <FsEstimatedVirtualList :data-source="dataSource" :loading="loading" :estimated-height="60" @getMoreData="addData">
      <template #item="{ item }">
        <div class="list-item">{{ item.id }} - {{ item.content }}</div>
      </template>
    </FsEstimatedVirtualList>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue";
import Mock from "mockjs";
import FsEstimatedVirtualList from "../components/FsEstimatedVirtualList.vue";

const dataSource = ref<
  Array<{
    id: number;
    content: string;
  }>
>([]);

const loading = ref(false);

const addData = () => {
  loading.value = true;
  setTimeout(() => {
    const newData = [];
    for (let i = 0; i < 20; i++) {
      const len: number = dataSource.value.length + newData.length;
      newData.push({
        id: len,
        content: Mock.mock("@csentence(40, 100)"), // 内容
      });
    }
    dataSource.value = [...dataSource.value, ...newData];
    loading.value = false;
  }, 2000);
};

onMounted(() => {
  addData();
});
</script>

<style scoped lang="scss">
.test-estimated-list-container {
  width: 100%;
  height: 100%;
}
.list-item {
  border: 1px solid #000;
  padding: 10px;
  letter-spacing: 0.1em;
}
</style>
