<template>
  <h1 class="app__header">Editor</h1>
  <EditorMain />
</template>

<script>
import EditorMain from "./components/EditorMain.vue";

export default {
  name: "App",
  components: {
    EditorMain,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-size: 14px;
  display: grid;
  grid-template-columns: 1fr;
  padding: 0 20px;
  background: #edeae5;
  height: fit-content;
  min-height: 100vh;
}

body::-webkit-scrollbar {
  width: 16px;
}

body::-webkit-scrollbar-thumb {
  background: #e7cc69;
  box-shadow: inset 2px 5px 8px hsl(0deg 0% 100% / 0%),
    inset -4px -2px 4px rgb(0 0 0 / 70%);
  border-radius: 16px;
}

body::-webkit-scrollbar-track {
  background: #f2d87e;
}

.app__header {
  margin: 10px 5px 5px;
}

body {
  margin: 0;
  background: #fef9c7;
}
</style>
