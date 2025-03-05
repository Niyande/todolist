<script setup>
import ListItem from './ListItem.vue'
import NewItemPopup from './NewItemPopup.vue'
import { ref } from 'vue'

const items = ref([{ content: 'Foo' }, { content: 'Bar' }])
const isPopupOpened = ref(false);
const popupArea=ref(null)

const openPopup = () => {
  isPopupOpened.value = true;
}

const closePopup = () => {
  isPopupOpened.value = false;
}

const addListItem = (content) => {
  items.value.unshift({content: content})
}

const removeListItem = (index) => {
  items.value.splice(index, 1)
}

</script>

<template>
  <main>
    <div class="wrapper">
      <h1 class="green">Lista zadań</h1>
      <button @click="openPopup">
        <img alt="plus button" src="../assets/square-plus.svg" width="50" height="50" />
      </button>
    </div>
    <NewItemPopup :isOpen="isPopupOpened" @modal-close="closePopup" @submit="addListItem(popupArea)" name="first-modal">
      <template #input>
        <textarea ref="popupArea" placeholder="Wpisz treść zadania..."></textarea>
      </template>
      <template #footer>
        <div>
          <button @click="addListItem(popupArea.value),closePopup()">Submit</button>
        </div>
      </template>
    </NewItemPopup>
    <div class="wrapper" id="list">
      <ListItem v-for="item in items">
        <template #content>{{ item.content }}</template>
        <template #delete>
          <button @click="removeListItem(items.indexOf(item))">
            <img alt="delete" src="../assets/trash.svg" width="50" height="50" />
          </button>
        </template>
      </ListItem>
    </div>
  </main>
</template>

<style scoped>
#list {
  width: 300px;
}
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.wrapper
{
  display: flex;
  place-items: flex-start;
  flex-wrap:wrap;
}
</style>