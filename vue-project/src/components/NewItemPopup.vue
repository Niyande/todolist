<script setup>
import { useTemplateRef, ref } from "vue";
import { onClickOutside } from '@vueuse/core'

const props = defineProps({
  isOpen: Boolean,
});

const emit = defineEmits(["modal-close", "addListItem"]);

const target = ref(null)
onClickOutside(target, ()=>emit('modal-close'))

const input = useTemplateRef('popupArea');
</script>

<template>
  <div v-if="isOpen" class="modal-mask">
    <div class="modal-wrapper">
      <div class="modal-container" ref="target">
        <div class="input-group">
          <textarea class="input" ref="popupArea" placeholder="Wpisz treść zadania..." autocomplete="off" style="resize: none"></textarea>
          <input class="button--submit" value="Dodaj" type="submit" @click="emit('addListItem', input.value); emit('modal-close')">
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
  @property --rotation {
    syntax: "<angle>";
    inherits: false;
    initial-value: 0deg;
  }

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
    color: var(--color-text);
    background-color: var(--color-background);
    font-size: 15px;
    border: 1px solid rgb(100, 61, 219);
    border-radius: 6px;
  }

  .input-group {
    display: flex;
    align-items: center;
  }

  .input {
    min-height: 50px;
    height: 4rlh;
    width: 100%;
    padding: 0 1rem;
    color: var(--color-text);
    background-color: var(--color-background);
    font-size: 15px;
    border: 1px solid rgb(100, 61, 219);
    border-radius: 6px 0 0 6px;
    scrollbar-color: rgb(100, 61, 219) transparent;
  }

  .button--submit {
    min-height: 50px;
    height: 4rlh;
    padding: .5em 1em;
    border: none;
    border-radius: 0 6px 6px 0;
    background-image: linear-gradient(var(--rotation), rgb(100, 61, 219), rgb(217, 21, 239));
    color: #fff;
    font-size: 15px;
    cursor: pointer;
    transition: --rotation 1s;
    --rotation: 45deg;
  }

  .button--submit:hover {
    --rotation: 225deg;
  }

  .input:focus, .input:focus-visible {
    outline: none;
  }
</style>


