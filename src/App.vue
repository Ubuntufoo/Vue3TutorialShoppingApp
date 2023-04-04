<script setup>
import { ref, computed } from 'vue'

const header = ref('Shopping List App')

const editing = ref(false)
const items = ref([
  { id: 1, label: "10 Party Hats", purchased: true, highPriority: false },
  { id: 2, label: "2 Board Games", purchased: true, highPriority: false },
  { id: 3, label: "20 Cups", purchased: false, highPriority: true },
])
//spread ("copy") operator used to ensure orig 'items' variable not mutated
const reversedItems = computed(() => [...items.value].reverse())
const newItem = ref("")
const newItemHighPriority = ref(false)
const saveItem = () => {
  items.value.push(
    {
      id: items.value.length + 1,
      label: newItem.value,
      highPriority: newItemHighPriority.value
    })
  newItem.value = ""
  newItemHighPriority.value = ""
}
const doEdit = (e) => {
  editing.value = e
  newItem.value = ""
}
const togglePurchased = (item) => {
  item.purchased = !item.purchased
}
</script>

<template>
  <div class="container w-50">
    <div class="header">
      <h1 class="m-3 text-center">{{ header }}</h1>
      <button v-if="editing" class="btn btn-secondary mt-2 mb-2" @click="doEdit(false)">
        Cancel
      </button>
      <button v-else class="btn btn-primary mt-2 mb-2" @click="doEdit(true)">
        Add Item
      </button>
    </div>

    <form class="add-item-form" v-if="editing" @submit.prevent="saveItem">
      <div class="form-group">
        <input id="newItem" v-model.trim="newItem" type="text" class="form-control" placeholder="eg. Eggs">
      </div>

      <div class="form-group mt-2 mb-2">
        <div class="form-check form-check-inline">
          <input id="highPriority" type="checkbox" v-model="newItemHighPriority" class="form-check-input">
          <label for="highPriority" class="form-check-label">High Priority</label>
        </div>

        <button :disabled="newItem.length < 5" class="btn btn-primary">
          Save Item
        </button>
      </div>
    </form>

    <ul class="list-group">
      <li v-for="(item, index) in reversedItems" @click="togglePurchased(item)" :key="item.id"
        :class="['list-group-item', item.purchased ? 'text-decoration-line-through' : '', item.highPriority ? 'list-group-item-danger' : '']">
        {{ item.label }}

      </li>
    </ul>

    <div v-if="!items.length" class="text-center">
      <button class="btn btn-primary" @click="doEdit(true)">Add Item</button>
    </div>
  </div>
</template>
