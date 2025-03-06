<script setup>
import ListItem from './ListItem.vue'
import NewItemPopup from './NewItemPopup.vue'
import { ref } from 'vue'
import Trashcan from './Trashcan.vue';
import PlusButton from './PlusButton.vue';

const items = ref([{ content: 'Foo', checked: false }, { content: 'Bar', checked: true}])
const isPopupOpened = ref(false);
const popupArea=ref(null)

const openPopup = () => {
  isPopupOpened.value = true;
}

const closePopup = () => {
  isPopupOpened.value = false;
}

const addListItem = (content) => {
  items.value.unshift({content: content, checked: false})
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
        <PlusButton/>
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
      <ListItem v-for="item in items" v-model:checked="item.checked">
        <template #content>{{ item.content }}</template>
        <template #delete>
          <button @click="removeListItem(items.indexOf(item))" style="height: 100%; margin: 0.5em;">
            <Trashcan/>
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