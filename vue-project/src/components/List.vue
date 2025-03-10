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
  console.log(content)
  items.value.unshift({content: content, checked: false})
}

const removeListItem = (index) => {
  items.value.splice(index, 1)
}

</script>

<template>
  <main>
    <div class="wrapper">
      <h1>Lista zadań</h1>
    </div>
    <NewItemPopup :isOpen="isPopupOpened" @modal-close="closePopup" @addListItem="addListItem" name="first-modal">
    </NewItemPopup>
    <div class="wrapper">
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
      <button id="add-button" @click="openPopup">
        <PlusButton/>
      </button>
    </div>
  </main>
</template>

<style scoped>
main {
  margin: 0 auto;
  padding: 2rem;
  width: 100rem;
  max-width: 400px;
}

#add-button {
  right: 0;
  top: 0;
  padding: 0;
  border: none;
  background-color: transparent;
}

#list {
  width: calc(100% - 3rem);
  border: 2px solid rgb(100, 61, 219);
  border-radius: 8px;
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

.wrapper
{
  display: flex;
  place-items: flex-start;
  flex-wrap:wrap;
}
</style>