<script setup>
import { reactive, onMounted } from 'vue';

onMounted(() => {
  console.log(props.node);
});
// Принимаем узел через props
const props = defineProps({
  node: {
    type: Object,
    required: true,
  },
});

// Состояния открыта/закрыта папка
const openFolders = reactive({});

// Функция переключения видимости детей
const toggle = (name) => {
  openFolders[name] = !openFolders[name];
  console.log(openFolders);
};
</script>

<template>
  <div class="tree-node">
    <div v-for="(item, name) in node" :key="name">
      <div @click="item.type === 'folder' && toggle(name)" class="node-label">
        <span>{{ item.type === 'folder' ? (openFolders[name] ? 'v' : '>') : '-' }}</span>
        <span>{{ name }}</span>
      </div>

      <TreeNode v-if="item.type === 'folder' && openFolders[name]" :node="item.children" />
    </div>
  </div>
</template>

<style scoped>
.tree-node {
  margin-left: 16px;
  cursor: pointer;
}
.node-label {
  display: flex;
  align-items: center;
  gap: 6px;
  padding: 2px 0;
}
</style>
