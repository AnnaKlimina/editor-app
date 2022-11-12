<template>
  <div class="code-element">
    <h3 class="code-element__header">Ваш JSON</h3>
    <pre>
    <code class="code-element__code">{{jsonShown}}</code>
    </pre>
  </div>
</template>

<script>
export default {
  name: "CodeElement",
  props: ["jsonShown"],
};
</script>

<style>
.code-element {
  background: #fce181;
  margin: 20px auto;
  padding: 10px;
  min-width: 500px;
  max-width: 80vw;
}

.code-element__header {
  border-radius: 3px;
  margin: 10px;
  background: #f8f5d7;
  width: -moz-fit-content;
  width: fit-content;
  padding: 7px 10px;
  box-shadow: 0px 0px 5px #00000082;
}

.code-element__code {
  margin: 20px;
  display: block;
}
</style>
