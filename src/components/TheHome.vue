<script setup>
import { ref, onBeforeMount } from 'vue';
import TreeNode from './TreeNode.vue';

defineProps({
  msg: {
    type: String,
    required: true,
  },
});

const data = ref(null);

onBeforeMount(() => {
  setTimeout(async () => {
    const response = await fetch('data.json');
    data.value = await response.json();
  }, 1000);
});
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <TreeNode :node="data.root" v-if="data" />
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
