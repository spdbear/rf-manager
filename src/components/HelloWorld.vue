<template>
  <h1>{{ msg }}</h1>

  <p>See <code>README.md</code> for more information.</p>

  <n-button @click="count++">count is: {{ count }}</n-button>
</template>

<script lang="ts">
import { ref, defineComponent } from "vue";
import { NButton } from "naive-ui";
export default defineComponent({
  name: "HelloWorld",
  components: {
    NButton,
  },
  props: {
    msg: {
      type: String,
      required: true,
    },
  },
  setup: () => {
    const count = ref(0);
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
