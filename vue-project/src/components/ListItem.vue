<template>
  <div class="item">
    <input type="checkbox" class="checkbox"/>
    <p class="content">
      <slot name="content"></slot>
    </p>
    <slot name="delete"></slot>
  </div>
</template>

<style scoped>
.item {
  margin-bottom: 2rem;
  display: flex;
  position: relative;
  width: 100%;
  border: 2px solid var(--color-border);
  border-radius: 8px;
}

.checkbox {
  width: 50px;
  height: 50px;
}

.content {
  width: 150px;
  margin-left: 50px;
}
</style>
