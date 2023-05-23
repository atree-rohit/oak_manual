<style scoped>
.root-container {
  display: flex;
  flex-direction: column;
  /* align-items: center; */
  /* justify-content: center; */
  margin: 0.5rem;
  padding: 0.5rem;
  height: 100vh;
}
</style>

<template>
  <div class="root-container">
    <table-of-contents />
  </div>
</template>

<script lang="ts">
import TableOfContents from './components/TableOfContents.vue'
import {defineComponent} from 'vue'
export default defineComponent({
  name: 'App',
  components: {
    TableOfContents
  }
})
</script>