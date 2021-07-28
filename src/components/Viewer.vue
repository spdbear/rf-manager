<template>
  <img src="../assets/notes/1-1-3.png" />
</template>

<script lang="ts">
import { ref, defineComponent, computed } from 'vue'
import { NButton } from 'naive-ui'
import { bmsSource } from '../assets/notes/35'
// import { Compiler, SongInfo, Notes } from "bms";

export default defineComponent({
  name: 'Viewer',
  components: {
    NButton,
  },
  setup: () => {
    const count = ref(0)
    const imgSrc = computed(() => require('../assets/notes/1-1-3.png'))
    return { count, imgSrc }
  },
})
</script>

<style scoped>
a {
  color: #42b983;
}

label {
  margin: 0 0.5em;
  font-weight: bold;
}

code {
  background-color: #eee;
  padding: 2px 4px;
  border-radius: 4px;
  color: #304455;
}
</style>
