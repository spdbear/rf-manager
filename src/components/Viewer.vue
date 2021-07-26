<template>
  <p>See <code>README.md</code> for more information.</p>

  <n-button @click="count++">count is: {{ count }}</n-button>
</template>

<script lang="ts">
import { ref, defineComponent } from "vue";
import { NButton } from "naive-ui";
import { bmsSource } from "../assets/notes/35";
// import { Compiler, SongInfo, Notes } from "bms";

export default defineComponent({
  name: "Viewer",
  components: {
    NButton,
  },
  setup: () => {
    const count = ref(0);

    // const compileResult = Compiler.compile(bmsSource);
    // const chart = compileResult.chart;
    // const info = SongInfo.fromBMSChart(chart);
    // const notes = Notes.fromBMSChart(chart);
    // console.log(info);
    // const hasColumnNotes = notes.all().filter((n) => n.column);
    // console.log(hasColumnNotes);
    return { count };
  },
});
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
