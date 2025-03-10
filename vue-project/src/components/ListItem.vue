<script setup lang="ts">
  import Checkbox from './Checkbox.vue';
  const checked = defineModel('checked')
</script>

<template>
  <div class="item">
    <Checkbox v-model:checked="checked"/>
    <p class="content">
      <slot name="content"></slot>
    </p>
    <slot name="delete"></slot>
  </div>
</template>

<style scoped>
.item {
  display: flex;
  position: relative;
  border-bottom: 2px solid rgb(217, 21, 239);
  border-radius: 8px;
  width: 100%;
}

.content {
  width: 100%;
  margin-left: 50px;
}
</style>
