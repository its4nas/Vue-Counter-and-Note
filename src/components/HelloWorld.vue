<script setup>
import { ref } from 'vue'

const count = ref(0)
</script>

<template>

  <div class="card">
    <button @click="count++">increase</button>
    <h1>counter is {{ count }}</h1>
    <button type="button" @click="count--">decrease</button>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
