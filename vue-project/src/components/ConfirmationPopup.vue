<script setup>
import { useTemplateRef, ref } from "vue";
import { onClickOutside } from '@vueuse/core'

const props = defineProps({
  isOpen: Boolean,
});

const emit = defineEmits(["modal-close", "deleteListItem"]);

const target = ref(null)
onClickOutside(target, ()=>emit('modal-close'))

const input = useTemplateRef('popupArea');
</script>

<template>
  <div v-if="isOpen" class="modal-mask">
    <div class="modal-wrapper">
      <div class="modal-container" ref="target">
        <div class="input-group">
          <p> Czy na pewno chcesz usunąć to zadanie?</p>
          <input class="button--submit" value="Usuń" type="submit" @click="emit('deleteListItem'); emit('modal-close')">
          <input class="button--submit" value="Anuluj" type="submit" @click="emit('modal-close')">
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

  .modal-mask {
    position: fixed;
    z-index: 9998;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
  }
  .modal-container {
    width: 300px;
    margin: 150px auto;
    padding: 20px 30px;
  }

  .input-group {
    display: flex;
    align-items: center;
  }

  .input {
    min-height: 50px;
    max-width: 150px;
    padding: 0 1rem;
    color: var(--color-text);
    background-color: var(--color-background);
    font-size: 15px;
    border: 1px solid rgb(100, 61, 219);
    border-radius: 6px 0 0 6px;
  }

  .button--submit {
    min-height: 50px;
    padding: .5em 1em;
    border: none;
    border-radius: 0 6px 6px 0;
    background-image: linear-gradient(45deg, rgb(100, 61, 219) 0%, rgb(217, 21, 239) 100%);
    color: #fff;
    font-size: 15px;
    cursor: pointer;
    transition: background-color .3s ease-in-out;
  }

  .button--submit:hover {
    background-image: linear-gradient(45deg, rgb(100, 61, 219) 0%, rgb(217, 21, 239) 100%);
  }

  .input:focus, .input:focus-visible {
    outline: none;
  }
</style>


