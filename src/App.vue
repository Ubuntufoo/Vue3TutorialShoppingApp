<script setup>
import { ref } from 'vue'

const header = ref('Shopping List App')
const items = ref([
  { id: 1, label: "10 Party Hats" },
  { id: 2, label: "2 Board Games" },
  { id: 3, label: "20 Cups" },
])
const newItem = ref("")
const newItemPriority = ref("low")
</script>

<template>
  <div class="container-fluid">
    <h1>{{ header }}</h1>
    <div class="col-2 mt-3 mb-2">
      <input type="text" placeholder="Add an item" size="40">
    </div>
    <div class="row">
      <div class="col-1">
        Priority:
      </div>
      <div class="col-1">
        <label>
          <input type="radio" v-model="newItemPriority" value="low">
          Low
        </label>
      </div>
      <div class="col-1">
        <label>
          <input type="radio" v-model="newItemPriority" value="high">
          High
        </label>
      </div>
    </div>
    {{ newItemPriority }}
    <ul>
      <li v-for="({ id, label }, index) in items" :key="id">
        {{ label }}
      </li>
    </ul>
  </div>
</template>