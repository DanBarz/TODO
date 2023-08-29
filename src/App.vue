<script setup>
import { ref, computed } from 'vue';

const all = ref([
  { value: "Mow the lawns", selected: false },
  { value: "Clean the fridge", selected: true },
  { value: "Play in garage", selected: true },
  { value: "Weed the garden", selected: false }
]);
const inputItem = ref("");

const selectedItems = computed(() => {
  return all.value.filter(item => item.selected);
});

function create() {
  const value = inputItem.value;
  const selected = false;
  all.value.push({ value, selected });
  inputItem.value = '';  // Reset the input field after adding
}

function removeTodo (itemToRemove) {
    const index = all.value.findIndex(item => item.value === itemToRemove.value);
    if (index !== -1) {
        all.value.splice(index, 1);
        saveData();
    }
}

</script>

<template>
<div class="card">
  <div class="card-title">
    <h1>Magic TO-DO</h1>
  </div>
  <div class="card-content">
    <p>Task 2.1C - Exploring Vue</p>
  </div>
  
  <div class="card-title">
    <h2>Today's Stuff!</h2>
  </div>
  
  <div id="today" >
    <p><li v-for="item in selectedItems" :key="item.value">
    {{ item.value }}
    <button @click="removeTodo(item)">Remove</button>
</li></p>
</div>
  
  <div class="card-title">
    <h2>All the Stuff! </h2>
  </div>
  
  <div id="all">
    <br>
    <p>Enter a new ToDo item:</p>
    <input class="input" type="text" v-model="inputItem" />
    <button @click="create">Create</button>
    <br>
    
    <ul>
      <p>
        <li v-for="item in all" :key="item.value">
        {{ item.value }}
        <input type="checkbox" v-model="item.selected"> Today
      </li>
      </p>
    </ul>
    {{ all }}
  </div>
</div>
</template>

<style scoped>
.card {
  min-height: calc(100vh - 150px);
  background: #333;
  padding: 3em;
  border-radius: 10px;
  color: white;
}

.card .input {
  padding: 0.5em;
  border-radius: 5px;
  border: 1px solid #ccc;
  width: 80%;
  margin-right: 1em;
}

.card .card-title {
  display: flex;
  justify-content: center;
  padding: 1em;
  align-items: center;
  background: #222;
  border-radius: 20px;
}
.card-content p {
  line-height: 1.5;
  margin: 30px auto;
}

p {
  margin: 1em;
  font-size: large;
  font-family: Arial, Helvetica, sans-serif;
}



button {
  padding: 0.25em;
  margin: 0.35em;
  border-radius: 5px;
  border: 1px solid #ccc;
  background: #222;
  color: white;
}

@media screen and (max-width: 530px) {
  .card {
    padding: 1em;
  }
}
</style>
