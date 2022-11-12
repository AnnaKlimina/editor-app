<template>
  <button class="create-button" @click="$emit('showJson')">
    Сгенерировать JSON
  </button>
</template>

<script>
export default {
  name: "CreateButton",
};
</script>

<style>
.create-button {
  margin: 10px;
  width: fit-content;
  background: linear-gradient(36deg, #fce181 30%, white 50%, #fce181 70%);
  padding: 10px;
  border: 2px solid #b4a063;
  border-radius: 5px;
  font-weight: 700;
  color: #6f4610;
}

.create-button:hover {
  opacity: 0.7;
}

.create-button:active {
  background: linear-gradient(36deg, #bebebe 30%, white 50%, #bebebe 70%);
  border: 2px solid #bebebe;
  color: black;
}
</style>
