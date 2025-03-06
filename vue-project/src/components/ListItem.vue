<script setup lang="ts">
  import Checkbox from './checkbox.vue';
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
  margin-bottom: 1rem;
  display: flex;
  position: relative;
  border: 2px solid var(--color-border);
  border-radius: 8px;
}

.content {
  width: 150px;
  margin-left: 50px;
}
</style>
