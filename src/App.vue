<template>
  <div class="p-5 pl-96 pr-96 space-y-2 w-screen h-screen bg-gray-100">
    <Select v-model="items" label="Status" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Select from './components/Select.vue'

export default defineComponent({
  name: 'App',
  components: { Select },
})
</script>
