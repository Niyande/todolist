<script setup>
import ListItem from './ListItem.vue'
import NewItemPopup from './NewItemPopup.vue'
import { ref } from 'vue'
import Trashcan from './Trashcan.vue';
import PlusButton from './PlusButton.vue';
import ConfirmationPopup from './ConfirmationPopup.vue';

const items = ref([{ content: 'Foo', checked: false }, { content: 'Bar', checked: true}])
const isAddPopupOpened = ref(false);
const isDeletePopupOpened = ref(false);
const deleteIndex = ref(null);

const openAddPopup = () => {
  isAddPopupOpened.value = true;
}

const closeAddPopup = () => {
  isAddPopupOpened.value = false;
}

const openDeletePopup = (index) => {
  isDeletePopupOpened.value = true;
  deleteIndex.value = index;
}

const closeDeletePopup = () => {
  isDeletePopupOpened.value = false;
}

const addListItem = (content) => {
  console.log(content)
  items.value.unshift({content: content, checked: false})
}

const removeListItem = () => {
  items.value.splice(deleteIndex.value, 1)
}

</script>

<template>
  <main>
    <div class="wrapper">
      <h1>Lista zadań</h1>
    </div>
    <NewItemPopup :isOpen="isAddPopupOpened" @modal-close="closeAddPopup" @addListItem="addListItem" name="first-modal"/>
    <ConfirmationPopup :isOpen="isDeletePopupOpened" @modal-close="closeDeletePopup" @deleteListItem="removeListItem" name="second-modal"/>
    <div class="wrapper">
      <div id="list">
        <ListItem v-for="item in items" v-model:checked="item.checked">
          <template #content>{{ item.content }}</template>
          <template #delete>
            <button class="delete-button" @click="openDeletePopup(items.indexOf(item))">
              <Trashcan/>
            </button>
          </template>
        </ListItem>
      </div>
      <button id="add-button" @click="openAddPopup">
        <PlusButton/>
      </button>
    </div>
  </main>
</template>

<style scoped>
main {
  padding: 0 2rem;
  margin: 0 2rem 0 calc(5rem + 0.5em);
  width: 100rem;
  max-width: 400px;
  height: 100vh;
}

#add-button {
  right: 0;
  top: 0;
  padding: 0;
  border: none;
  background-color: transparent;
  margin-left: 0.5em;
}

#list {
  width: calc(100% - 3rem - 0.5em);
  height: calc(100vh - 6rem);
  border: 2px solid rgb(100, 61, 219);
  border-radius: 8px;
  overflow-y: auto;
  scrollbar-color:rgb(100, 61, 219) transparent;
}
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  width: calc(100% - 3rem);
  background-image: linear-gradient(10deg, rgb(100, 61, 219) 0%, rgb(217, 21, 239) 100%);
  color: transparent;
  background-clip: text;
}

h3 {
  font-size: 1.2rem;
}

.delete-button {
  height: 2em;
  width: 2em;
  margin: 0.5em;
}

.wrapper
{
  display: flex;
  place-items: flex-start;
  flex-wrap:wrap;
}
</style>