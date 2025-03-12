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
          <div class="button-wrapper">
            <input class="button--submit" value="Usuń" type="submit" @click="emit('deleteListItem'); emit('modal-close')">
            <input class="button--submit" value="Anuluj" type="submit" @click="emit('modal-close')">
          </div>
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
    padding: 20px 30px;
    color: var(--color-text);
    background-color: var(--color-background);
    font-size: 15px;
    border: 1px solid rgb(100, 61, 219);
    border-radius: 6px;
  }

  .input-group {
    display: flex;
    flex-direction: column;
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
    margin: auto;
    min-height: 50px;
    padding: .5em 1em;
    border: none;
    border-radius: 6px;
    background-image: linear-gradient(var(--rotation), rgb(100, 61, 219) 0%, rgb(217, 21, 239) 100%);
    color: #fff;
    font-size: 15px;
    cursor: pointer;
    --rotation: 45deg;
    transition: --rotation 1s;
  }

  .button--submit:hover {
    --rotation: 225deg;
  }

  .input:focus, .input:focus-visible {
    outline: none;
  }

  .button-wrapper
  {
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
  }

  p {
    width: 100%;
    text-align: center;
    margin-bottom: 1em;
  }
</style>


