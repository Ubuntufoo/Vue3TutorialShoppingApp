<script setup>
import { ref } from 'vue'

const header = ref('Shopping List App')
const items = ref([
  { id: 1, label: "10 Party Hats" },
  { id: 2, label: "2 Board Games" },
  { id: 3, label: "20 Cups" },
])
const newItem = ref("")
const newItemHighPriority = ref(false)
const iceCreamFlavors = ref([])
</script>

<template>
  <div class="container-fluid">
    <h1>{{ header }}</h1>
    <form class="add-item-form" @submit.prevent="items.push({ id: items.length + 1, label: newItem })">
      <input v-model.trim="newItem" type="text" placeholder="Add an item" size="20">
      <div class="">
        <div class="">
          Priority:
        </div>
        <div class="">
          <label>
            <input type="checkbox" v-model="newItemHighPriority">
            High Priority
          </label>
          <button class="btn btn-primary">
            Save Item
          </button>
        </div>
      </div>
    </form>
    <ul>
      <li v-for="({ id, label }, index) in items" :key="id">
        {{ label }}
      </li>
    </ul>
  </div>
</template>